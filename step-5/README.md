# Step 5: User experience (UX)
Let's fix up some of the smaller interactions in our game.

First, let's add a `setTimeout` function inside of our `matchCards` function, so that our user has a chance to see the second card revealed, before deciding that it doesn't match. Wrap the last 5 lines of code in the `matchCards` function in a `setTimeout` function:
```js
  // these cards didn't match so we'll un-flip them, but let the user see them both before they disappear
  setTimeout(() => {
    cardOne.classList.remove("flip");
    cardTwo.classList.remove("flip");
    cardOne = cardTwo = ""; // reset the cardOne & cardTwo variables to empty string
    return disableDeck = false;
  }, 1200);
```

Did you notice that while the two cards are being evaluated, you cannot flip a third card? That's because of the `disableDeck` variable!

Now that you've been playing your game, it might feel a little bit laggy with the 1200ms `setTimeout` that we added. Let's give this some more pizazz by adding another animation.

Create a `shake` animation with CSS by putting this `@keyframes` block into your `style.css` file:
```css
@keyframes shake {
  0%, 100%{
    transform: translateX(0);
  }
  20%{
    transform: translateX(-13px);
  }
  40%{
    transform: translateX(13px);
  }
  60%{
    transform: translateX(-8px);
  }
  80%{
    transform: translateX(8px);
  }
}
```

Now let's reference the animation with a class selector for a card with a `.shake` class:
```css
.card.shake{
  animation: shake 0.35s ease-in-out;
}
```

In your `script.js` file, just above the `setTimeout` function you added in the previous step, add another `setTimeout` function to apply the `shake` class to the currently-viewable cards (which we already know do not match) and have it happen at `400` milliseconds:
```js
setTimeout(() => {
  cardOne.classList.add("shake");
  cardTwo.classList.add("shake");
}, 400);
```

Oh! We also need to remove the `shake` class when the non-matching cards are un-flipped. Add the string `"shake"` to the code where you remove the `"flip"` class from the `classList` of the two selected cards:
```js
cardOne.classList.remove("shake", "flip");
cardTwo.classList.remove("shake", "flip");
```

How does your game look on a small screen? Could this be played on a smartphone with a touchscreen? Probably not! Let's add some CSS to make the game a bit more responsive:
```css
@media screen and (max-width: 700px) {
  .cards {
    height: 350px;
    width: 350px;
  }

  .card .front-view img {
    width: 17px;
  }

  .card .back-view img {
    max-width: 40px;
  }
}

@media screen and (max-width: 530px) {
  .cards {
    height: 300px;
    width: 300px;
  }

  .card .front-view img {
    width: 15px;
  }

  .card .back-view img {
    max-width: 35px;
  }
}
```

Play your game in your browser until you've matched all 8 pairs of cards. You should see the `YOU WIN!` message in the console. YAY! You've won. What should happen next?

Commit this work to your repository, make a new branch, and build something that you would like to see happen when the game is won. Then add some other game features. Should this game show the player how many pairs they've matched as they play? Should there be a button to start or reset the game? Should you see a special message when you win? Should this game have a timer?

Use any suggestion from above, or get creative and come up with other feature ideas! 

# Final assignment:
Add at least 2 additional game features to the game using branches and pull requests. 
Share your work and get some feedback!