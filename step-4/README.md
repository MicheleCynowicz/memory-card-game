# Step 4: Click events and flipped cards
When it comes to JavaScript and listening for user events, we can write functions with an already-expected parameter, the `event` parameter, which expects an argument that is an `Object` carrying specific event properties with values taken from the event input.

For example: when I am browsing the web on my laptop, I sometimes click a button on the screen that has text that reads "Checkout". When I click this button, a `click` event will call a function (callback function) to run.

That callback function, being called upon by a `click` event, knows to expect to recieve an `Object` full of data about what I clicked on - which includes the HTML element that was clicked, such as `<button id="checkout">` or `button#checkout`. 

In the case of our game cards, let's see what type of data is given to the callback function when clicking on a "card" on the screen. In your `flipCard` function, add a paramter `evt`. We _can_ call this anything; `event`, `evt`, `e`, `click`, etc are typical parameter names you might see in other people's code, often named this way to indicate that an event object is expected. Once you have the parameter name in place, log it to the console from within the function:
```js
function flipCard(evt) {
  console.log('flipCard was executed');
  console.log(evt);
}
```

Test this in your browser by reloading your game and clicking on different cards. Look at the console output and you will see all the data that is being passed from the click event to the `flipCard(evt)` function each time. There's a lot of data to look at there, but for our game to work the function only needs to know which card element was clicked.

Assign the event's _target_ to a variable `clickedCard` (you can remove the console logs or comment them out):
```js
function flipCard(evt) {
  // console.log('flipCard was executed');
  // console.log(evt);
  const clickedCard = evt.target;
}
```
In your console logs from earlier, you might have seen the event object formatted like this: `click: { target: li.card }`. That meant you clicked on an `<li>` element with a class of `card` - but wait! ALL of the `<li>` tags are `<li class="card">`! No worries, the event that is being passed is not just giving us the HTML, it is representing the exact DOM element that was clicked - the individal _card_ on the screen. The `evt.target` is representing the entire HTML element. That's the `li` tag that was clicked AND all of its `childNodes`.

Before we go further into our `flipCard` function, let's use some CSS to make sure that all the `back-view` cards are hidden from the player's view - we want to only show the question mark icon in the event that a given card was clicked. To do this, add the following to your `style.css` file:
```css
.card .back-view {
  transform: rotateY(-180deg);
}
```

Now when you test the game in the browser, all the cards should give the appearance of being "face-down".

Next we want to have some CSS to support the card's "flipped" state. We will use javaScript to add and remove a `flip` class to the clicked card element. Add this CSS to your `style.css` file so that something visual will happen to a card element when it has the `flip` class applied:
```css
.card.flip .back-view {
  transform: rotateY(0);
}
.card.flip .front-view {
  transform: rotateY(180deg);
}
```

Go back to the `script.js` file, and add this conditional statement after the `clickedCard` variable is assigned:
```js
if (cardOne !== clickedCard && !disableDeck) { // make sure that the current variable cardOne is not the same value as the clickedCard, AND that the deck is NOT disabled

  }
```

What is happening in this condition?
We want to be able to compare two cards, but we need to assign values to the `cardOne` and `cardTwo` global variables. At the time that we compare the variables, we don't want the user to be able to click a _third_ card.

When we start the game, the variable `disableDeck` is set to `false`. We will want to stop the `flipCard` function from doing anything if there are already two cards flipped. So when two cards are available we will change the `disableDeck` variable to `true`.

We are using the NOT operator `!` to see that the set of cards of is NOT yet disabled. If the deck is not yet disabled, and the variable is still `false` then `!disableDeck` will evaluate to `true`.

We also begin the game with a `cardOne` variable that is defined, but has no value. So when we first click a card in our game, `cardOne` should be _falsy_.

This condition will check for two things. First, we want to be sure that the card that was clicked is not ALREADY a flipped card, so we use the comparison operation `cardOne !== clickedCard`. Then we also want to ensure that our functions are not currently comparing two cards, so we want to be sure that `!disableDeck` evaluates to `true`. This way both conditions are met and the rest of our `flipCard` function will run.

Inside of our condition, we will first add the `flip` class to the `clickedCard` DOM element:
```js
clickedCard.classList.add("flip"); // add the 'flip' class to the classes currently assigned to the clickedCard
```
Test this in your browser - you should be able to flip each card!

Now that we know we can _flip_ these cards over, let's start assigning variables so that the `flipCard` function will only allow the user to flip two cards at a time.

After the `clickedCard.classList.add("flip");` line in the condition, add this code:
```js
if(!cardOne) { // if there is not yet a value assigned to the cardOne variable...
    return cardOne = clickedCard; // set the cardOne value as the clickedCard and end this function.
}
// everything below will execute if the condition above was not met (if cardOne already had a value when flipCard() was called)
cardTwo = clickedCard; // set the cardTwo value as the clickedCard
disableDeck = true; // set this to true for the next time this flipCard function is called, when the top level condition is evaluated
```

Test the game now, and you should only be able to _flip_ two cards.

In [Step 5](/step-5) we will evaluate if the two flipped cards match.
