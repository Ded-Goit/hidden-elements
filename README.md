# hidden-elements

## Step 1: Basic visibility checks

### Step 1: Check the display property

You can check if an element is hidden by using its display property.

```JavaScript
function isElementHiddenByDisplay(element) {
return window.getComputedStyle(element).display === 'none';
}
```

### Step 2: Check the visibility property

You can check if an element is hidden by using its visibility property.

```JavaScript
function isElementHiddenByVisibility(element) {
return window.getComputedStyle(element).visibility === 'hidden';
}
```

### Step 3: Use window.getComputedStyle() for precise checking

Using window.getComputedStyle() provides the most precise visibility check because it takes inherited styles into account.

```JavaScript
function isElementHiddenByComputedStyle(element) {
const style = window.getComputedStyle(element);
return style.display === 'none' || style.visibility === 'hidden';
}
```

## Step 2: Advanced visibility checks

#### Substep 1: Check offsetWidth and offsetHeight

These properties help determine whether the element is rendered with the size.

```JavaScript
function isElementRendered(element) {
return element.offsetWidth > 0 && element.offsetHeight > 0;
}
```

#### Substep 2: Check getBoundingClientRect()

This method checks whether the element is in the viewport.

```JavaScript
function isElementInViewport(element) {
const rect = element.getBoundingClientRect();
return (
rect.top >= 0 &&
rect.left >= 0 &&
rect.bottom <= (window.innerHeight || document.documentElement.clientHeight) &&
rect.right <= (window.innerWidth || document.documentElement.clientWidth)
);
}
```

## Step 3: Check the hidden property

The hidden attribute in HTML5 can directly indicate whether an element is hidden.

```JavaScript
function isElementHiddenAttribute(element) {
return element.hidden;
}
```

# Now let's combine these methods into a complex function:

```JavaScript
function isElementHidden(element) {
const style = window.getComputedStyle(element);

// Check display property
if (style.display === 'none') return true;

// Check visibility property
if (style.visibility === 'hidden') return true;

// Check offsetWidth and offsetHeight
if (element.offsetWidth === 0 && element.offsetHeight === 0) return true;

// Check hidden attribute
if (element.hidden) return true;

// Check if element is within the viewport
const rect = element.getBoundingClientRect();

if (
rect.top < 0 ||
rect.left < 0 ||
rect.bottom > (window.innerHeight || document.documentElement.clientHeight) ||
rect.right > (window.innerWidth || document.documentElement.clientWidth)
) return true;

return false;
}
```

What to do next
If some methods are not cross-browser compatible, consider using polyfills or libraries such as [jQuery](https://jquery.com/) for wider compatibility.
Always test your code across browsers to ensure consistent behavior.
