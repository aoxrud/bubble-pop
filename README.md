# Bubble Pop Game
A simple game written only in HTML and CSS, without Javascript.

### Browser support
It only works with Chrome because it supports the `::before` pseudo element on the `<input type='checkbox' />` element.

### Try it out
[Codepen example](https://codepen.io/aoxrud/pen/gQbNGY) or run it locally via the [dist/index.html](dist/index.html) page.

### Why?
I was inspired by [The Mine: No JS, CSS only adventure game](https://codepen.io/jcoulterdesign/pen/NOMeEb) and decided to give it a try using the same checkboxes technique but with a simpler game. A game that any young toddler would enjoy.

### How does the bubble popping work?
Each bubble is a checkbox element `<input type='checkbox' />` that has a pseudo-element `::before` styled as a bubble which sits in the forefront of the checkbox.
When a bubble is clicked, the checkbox behind the scene is checked.
We use `.checkbox:checked` CSS selector to detect when a bubble is clicked and hide the checkbox entirely.

### How does the "game complete" work?
In order to know when all bubbles have been popped, the code looks for all the checkboxes to be `:checked`.
The caveat is that the code needs to know exactly how many bubbles there are and for the elements to be laid out in a specific way so that we can use css to select it.

The code has a few `.checkbox`es followed by a `.complete`

```
input.checkbox(type='checkbox')
input.checkbox(type='checkbox')
.complete Game Complete
```

If we wanted to select the `.complete` element once all the checkboxes are checked, our css selector looks something like this:
`.checkbox:nth-child(1):checked + .checkbox:nth-child(2):checked + .complete`


### Development notes
Even though this could be written in vanilla html and css, it has a lot of repeated code which would be a nightmare to manually maintain and debug.
I've opted to use preprocessors like [pug](https://pugjs.org) and [sass](https://sass-lang.com/) to help with that.
The benefits of these preprocessors is that they offer things like loops and variables which keep the code concise and easily maintainable.

### Why is there a `package.json` if the game doesn't have javascript?
The `package.json` file is there to help with the preprocessing of css and html.
It will take care of watching for changes in the `src/` files and compiling them to plain css/html files in the `dist/` directory.

- Run `npm install` to install pug, sass, and watch tools.
- Run `npm run build` to build the `src/` into the `dist/`.
- Run `npm run watch` to run a watcher that will compile the source files in `src/` into `dist/` any time the source files change.