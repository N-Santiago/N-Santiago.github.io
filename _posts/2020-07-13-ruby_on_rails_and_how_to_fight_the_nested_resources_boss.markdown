---
layout: post
title:      "Ruby on Rails and How to Fight the Nested Resources Boss"
date:       2020-07-13 18:45:07 +0000
permalink:  ruby_on_rails_and_how_to_fight_the_nested_resources_boss
---


Yes, this is how I'm calling my Rails Project Blog title. So it feels like that, like getting to the final boss and having a hard time. Just like a good old video game. 

![](https://i.pinimg.com/originals/1d/45/58/1d4558056f44793a1c6d0df3eaa4a3d8.gif)

For the Rails project, I decided to go ahead and continue with the "Small Reviews" project. In case this is the first blog post you read from me, Small Reviews is my real life movie review project. One of my goals in life is to Small Reviews (take from the spanish word "reseñita" who's kind of I would say "pequeña reseña" rather than "reseña" in my Puerto Rican slang) turn into this bigger website or app for people who share the same passion as me. 

For this project, we'll obviously make the whole CRUD structure for users to be able to create, read, update and delete the reviews with some restrictions left to the reviewer and user admin using gems Devise for authentication, Omniauth for Facebook users to log in (I decided Facebook cause I want this to be as close as the real Go-Live thing as possible and Devise for authentication. There's a lot of gems. Use them accordingly but be careful, don't get too greedy or addicted to them. 

![](https://miro.medium.com/max/640/0*oJVi5fNHnkkL6MGw.jpg)

After creating the users and allowing them to log on, I proceeded to add the reviews and categories tables to start talking about our favorite movies and categorize them by genres. To add a Nested Resource; what's better than adding comments? Like a author solving a writer's block by killing a character, I decided to make it simple by adding comments. After all, that's what we do on the Internet, comment, right? Well, nested resources will always feel like a labyrinth. 

![](https://i.dailymail.co.uk/i/pix/2015/01/08/2482200F00000578-2901789-image-a-15_1420716246493.jpg)

It was scary, but we can beat it. First, let's see the review and comment models. 

Review Model
```
class Review < ApplicationRecord
    belongs_to :user
    belongs_to :category
    has_many :comments, dependent: :destroy 
    # dependent: :destroy means the comments related 
    # to the specific review in mention get deleted if the post does.
    has_many :users, through: :comments
    validates :title, presence: true, length: { in: 3..30 }
    validates :content, presence: true, length: { maximum: 250 }
    default_scope { order(created_at: :desc)}
    #by default, the reviews will be displayed from newest to oldest.
end
```

Comment Model
```
class Comment < ApplicationRecord
    belongs_to :user
    belongs_to :review
    validates :content, presence: true, length: { maximum: 250 }
end 
```

The reviews will belong to the user, to a category and will have many comments and also many users through those comments. A comment will belong to the user who wrote it and the review in which was written. 

Now, let's take a look to the controllers.

Review Controller

```
class ReviewsController < ApplicationController
    before_action :set_review, only: [:show, :edit, :update, :destroy]
    before_action :authorize!, only: [:edit, :destroy]
    
    def index
      @reviews = Review.all
    end
  
    def new
      @review = Review.new
      @comment = Comment.new
      @comment.review_id = @review.id 
      #We need to declare the comments in the new action. 
    end
  
    def create
      @review = Review.new(review_params)
      @review.user_id = current_user.id
      if @review.save
        redirect_to review_path(@review)
      else
        render 'new' 
      end
    end
  
    def show
      @comment = Comment.new 
      #We also need to declare the new comment in the show action. 
    end
  
    def edit
    end
  
    def update
      if @review.update(review_params)
        redirect_to review_path(@review)
      else  
        render 'edit'
      end  
    end
  
    def destroy
      @review.destroy
      redirect_to reviews_path   
    end
  
    private

      def set_review
        @review = Review.find_by(id: params[:id])
    end 
  
      def review_params
        params.require(:review).permit(:title, :content, :category_id)
      end

      def authorize! 
        authorize @review #authorize method using the Pundit gem
    end 
end
```

Comment Controller 

```
class CommentsController < ApplicationController
    before_action :get_comment, only: [:edit, :update, :destroy]
    before_action :authorize!, only: [:edit, :destroy]
    before_action :set_comments, only: [:edit, :update, :destroy]

    def new
        @comment = Comment.new 
    end 

    def create
        @comment = Comment.new(comment_params)
        @comment.user_id = current_user.id
        @comment.review_id = params[:review_id]
        #Declare the review id. 
        @comment.save
        redirect_to review_path(@comment.review)
    end

    def edit
    end 

    def update
        @comment.update(comment_params)
        redirect_to review_path(@review)
    end 
  
    def destroy
        @comment.destroy
        redirect_to review_path(@review)
    end

    private #Very important helpers.

    def get_comment
        @comment = Comment.find_by(id: params[:id])
    end 

    def set_comments
        @review = @comment.review 
        @comments = @review.comments.find_by(id: params[:id])
    end 
        
    def comment_params
        params.require(:comment).permit(:content, :review_id)
    end 

    def authorize! 
        authorize @comment #authorize method using the Pundit gem
    end 

end
```

Now that we have the controllers, let's work out the code in the views. This is how the comment related codes will look like in our show review file. 

```
<% if user_signed_in? %>
<%= render partial: 'comments/form' %>
<% end %>
```
If the user is signed in, he'll be able to see the comment form rendered from file */views/comments/form *.

Here's the code from that helpful file. 

```
<%= form_for [ @review, @comment ] do |f| %>

    <% if @comment.errors.any? %>
        <div id="error_explanation">
            <h2>
            <%= pluralize(@comment.errors.count, "error") %>
            prohibited this comment from being saved:
            </h2>
 
        <ul>
            <% @comment.errors.full_messages.each do |msg| %>
            <li><%= msg %></li>
            <% end %>
        </ul>
        </div>
    <% end %>

  <p>
    <%= f.label :content, "What Do You Think?" %><br/>
    <%= f.hidden_field :review_id %>
    <%= f.text_area :content %>
  </p>
  <p>
    <%= f.submit 'Submit' %>
  </p>
<% end %>
```

As you can see, that form is iterating the errors and everything. Pretty cool. 

Now that we have the form, let's show those passionate film connoseurs comments. 

```
<% if @review.comments.present? %>
<h5>Comments:</h5>
<%= render partial: 'reviews/comment', collection: @review.comments %>
<% end %>
```
Here, we are stating the reviews will be shown rendered if their created. We don't want that Review page to look ugly with **Comments:** header with nothing. So we are rendering from a partial file in the views/reviews directory. Let's take a look at how we are iterating the data from that file. 

```
<div>
  <p><strong><%= comment.user.username %></strong><br>
  <%= comment.content %></p>
  <% if user_signed_in? && (current_user.wrote_this(comment) || current_user.admin) %>
  <%= link_to 'edit', edit_review_comment_path(@review, comment) %> 
  <%= link_to 'delete', comment_path(comment), method: :delete, data: { confirm: 'Are you sure?' } %>
  <% end %>
</div>
```
A last touch a gave is another statement. If the user is signed in and is the one who wrote the comment or an admin, he or she will have access to either edit it and delete it. A good friend of mine showed me how to do create that method in the User model and I'll pay it forward by showing it to you. 

```
def wrote_this(obj)
    if obj.class == Review && obj.user_id == self.id 
      true
    elsif obj.class == Comment && obj.user_id == self.id 
      true
    else
      false
    end
  end
```
Pretty neat, huh? Finally, we'll do the most important thing when creating the nested resource. The one thing that made that resource....nested. Let's go to the routes file and add the following.

```
resources :reviews do
    resources :comments
  end
```
You can even modify it by adding ```only: [:show, :new, :create, :edit, :update, :destroy]``` however you like or your project require to function as expected. 

As you can see, there's a lot of steps. However, the result will be very rewarding and is going to be an awesome experience to get it done. Remember to plan ahead your models and the way you want them to interact. Code line by code line, you'll finally be able to beat the boss. There's no guarantee the princess will be in that castle though.

![](https://i.gifer.com/774U.gif)
