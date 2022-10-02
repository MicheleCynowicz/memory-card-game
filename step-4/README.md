# Step 4: Compare cards and count pairs
In the last step we setup the `flipCard` function and the global variables `cardOne`, `cardTwo`, and `disableDeck` in such a way that our player can only _flip_ two cards on the game board. Next we will create a `matchCards` function in `script.js` to evaluate the contents of our two cards to decide if they are a match.

In `script.js` create this new function:
```js
function matchCards(img1, img2) {

}
```

Since our `li.card` elements are all the same with the exception of the `src` attibute value (the actual image filename), we will want to compare the two card element's `back-view` image files. The `cardOne` and `cardTwo` DOM elements are assigned within the `flipCard` function, so go back to the `flipCard` function, and add this code after the line `disableDeck = true;`:
```js
// if the function has come this far, it means we have set values for both cardOne and cardTwo.
// each of the cardOne and cardTwo variables currently represent a whole HTML element with childNodes
let cardOneImg = cardOne.querySelector(".back-view img").src; // query the elements inside cardOne to get the value of the img src, such as `images/img-2.png`, and set that as the value of cardOneImg
let cardTwoImg = cardTwo.querySelector(".back-view img").src; // query the elements inside cardOne to get the value of the img src, such as `images/img-2.png`, and set that as the value of cardTwoImg
matchCards(cardOneImg, cardTwoImg); // now check the images by filename to see if they are a match!
```

Now we have a place inside of the `flipCard` function where the `matchCards` function is called, and we are passing two arguments: `cardOneImg` and `cardTwoImg` for the function to compare.

In the `matchCards` function, create a condition using the `===` comparative operator:
```js
if (img1 === img2) { // this code will run if the card images match

}
```

Yay! You've matched a pair of cards. In order to win the game, the player must match all 8 pairs of cards. Once a pair has been matched, you will need to increment the number of `matchedPairs`. Add this increment operation inside the condition:
```js
matchedPairs++; // if the card images match, we can imcrement the global `matchedPairs` variable by 1 match
```

If the number of `matchedPairs` gets to `8`, then the game is won! Below the `matchedPairs++` line, add a condition and a response to decide if the game has been won:
```js
if (matchedPairs == 8) { // if your number of matches is 8, you've made all the matches! Game Won!
  console.log('YOU WIN!');
  return; // for now, lets call this game over, end this function and do nothing else.
}
// everything below will execute if the game has not yet been won...
```

What if the game is still going, after a set of two cards are a match?
First, we will want the matched cards to stay visible, and in a state where they cannot be _un-flipped_. On the next line in the `matchCards` function, add this code to remove the click event listeners from the `cardOne` and `cardTwo` elements:
```js
cardOne.removeEventListener("click", flipCard); // remove the eventlistener so that this matched card cannot be flipped anymore
cardTwo.removeEventListener("click", flipCard); // remove the eventlistener so that this matched card cannot be flipped anymore
```

Finally, while still in the `matchCards` function, reset the `cardOne`, `cardTwo`, and `disableDeck` variables to their original values from the start of the game, and end the function:
```js
cardOne = cardTwo = ""; // now reset the cardOne & cardTwo variables to empty strings, so we can use them again
disableDeck = false;
return;  // end function
```

Now we have code to handle what will happen to our game cards if the two selected cards match each other. What if they don't match?

We end the `matchCards` function with the `return;` statement inside of the condition `if (img1 === img2) {}` but this means that the function only ends here if the two cards match! Add this code to the `matchCards` function, after the closing bracket of the `if (img1 === img2) {}` condition:
```js
// these cards didn't match, un-flip them...
  cardOne.classList.remove("flip");
  cardTwo.classList.remove("flip");
  cardOne = cardTwo = ""; // reset the cardOne & cardTwo variables to empty string
  disableDeck = false;
  return;
```

Your `flipCard` and `matchCards` functions should now read like this:
```js
function flipCard(evt) { // take an event object's as a scoped variable
  const clickedCard = evt.target; // set the event's target DOM element as a variable
  if (cardOne !== clickedCard && !disableDeck) { // make sure that the current variable cardOne is not the same value as the clickedCard, AND that the deck is NOT disabled
      clickedCard.classList.add("flip"); // add the 'flip' class to the classes currently assigned to the clickedCard
      if(!cardOne) { // if there is not yet a value assigned to the cardOne variable...
          return cardOne = clickedCard; // set the cardOne value as the clickedCard and end this function.
      }
      // everything below will execute if the condition above was not met (if cardOne already had a value when flipCard() was called)
      cardTwo = clickedCard; // set the cardTwo value as the clickedCard
      disableDeck = true; // set this to true for the next time this flipCard function is called, when the top level condition is evaluated
      // if the function has come this far, it means we have set values for both cardOne and cardTwo.
      // each of the cardOne and cardTwo variables currently represent a whole HTML element with childNodes
      let cardOneImg = cardOne.querySelector(".back-view img").src; // query the elements inside cardOne to get the value of the img src, such as `img-2.png`, and set that as the value of cardOneImg
      let cardTwoImg = cardTwo.querySelector(".back-view img").src; // query the elements inside cardOne to get the value of the img src, such as `img-2.png`, and set that as the value of cardTwoImg
      matchCards(cardOneImg, cardTwoImg); // now check the images by filename to see if they are a match!
  }
}

function matchCards(img1, img2) {
  if (img1 === img2) { // this code will run if the card images match
    matchedPairs++; // if the card images match, we can imcrement the global `matchedPairs` variable by 1 match
    if (matchedPairs == 8) { // if your number of matches is 8, you've made all the matches! Game Won!
        console.log('YOU WIN!');
        return; // for now, lets call this game over, end this function and do nothing else.
    }
    // everything below will execute if the game has not yet been won...
    cardOne.removeEventListener("click", flipCard); // remove the eventlistener so that this matched card cannot be flipped anymore
    cardTwo.removeEventListener("click", flipCard); // remove the eventlistener so that this matched card cannot be flipped anymore
    cardOne = cardTwo = ""; // now reset the cardOne & cardTwo variables to empty strings, so we can use them again
    disableDeck = false;
    return; // end function
  }
  // these cards didn't match, un-flip them...
  cardOne.classList.remove("flip");
  cardTwo.classList.remove("flip");
  cardOne = cardTwo = ""; // reset the cardOne & cardTwo variables to empty string
  disableDeck = false;
  return; 
}
```

Test this in your browser! The first card you click will flip over, displaying the hidden image underneath. When you click the next card, it seems like nothing happened, and the first card is flipped back to its front-view. BUT something DID happen. If you keep playing the game until you find a matching pair, the matched pair stays matched.

JavaScript is FAST. In this case, it's faster than the CSS animation to flip the second card! When you clicked a second card that was not a match, the comparison happened SO FAST in JavaScript that the `flip` class is added AND removed faster than the CSS could respond!

That's not fair gameplay is it? You never get to view the second card you clicked UNLESS it was a matched image :-(

We'll fix this in [Step 5](/step-5).


