---
layout: post
title:      "Album Geeks - The Fetching Experiment From a Vinyl Lover"
date:       2021-03-23 00:12:28 +0000
permalink:  album_geeks_-_the_fetching_experiment_from_a_vinyl_lover
---


As my second attempt on passing the Javascript project, I decided to go for something fairly simpler than the previous incomplete project. That would be a virtual record store. 

Contrary to the previous project, I went for a limited amount of categories. That would be just vinyl, CD and cassettes. Just like browsing your local hip record store by format. The form on ```index.html``` looks like this:

```
<div id="form-container">
        <h3>Add Album</h3>
        <form id="new-album">
            <label>Title:</label>
            <input type="text" id="name">
            <label>Artist:</label>
            <input type="text" id="artist">
            <label>Genre:</label>
            <input type='text' id='genre'><br><br>
            <label>Description:</label>
            <input type="text" id="description" size="50"><br><br>
            <label>Category:</label>
            <select name="category" id="category_id">
                <option value="1">vinyl</option>
                <option value="2">CD</option>
                <option value="3">Cassette</option>
            </select>
            <label>Condition:</label>
            <select name="condition" id="condition">
                <option value="sealed">Sealed</option>
                <option value="mint">Mint (M)</option>
                <option value="near-mint">Near Mint (NM)</option>
                <option value="excellent">Excellent (E)</option>
                <option value="very-good-plus">Very Good + (VG+)</option>
                <option value="very-good">Very Good (VG)</option>
                <option value="good">Good (G)</option>
                <option value="fair">Fair (F)</option>
                <option value="poor">Poor (P)</option>          
            </select>
            <label>Price:</label>
            <input type='number' id='price'><br><br>
            <input type="submit" value="Submit">
        </form>
    </div><br>
```

Notice that the `category_id` dropdown is not some fancy complicated Javascript code, that would be binded in this function:

```
function bindAlbumFormEventListener() {
    albumForm.addEventListener("submit", function(e) {
        e.preventDefault()
        const name = document.getElementById("name").value
        const artist = document.getElementById("artist").value
        const genre = document.getElementById("genre").value
        const category_id = document.getElementById("category_id").value
        const condition = document.getElementById("condition").value
        const description = document.getElementById("description").value
        const price = document.getElementById("price").value;
        const data = {
            name,
            artist,
            genre,
            category_id,
            condition,
            description,
            price,
        };
        submitAlbum(data)
    })
```

Do the event listener, declare each constant as getting their value and submit that data. Sounds simple, specially for a coding veteran, right? Well, let's do the challenging part. That would be fetching the data. Javascript is not easy and though I feel comfortable with the idea of manipulating the DOM. The `fetch` can be as hard as deciding which special edition colored vinyl of your favorite band's new album will you choose. 

![](https://images.creativemarket.com/0.1.0/ps/8289919/600/400/m1/fpnw/wm0/presentation06-.jpg?1588974460&s=c88c008098e05ba2745013785b31ab4c)

First, let's go ahead and submit those albums for sale. Let's fetch the 'POST' request:

```
function submitAlbum(data) {
    fetch(BASE_URL+"/albums", {
        method: "POST",
        headers: {
            Accept: "application/json",
            "Content-Type": "application/json"
        },
        body: JSON.stringify({ album: data }),
    })
    .then((res) => res.json())
    .then((album) => {
        const newAlbum = new Album(album)
        mainListEl.innerHTML += newAlbum.renderAlbumsIndex()
       init()
    }) 
}
```

Once we submit the album, it will be rendered as required by the `renderAlbumsIndex()` method in `Album.js`. 

```
renderAlbumsIndex() {
        return `
            <div>
                <a  href="#"><h3 data-id=${this.id} class="text-sm font-medium hover:text-gray-400 album-link">${this.name}<br>
                by ${this.artist}</h3></a><button data-id=${this.id} type="button" class="delete-btn hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow">X</button>
            </div>
        `
    } 
```

Of course, we have our 'GET' request. Leaving that 'GET' request behind would be like covering the rest of the album racks in a physical brick and mortar store. This is how the 'GET' request looks like:

```
const getAlbums = () => {
    mainListEl.innerHTML = "<strong>Loading the albums...</strong>";
    fetch(BASE_URL+"/albums")
    .then((res) => res.json())
    .then((data) => {
        mainListEl.innerHTML = "";
        mainListTitleEl.innerHTML = "<h2>Albums</h2>";
        data.forEach(albumObject => {
            const newAlbum = new Album(albumObject)
            mainListEl.innerHTML += newAlbum.renderAlbumsIndex()
        })
        document
            .querySelectorAll(".album-link")
            .forEach((link) => link.addEventListener("click", showAlbumDetails));
        document 
            .querySelectorAll(".delete-btn")
            .forEach((btn) => btn.addEventListener("click", deleteAlbum))
    })
}
```

And finally, we wanna sell those albums. So deleting them in order to be sold is totally necessary. And if we noticed the last few lines, we're actually have the event listener for the delete buttons. So let's finalize with the fetch 'DELETE' request. 

```
function deleteAlbum(e) {
    const { id } = e.target.dataset
    fetch(`http://localhost:3000/albums/${id}`, {
        method: "DELETE"
    })
    .then((res) => res.json())
    .then((data) => {
        e.target.parentElement.remove();
    });
```

So there we have it, the complete project with a rails API and three fetch requests. There's more to do here in order to be on the same league as websites like Discogs. But with at least we learned how to work on those challenging fetch requests and dominating the DOM with Javascript.

Now if you excuse me, I'm gonna buy some vinyl records...

![](https://www.telegraph.co.uk/content/dam/music/2019/08/01/cassette-xlarge_trans_NvBQzQNjv4BqxajMzEiAhrDH1suGRf0qzGaysGF-4QcW-oeMs3CBZrE.jpg)

...and also some cassettes. 

