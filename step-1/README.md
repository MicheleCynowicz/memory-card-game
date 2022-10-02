# Step 1: Prepare the game board
In your new, empty project, create the following files:

In your `index.html` file, add some boilerplate code:
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Memory Card Game</title>
    <link rel="stylesheet" href="./style.css" />
  </head>
  <body></body>
</html>
```

Now add some markup within the `<body>` tag to create an area to stage a set of _cards_:
```html
<div class="game-board">
  <ul class="cards">

  </ul>
</div>
```

Now lets add some CSS to your `style.css` file:
```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background: #6563FF;
}

.game-board {
  padding: 25px;
  border-radius: 10px;
  background: #F8F8F8;
  box-shadow: 0 10px 30px rgba(0,0,0,0.1);
}
```

Preview your game in a browser. There isn't much to it yet, but you should at least see a small "game board" on the screen.

Next add the following block of 16 `li` tags inside of the `<ul>` tag in your `index.html` file:
```html
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-1.png" alt="card-img">
  </div>
</li>
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-1.png" alt="card-img">
  </div>
</li>
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-2.png" alt="card-img">
  </div>
</li>
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-2.png" alt="card-img">
  </div>
</li>
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-3.png" alt="card-img">
  </div>
</li>
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-3.png" alt="card-img">
  </div>
</li>
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-4.png" alt="card-img">
  </div>
</li>
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-4.png" alt="card-img">
  </div>
</li>
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-5.png" alt="card-img">
  </div>
</li>
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-5.png" alt="card-img">
  </div>
</li>
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-6.png" alt="card-img">
  </div>
</li>
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-6.png" alt="card-img">
  </div>
</li>
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-7.png" alt="card-img">
  </div>
</li>
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-7.png" alt="card-img">
  </div>
</li>
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-8.png" alt="card-img">
  </div>
</li>
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-8.png" alt="card-img">
  </div>
</li>
```

Notice that in the code you've just added the `li` tags carry a class of `card`. Each `<li>` tag will visually represent a card in the game.

Now add some CSS to make them look like game cards. In your `style.css` file, add this CSS for the _cards_:
```css
.cards,
.card,
.view {
  display: flex;
  align-items: center;
  justify-content: center;
}

.cards {
  height: 400px;
  width: 400px;
  flex-wrap: wrap;
  justify-content: space-between;
}

.cards .card {
  cursor: pointer;
  list-style: none;
  user-select: none;
  position: relative;
  perspective: 1000px;
  transform-style: preserve-3d;
  height: calc(100% / 4 - 10px);
  width: calc(100% / 4 - 10px);
}

.card .view {
  width: 100%;
  height: 100%;
  position: absolute;
  border-radius: 7px;
  background: #fff;
  pointer-events: none;
  backface-visibility: hidden;
  box-shadow: 0 3px 10px rgba(0,0,0,0.1);
  transition: transform 0.25s linear;
}

.card .front-view img {
  width: 19px;
}

.card .back-view img {
  max-width: 45px;
}
```
Preview your `index.html` file. You should see a game board with what appears to be 16 cards, with 8 matching image pairs.

If it's there, you can move on to [Step 2](/step-2).