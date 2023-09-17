# Infinite-Scroll

This a simple web application in which when the user can have infinite scrolling, where images are displayed continuously as you scroll, ensuring that the images never run out.
The application is made with the help of the HTML,CSS ans JS concepts.

## Implementation of Project

The project is implemented with the help of the following steps which are mentioned below. This project can be easily implemented by anyone who are having prior basic knowledge about HTML,CSS and JS. The steps are:

### Step-1: HTML

A HTML file is created with the name index.html and the following code is added:

```

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Infinite Scroll</title>
    <link rel="stylesheet" href="style.css" />
  </head>

  <body>
    <h1>INFINITE SCROLL</h1>

    <div class="img-container" id="img-container"></div>
    <script defer src="index.js"></script>
  </body>
</html>

```

### Step-2: CSS

Then another file is created with the name style.css which holds the styling code for the application, the following code is added int the file:

```

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
 background-color: rgb(6, 255, 101);
}

h1 {
  text-align: center;
  margin-top: 25px;
  margin-bottom: 45px;
  font-size: 40px;
  letter-spacing: 1px;
 text-decoration: underline;
  color:rgb(240, 92, 7);
}

.img-container {
  margin: 10px 30%;
 
}

.img-container img {
  width: 100%;
  margin-top: 5px;
  border-radius: 20px;
  border-style: solid;
  border-color: rgb(252, 6, 100);
  
}


@media screen and (max-width: 600px) {
  h1 {
    font-size: 20px;
  }
  .img-container {
    margin: 10px;
  }
}

```

### Step-3: JS

In the final step the functionality of the web application is added with the help of JS in the file which is created with the name as index.js and the following code is added:

```

const imageContainer = document.getElementById("img-container");
const loader = document.getElementById("loader");

let photosArray = [];

let ready = false;
let imagesLoaded = 0;
let totalImages = 0;

const count = 10;
const apikey = "alG7OhSYiSVHWPUrodbTbJetFhdju6NI0NYc8_d2ZUk";
const apiUrl = `https://api.unsplash.com/photos/random/?client_id=${apikey}&count=${count}`;

function setAttribute(element, attributes) {
  for (const key in attributes) {
    element.setAttribute(key, attributes[key]);
  }
}

function imageLoaded() {
  imagesLoaded++;
  if (imagesLoaded === totalImages) {
    ready = true;
  }
}

function displayPhotos() {
  totalImages = photosArray.length;

  imagesLoaded = 0;

  photosArray.forEach((photo) => {
    const item = document.createElement("a");

    setAttribute(item, {
      href: photo.links.html,
      target: "_blank",
    });

    const img = document.createElement("img");
    setAttribute(img, {
      src: photo.urls.regular,
      alt: photo.alt_description,
      title: photo.alt_description,
    });

    img.addEventListener("load", imageLoaded);

    item.append(img);

    imageContainer.append(item);
  });
}

async function getPhotos() {
  try {
    const response = await fetch(apiUrl);
    photosArray = await response.json();
    displayPhotos();
  } catch (error) {
    console.log(error);
  }
}

window.addEventListener("scroll", () => {
  if (
    window.scrollY + window.innerHeight >= document.body.offsetHeight &&
    ready
  ) {
    ready = false;
    getPhotos();
  }
});

getPhotos();

```


**Hosted Link**: https://suk-18.github.io/Infinite-Scroll.github.io/
