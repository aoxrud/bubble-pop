# Bubble Pop Game
A simple game written only in HTML and CSS, without Javascript.

![](game-preview
.gif)


### Try it out
[Codepen example](https://codepen.io/aoxrud/pen/gQbNGY) or run it locally via the [dist/index.html](dist/index.html) page.

### Why?
I was inspired by [The Mine: No JS, CSS only adventure game](https://codepen.io/jcoulterdesign/pen/NOMeEb) and decided to give it a try using the same checkboxes technique, but with a simpler game. A game that any young toddler would enjoy.

### How does the bubble popping work?
The code takes advantage of the default browser behavior that focuses on the input once the linked label is clicked.
Each bubble is a `<label>` element linked to a checkbox element `<input type='checkbox' />`.
When a bubble is clicked, the linked checkbox is checked.
We use `.checkbox:checked` CSS selector to detect when a bubble is clicked and hide the bubble complete.

### How does the "game complete" work?
In order to know when all bubbles have been popped, the code looks for all the checkboxes to be `:checked`.
The caveat is that the code needs to know exactly how many bubbles there are and for the elements to be laid out in a specific way so that we can use CSS's general sibling selector `~` to detect the states.

The code has a few `.checkbox`es followed by a `.complete`

If we wanted to select the `.complete` element once all the checkboxes are checked, our css selector looks something like this:
`#checkbox-1:checked + #checkbox-2:checked + .complete`

### How does the bubble pop at the clicked location?
The elements are laid out in such a way that each is responsible for a single task.
The `checkbox` is tied to the `label` and only responsible for tracking the popped state.
The `label` is the one that get animated from bottom to the top using `translateY` and it has a child element `.bubble` that is the actual bubble.
Once the checkbox is checked, we trigger the `pop` animation on the `.bubble` element.


The alternative would be to combine the floating and popping animations on the same element. However, it turns out to be problematic because both animations operate using the `transform` property. The problem is that when the `transform` property is set, it resets the existing transformation. In our case, it would cause clicked bubbles to reset to the starting position before popping.

### Why did you use preprocessors?
Even though this could be written in vanilla html and css, it has a lot of repeated code which would be a nightmare to manually maintain and debug.
I've opted to use preprocessors like [pug](https://pugjs.org) and [sass](https://sass-lang.com/) to help with that.
The benefits of these preprocessors is that they offer things like loops and variables which keep the code concise and easily maintainable.

### Why is there a `package.json` if the game doesn't have javascript?
The `package.json` file is there to help with the preprocessing of css and html. There is no javascript used to run the game.

It will take care of watching for changes in the `src/` files and compiling them to plain css/html files in the `dist/` directory.

- Run `npm install` to install pug, sass, and watch tools.
- Run `npm run build` to build the `src/` into the `dist/`.
- Run `npm run watch` to run a watcher that will compile the source files in `src/` into `dist/` any time the source files change.