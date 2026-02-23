## 1️. What is the difference between getElementById, getElementsByClassName, and querySelector / querySelectorAll?

---

**Answer:**

`getElementById()`, `getElementsByClassName()`, `querySelector()`, and `querySelectorAll()` are JavaScript methods used to select HTML elements from the DOM.

### getElementById()

The `getElementById()` method selects a single element using a specific id and returns only one element. It is very fast because an id is usually unique within a webpage.

### getElementsByClassName()

The `getElementsByClassName()` method selects all elements that share a specific class name and returns them as an **HTMLCollection**, which is a **live collection**. This means if the DOM changes, the collection updates automatically.

### querySelector()

The `querySelector()` method uses CSS selectors to select the **first matching element**. It is more flexible because it allows you to use id, class, tag, attribute, and other CSS selector patterns.

### querySelectorAll()

The `querySelectorAll()` method also uses CSS selectors but returns **all matching elements** as a **NodeList**. Unlike HTMLCollection, this NodeList is **static**, meaning it does not automatically update if the DOM changes later.

---

### Summary

- Use `getElementById()` to select a single element by id.
- Use `getElementsByClassName()` to select multiple elements by class.
- Use `querySelector()` or `querySelectorAll()` for flexible CSS-based selection.

---

## 2️. How to Create and Insert a New Element into the DOM

**Answer:**

Creating and inserting elements into the DOM dynamically allows you to update a webpage without reloading it. JavaScript provides methods to create elements, set their content or attributes, and insert them at a specific location in the DOM.

---

### Step 1: Create a New Element

Use `document.createElement()` to create an element in memory:

```javascript
const newDiv = document.createElement('div');
```

### Step 2: Add Content

Add text or HTML content to the element:

```javascript
newDiv.textContent = 'This is a dynamic div';
newDiv.innerHTML = '<strong>Hello!</strong> I am dynamic';
```

### Step 3: Add Attributes or Classes

Set an id, class, or custom attributes:

```javascript
newDiv.id = 'dynamicDiv';
newDiv.className = 'highlighted';
newDiv.setAttribute('data-info', 'dynamic element');
```

### Step 4: Select a Parent Element

Choose the container where the element will be inserted:
const container = document.getElementById('container');

### Step 5: Insert the Element

Insert the element into the DOM:

```javascript
container.appendChild(newDiv); // Add to the end
container.prepend(newDiv); // Add to the beginning
container.insertBefore(newDiv, container.firstChild); // Insert before a specific child
```

### Step 6: Add Event Listeners (Optional)

Make the new element interactive:

```javascript
newDiv.addEventListener('click', () => {
    alert('Dynamic div clicked!');
});
```

### Step 7: Full Example

const container = document.getElementById('container');

```javascript
const newDiv = document.createElement('div');
newDiv.textContent = 'I am dynamic!';
newDiv.className = 'highlighted';
newDiv.setAttribute('data-info', 'dynamic element');

container.appendChild(newDiv);

newDiv.addEventListener('click', () => {
    alert('Dynamic div clicked!');
});
```

---

### Summary

- Elements exist in memory until added to the DOM.
- Use appropriate insertion methods to control placement.
- Always select a valid parent container.
- Dynamic elements can have interactivity using event listeners.
- Any HTML element can be created dynamically: div, span, button, li, etc.

---

## 3. What is Event Bubbling? And how does it work?

---

**Answer:**

`Event Bubbling` is a JavaScript event propagation mechanism where an event starts from the target element and then propagates upward through its parent elements in the DOM hierarchy.

When an event (like `click`) occurs on an element, it does not stop there. Instead, it moves upward to its parent, then to the parent’s parent, and continues until it reaches the `document` object.

`How Event Bubbling Works`

### When a user clicks on an element:

- The event is triggered on the **target element**.
- The event then propagates to its **parent element**.
- It continues propagating upward through ancestor elements.
- Finally, it reaches the root (`document`).

---

**Example**

`HTML`

```javascript
<div id="parent">
    <button id="child">Click Me</button>
</div>
```

`JavaScript`

```javascript
document.getElementById('parent').addEventListener('click', function () {
    console.log('Parent clicked');
});

document.getElementById('child').addEventListener('click', function () {
    console.log('Button clicked');
});
```

`Output (When Button is Clicked)`

```javascript
Button clicked
Parent clicked
```

**Explanation**

- The event first triggers on the button.
- Then it bubbles up to the parent div.

### Summary

- Events start at the target element.
- They propagate upward through parent elements.
- Bubbling can be stopped using stopPropagation().
- It is useful for event delegation and efficient event handling.

---

## 4. What is Event Delegation in JavaScript? Why is it useful?

---

**Answer:**
`Event Delegation` is a technique in JavaScript where instead of attaching event listeners to multiple child elements, you attach a single event listener to their parent element and handle events using `event bubbling`.

Because events bubble up through the DOM, the parent element can detect and handle events triggered by its child elements.

_How Event Delegation Works_

- Attach an event listener to a `parent element`.
- When a child element is clicked (or triggered), the event bubbles up to the parent.
- Inside the event handler, use `event.target` to identify which child element triggered the event.

**Example**

`HTML`

```javascript
<ul id="itemList">
    <li>Item 1</li>
    <li>Item 2</li>
    <li>Item 3</li>
</ul>
```

`JavaScript (With Event Delegation)`

```javascript
document.getElementById('itemList').addEventListener('click', function (event) {
    if (event.target.tagName === 'LI') {
        console.log('Clicked:', event.target.textContent);
    }
});
```

**Why Event Delegation is Useful**

- Improves Performance:
  _Instead of adding event listeners to many child elements, you use only one listener on the parent._
- Handles Dynamic Elements:
  _If new child elements are added later using JavaScript, they automatically work without adding new event listeners._
- Cleaner and Maintainable Code:
  _Less repetitive code and easier event management._

**Summary**

- Event Delegation uses event bubbling.
- A single parent event listener handles child events.
- It improves performance.
- It works with dynamically added elements.
- It keeps code clean and scalable.

---

## 5. What is the difference between preventDefault() and stopPropagation() methods?

---

**Answer:**
Both preventDefault() and stopPropagation() are event methods in JavaScript, but they serve different purposes.

`preventDefault()`

### What It Does

`preventDefault()` stops the default behavior of an element.

### Example of Default Behaviors

- Clicking a link (<a>) → Navigates to another page
- Submitting a form → Reloads the page
- Right-click → Opens context menu

`Example`

_HTML_

```javascript
<a href="https://example.com" id="myLink">
    Visit
</a>
```

_Java Script_

```javascript
document.getElementById('myLink').addEventListener('click', function (event) {
    event.preventDefault();
    console.log('Link click prevented');
});
```

`Result`

- The link will not navigate to the URL.
- The default action is blocked.

---

`stopPropagation()`

### What It Does

`stopPropagation()` stops the event from `bubbling up (or capturing down)` the DOM tree.
It prevents the event from reaching parent elements.

`Example`

_HTML_

```javascript
<div id="parent">
    <button id="child">Click Me</button>
</div>
```

_Java Script_

```javascript
document.getElementById('parent').addEventListener('click', function () {
    console.log('Parent clicked');
});

document.getElementById('child').addEventListener('click', function (event) {
    event.stopPropagation();
    console.log('Button clicked');
});
```

_Result (When Button is Clicked)_

```javascript
Button clicked
```

- The parent event will NOT execute.
- The event does not bubble upward.

### Summary

- preventDefault() → Stops browser's default action.
- stopPropagation() → Stops event movement through the DOM.
- They solve different problems but are often used together.

---
