# Step 2: Complete game board markup
In your root directory, create a `script.js` file.

In the `<head>` of your `index.html` file, reference that file.
```html
<script src="./script.js" defer></script>
```
Note that the `<script>` tag above has the `defer` attribute. We are asking our script tag to defer running any scripts until the whole HTML file has rendered.

Within the `game-board` div, add a `ul` for the whole set of _cards_. Each _card_ will be represented by an `<li>` tag, which contains some nested HTML.
```html
<ul class="cards">
  <li class="card">
    <div class="view front-view">
      <img src="images/que_icon.svg" alt="icon">
    </div>
    <div class="view back-view">
      <img src="images/img-1.png" alt="card-img">
    </div>
  </li>
</ul>
```
Note here that there are two divs - a `front-view` and a `back-view`. The `front-view` div contains an `img` tag that's noted as an `icon` and the `back-view` div contains an `img` tag that's noted as `card-img`. In this game, the `back-view` is going to be the image to match, which will be revealed when a card is flipped over. The `fron-view` will be a question mark icon.

# Images
Create an `images` directory in your project root, and add these images:
- [img-1.png](/step-2/images/img-1.png)
- [img-2.png](/step-2/images/img-2.png)
- [img-3.png](/step-2/images/img-3.png)
- [img-4.png](/step-2/images/img-4.png)
- [img-5.png](/step-2/images/img-5.png)
- [img-6.png](/step-2/images/img-6.png)
- [img-7.png](/step-2/images/img-7.png)
- [img-8.png](/step-2/images/img-8.png)
- [que_icon.svg](/step-2/images/que_icon.svg)

Note that there are 8 images, and one icon. Our game board should have 16 cards, of 8 matching pairs.

In your `index.html` file, create 15 more `li` tags like this:
```html
<li class="card">
  <div class="view front-view">
    <img src="images/que_icon.svg" alt="icon">
  </div>
  <div class="view back-view">
    <img src="images/img-1.png" alt="card-img">
  </div>
</li>
```

Once you have all 16 `<li class="card">...</li>` blocks setup, go through the `back-view` image tags and change the `src` values to be `images/img-1.png`, `images/img-2.png`, `images/img-3.png`, `images/img-4.png`, `images/img-5.png`, `images/img-6.png`, `images/img-7.png`, and `images/img-8.png`. Repeat each image number a second time, so that you have a pair of each image in the `back-view` divs in your code.

In your `style.css` file, add this CSS for the _cards_:
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

Preview your game - you should see your game board with 16 cards, and 8 matching image pairs. Onward to [Step 3](/step-3)!