# Event Delegation in JavaScript – Explained with an Example

**Event Delegation is a pattern based upon the concept of Event Bubbling. It is an event-handling pattern that allows you to handle events at a higher level in the DOM tree other than the level where the event was first received.**

## A Brief Intro to Event Propagation

By default, events triggered on an element propagate up the DOM tree to the element's parent, its ancestors, and on up until the root element (`html`).

Look at this example:

```html
<div>
  <span>
    <button>Click Me!</button>
  </span>
</div>
```

Here we have a `div` which is a parent of a `span` which in turn is a parent of the `button` element.

Due to event bubbling, when the button receives an event, say click, that event bubbles up the tree, so `span` and `div` will respectively receive the event also.

## How Does Event Delegation Work?

With event delegation, instead of handling the click event on the `button`, you can handle it on the `div`.

The idea is that you "**delegate**" the handling of an event to a different element (in this case, the div, which is a parent element) instead of the actual element (the button) that received the event.

Here's what I mean by that in code:

```javascript
const div = document.getElementsByTagName("div")[0]

div.addEventListener("click", (event) => {
  if(event.target.tagName === 'BUTTON') {
    console.log("button was clicked")
  }
})
```

The `event` object has a `target` property which contains information about the element that actually received the event. On `target.tagName`, we get the name of the tag for the element, and we check if it's **BUTTON**.

With this code, when you click the `button`, the event bubbles up to the `div` which handles the event.

## Benefits of Event Delegation

Event Delegation is a useful pattern that allows you to write cleaner code, and create fewer event listeners with similar logic.

What do I mean by this? Look at this code:

```html
<div>
  <button>Button 1</button>
  <button>Button 2</button>
  <button>Button 3</button>
</div>
```

Here we have 3 buttons. Let's say we wanted to handle a click event on each button, such that when it is clicked, the button's text is logged to the console. We can implement that like this:

```javascript
const buttons = document.querySelectorAll('button')

buttons.forEach(button => {
  button.addEventListener("click", (event) => {
    console.log(event.target.innerText)
  })
})
```

I'm using `querySelectorAll` here as it returns a `NodeList` which I can use the `forEach` method for. `getElementsByTagName` returns an `HTMLCollection` which doesn't have the `forEach` method.

When you click on the first button, you have "Button 1" logged on the console. For the second button, "Button 2" is logged, and for the third button, "Button 3" is logged.

Although this works as we want, we have created three event listeners for the three buttons.

Since the click event on these buttons propagates upward in the DOM tree, we can use a common parent or ancestor that they have to handle the event. In this case, we delegate a common parent that they share to handle the logic we want.

Here's how:

```javascript
const div = document.querySelector('div')

div.addEventListener("click", (event) => {
  if(event.target.tagName === 'BUTTON') {
    console.log(event.target.innerText)
  }
})
```

Now, we have just one event listener, but the same logic: when you click the first button, "Button 1" is logged to the console, and the same thing for the other buttons.

Even if we add an extra button like this:

```html
<div>
  <button>Button 1</button>
  <button>Button 2</button>
  <button>Button 3</button>
  <button>Button 4</button>
</div>
```

We won't have to change the JavaScript code as this new button also shares the `div` parent (which we delegated for the event handling) with the other buttons.

## Wrapping Up

With event delegation, you create fewer event listeners and perform similar events-based logic in one place. This makes it easier for you to add and remove elements without having to add new or remove existing event listeners.

Event delegation is possible because of event propagation in the DOM, where the event a child element receives is also passed to the child's parent and ancestors.

Thank you for reading, and happy coding!

Article archoved from: [https://www.freecodecamp.org/news/event-delegation-javascript/](https://www.freecodecamp.org/news/event-delegation-javascript/)
