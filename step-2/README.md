# Step 2: Setup script file
When a player wants to begin a a memory game, the cards need to be "shuffled" so that they show up in a random order. We will accomplish this with JavaScript.

In the `<head>` of your `index.html` file, reference the `script.js` file.
```html
<script src="./script.js" defer></script>
```
Note that the `<script>` tag above has the `defer` attribute. We are asking our script tag to defer running any scripts until the whole HTML file has rendered.

At the top of your `script.js` file, setup some global variables:
```js
const cards = document.querySelectorAll(".card");
let matchedPairs = 0;
let cardOne, cardTwo;
let disableDeck = false;
```
With this code in place, `cards` is a constant that will be an `Array` of `li` tags in the DOM.

The other variables are defined with the `let` keyword. Their values will be changed as the program steps through different functions.

Let's start with a function that won't do much right away, we'll call this one `flipCard`.
Add this `flipCard` function under your global variables.
```js
function flipCard() {
  console.log('flipCard was executed');
}
```

After the `flipCard` function, add a function to shuffle the cards (what fun would this game be if the cards were always in the same position?):
```js
function shuffleCards() {

}
```
Since we'll be making value changes to the global variables (mentioned above) as the game is played, when we DO want to replay the game, we'll want to shuffle the cards and begin again. Start building this `shuffleCards` function with some lines of code that reset the global variables to their original state:
```js
  matchedPairs = 0; // reset matchedPairs variable to 0
  disableDeck = false; // reset disableDeck boolean to false
  cardOne = cardTwo = ""; // reset cardOne and cardTwo variables to empty string
```
Now what about the cards? We already have a `const cards` array that represents each of the `li` tags in the DOM, but we don't need to move the positions of our HTML elements, instead we can use an array of numbers to help shuffle our cards.

On the next line create an array of the numbers 1 through 8, with a duplicate set of those:
```js
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 1, 2, 3, 4, 5, 6, 7, 8]; // create an array of the image numbers, 1-8, twice
```
Now we'll "shuffle" this array using the JS Array method `.sort()`:
```js
arr.sort(() => Math.random() > 0.5 ? 1 : -1); // randomly sort the array
```
There's no need to re-assign the `arr` variable here, the `.sort()` method does that for us.

Now we have an array of `cards` and an array of corresponding numbers that have been randomly sorted (shuffled), so we can use a `.foreach()` loop to combine them:
```js
cards.forEach((card, i) => { // loop over the set of cards. For each `card`...
  card.classList.remove("flip"); // remove the 'flip' class
  let imgTag = card.querySelector(".back-view img"); // find the back-view image tag by querying all the childNodes of the current card element for the '.back-view img' CSS selector
  imgTag.src = `images/img-${arr[i]}.png`; // set the value of the src attribute on the current imgTag to a numbered filename based on our randomized array
  card.addEventListener("click", flipCard); // add a click event listener to the current card to execute a function `flipCard` when clicked
});
```

The whole `shuffleCards` function definition should now look like this:
```js
function shuffleCards() {
  matchedPairs = 0; // reset matchedPairs variable to 0
  disableDeck = false; // reset disableDeck boolean to false
  cardOne = cardTwo = ""; // reset cardOne and cardTwo variables to empty string
  let arr = [1, 2, 3, 4, 5, 6, 7, 8, 1, 2, 3, 4, 5, 6, 7, 8]; // create an array of the image numbers, 1-8, twice
  arr.sort(() => Math.random() > 0.5 ? 1 : -1); // randomly sort the array
  
  cards.forEach((card, i) => { // loop over the set of cards. For each card...
      card.classList.remove("flip"); // remove the 'flip' class
      let imgTag = card.querySelector(".back-view img"); // find the back-view image tag by querying all the childNodes of the current card element for the '.back-view img' CSS selector
      imgTag.src = `images/img-${arr[i]}.png`; // set the value of the src attribute on the current imgTag to a numbered filename based on our randomized array
      card.addEventListener("click", flipCard); // add a click event listener to the current card to execute a function `flipCard` when clicked
  });
}
```

At the end of the `style.js` file, execute the `shuffleCards()` function:
```js
shuffleCards();
```

Test the game in your browser with the devTools JavaScript console open. Whenever you refresh the page, the card images should shuffle. When you click on a card you should see your `console.log` message from the `flipCard` function.

In [Step 3](/step-3), we'll build-out the `flipCard` function.