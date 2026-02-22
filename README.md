## 1️ What is the difference between getElementById, getElementsByClassName, and querySelector / querySelectorAll?

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
