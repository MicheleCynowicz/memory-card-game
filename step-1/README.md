# Getting Started
In your new, empty project, create the following files:
`index.html`
`style.css`

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

Now make an empty div inside the `<body>` tag for the game board. Give your div a class of `game-board`.

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

Preview your game in a browser. There isn't much to it yet, but you should at least see a small "game board" on the screen. If it's there, you can move on to Step 2.