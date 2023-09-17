## Movie Search 

This is a simple movie search web that allows users to search for movies by name. The app is built using HTML, CSS, and JavaScript.


## Step 1

Create a new file called `index.html` in your project folder with this content:
```

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Movie Search</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <div id="container">
        <span>MovieSearch</span>
      <input
        type="text"
        id="movieSearch"
        placeholder="Search here..."
      />
      <button id="search">Search</button>
    </div>
    <div id="root"></div>
    <script src="script.js"></script>
  </body>
</html>

```

## Step 2

### In the same directory create another file named `style.css` which will contain all of our CSS code for styling purposes. Add these styles to it

```

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  #container {
    background-color: #4285f4;
    padding: 15px;
    margin-top: 40px;
    text-align: center;
  }
  span{
    font-size: 45px;
    color: #ff6633;
    font-weight: bolder;
    margin-right: 35%;
  }
  ::placeholder{
    color:rgb(182, 177, 177);
    font-weight: 100;
  }
  #movieSearch {
    padding: 15px 50px;
    border-radius: 10px;
    border: 1px solid black;
    font-size: 20px;
    font-weight: 300;
  }
  #search {
    background-color: #f57f26;
    color: white;
    padding: 15px 20px;
    border-radius: 10px;
    border: 1px solid antiquewhite;
    font-weight: 600;
    font-size: 20px;
  }
  #root {
    margin-top: 30px;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 15px;
    align-items: center;
    justify-content: center;
  }
  #rootDiv {
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
  }
  
  img {
    border-radius: 10px;
  }
  h3 {
    text-transform: uppercase;
    font-weight: 900;
    font-size: 20px;
  }
  #YearDiv {
    font-size: 30px;
    font-weight: 900;
  }
```

## Step 3

### Create a new file in the components folder called script.js and add this code to it:

```
const movie = document.getElementById("movieSearch");
const btn = document.getElementById("search");
const root = document.getElementById("root");
async function getMovie() {
  root.innerText = "";
  let movieName = movie.value;
  try {
    let response = await fetch(
      `https://www.omdbapi.com/?&apikey=bce5f182&s=${movieName}`
    );
    let data = await response.json();
    console.log(data);
    const movieList = data.Search;
    console.log(movieList);

    movieList.forEach((movie) => {
      console.log(movie);
      getMovies(movie);
    });

    function getMovies(movie) {
      const newDiv = document.createElement("div");
      newDiv.id = "rootDiv";
      newDiv.innerHTML = `
      <div id ="imgDiv"><img src = ${movie.Poster}</div>
      <h3 id ="titleDiv">${movie.Title} </h3></br>
      <p id ="YearDiv">${movie.Year}</p>
      `;
      root.appendChild(newDiv);
    }
    movie.value = "";
  } catch (error) {
    console.log(error, "error");
  }
}

btn.addEventListener("click", getMovie);

```


