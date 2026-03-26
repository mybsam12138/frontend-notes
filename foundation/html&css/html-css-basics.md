# HTML & CSS Basics

## 1. What HTML and CSS are

- **HTML (HyperText Markup Language)** defines the **structure** of a webpage.
- **CSS (Cascading Style Sheets)** defines the **presentation** of that webpage.

A simple way to remember it:

- HTML = **what is on the page**
- CSS = **how it looks**

Example:

```html
<h1>Hello</h1>
<p>This is a paragraph.</p>
<button>Click me</button>
```

```css
h1 {
  color: blue;
}

button {
  background: black;
  color: white;
}
```

---

## 2. Basic HTML structure

A standard HTML page usually looks like this:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>My Page</title>
</head>
<body>
  <h1>Hello World</h1>
</body>
</html>
```

### Important parts

- `<!DOCTYPE html>`: tells the browser this is an HTML5 document
- `<html>`: root element of the page
- `<head>`: metadata, title, css links, charset, viewport
- `<body>`: visible page content

---

## 3. Common HTML tags

### Text tags

```html
<h1>Main Title</h1>
<h2>Subtitle</h2>
<p>This is a paragraph.</p>
<span>Inline text</span>
<strong>Important text</strong>
<em>Emphasized text</em>
```

- `h1` ~ `h6`: headings
- `p`: paragraph
- `span`: generic inline container
- `strong`: strong importance
- `em`: emphasis

### Link and image

```html
<a href="https://example.com">Visit Example</a>
<img src="photo.jpg" alt="A photo" />
```

- `a`: hyperlink
- `img`: image
- `alt`: alternative text for accessibility and fallback

### List

```html
<ul>
  <li>Apple</li>
  <li>Banana</li>
</ul>

<ol>
  <li>Step one</li>
  <li>Step two</li>
</ol>
```

- `ul`: unordered list
- `ol`: ordered list
- `li`: list item

### Layout-related tags

```html
<div>Block container</div>
<header>Page header</header>
<nav>Navigation area</nav>
<main>Main content</main>
<section>A section</section>
<article>Independent content</article>
<aside>Side content</aside>
<footer>Page footer</footer>
```

- `div`: generic block container
- semantic tags like `header`, `main`, `section` help readability, SEO, and accessibility

### Form tags

```html
<form>
  <label for="username">Username</label>
  <input id="username" type="text" />
  <button type="submit">Submit</button>
</form>
```

Common form elements:

- `form`
- `label`
- `input`
- `textarea`
- `select`
- `option`
- `button`

---

## 4. HTML attributes

Attributes provide extra information to elements.

Example:

```html
<input type="text" placeholder="Enter your name" disabled />
```

Here:

- `type`
- `placeholder`
- `disabled`

are attributes.

Common attributes:

- `id`: unique identifier
- `class`: group/style hook
- `src`: resource path
- `href`: link address
- `alt`: image description
- `style`: inline style
- `title`: tooltip text
- `value`: default value
- `name`: form field name

---

## 5. Block elements vs inline elements

### Block elements

They usually start on a new line and take full width by default.

Examples:

- `div`
- `p`
- `h1`
- `section`
- `ul`

### Inline elements

They stay in the same line and only take needed width.

Examples:

- `span`
- `a`
- `strong`
- `em`

This matters a lot when doing layout and styling.

---

## 6. What CSS does

CSS controls:

- color
- size
- spacing
- border
- layout
- alignment
- responsive behavior
- animations and transitions

Example:

```css
p {
  color: #333;
  font-size: 16px;
  line-height: 1.6;
}
```

---

## 7. CSS syntax

Basic syntax:

```css
selector {
  property: value;
  property: value;
}
```

Example:

```css
h1 {
  color: red;
  font-size: 32px;
}
```

- `h1` is the selector
- `color` and `font-size` are properties
- `red` and `32px` are values

---

## 8. Ways to use CSS

### Inline CSS

```html
<p style="color: red;">Hello</p>
```

- quick
- not recommended for large projects

### Internal CSS

```html
<head>
  <style>
    p {
      color: blue;
    }
  </style>
</head>
```

### External CSS

```html
<head>
  <link rel="stylesheet" href="styles.css" />
</head>
```

This is the most common and recommended way.

---

## 9. Common CSS selectors

### Element selector

```css
p {
  color: green;
}
```

### Class selector

```css
.card {
  border: 1px solid #ddd;
}
```

Used with:

```html
<div class="card"></div>
```

### ID selector

```css
#header {
  background: black;
}
```

Used with:

```html
<div id="header"></div>
```

### Descendant selector

```css
.card p {
  color: gray;
}
```

This means: select all `p` inside `.card`

### Multiple selector

```css
h1, h2, h3 {
  font-weight: bold;
}
```

### Universal selector

```css
* {
  box-sizing: border-box;
}
```

---

## 10. Important CSS properties

### Text

```css
color: #222;
font-size: 16px;
font-weight: 700;
font-family: Arial, sans-serif;
line-height: 1.5;
text-align: center;
```

### Box model

```css
width: 200px;
height: 100px;
padding: 16px;
border: 1px solid #ccc;
margin: 20px;
```

### Background

```css
background: #f5f5f5;
background-color: lightblue;
background-image: url("bg.png");
```

### Border and radius

```css
border: 1px solid #ddd;
border-radius: 8px;
```

### Display

```css
display: block;
display: inline;
display: inline-block;
display: none;
```

---

## 11. The CSS box model

Every element can be thought of as a box:

- **content**: actual text/image/content
- **padding**: space inside the border
- **border**: edge line around the box
- **margin**: space outside the border

Example:

```css
.box {
  width: 200px;
  padding: 20px;
  border: 5px solid black;
  margin: 10px;
}
```

Actual rendered width is usually:

- content width
- plus left/right padding
- plus left/right border
- margin affects outer spacing

A common setting is:

```css
* {
  box-sizing: border-box;
}
```

This makes width and height calculations easier.

---

## 12. Normal document flow

By default, HTML elements are laid out in normal flow:

- block elements go top to bottom
- inline elements go left to right within a line

Before learning Flexbox and Grid, this default flow is the base model.

---

## 13. Basic layout concepts in CSS

### `display`

Controls how an element behaves.

```css
display: block;
display: inline;
display: inline-block;
display: flex;
display: grid;
```

### `position`

```css
position: static;
position: relative;
position: absolute;
position: fixed;
position: sticky;
```

Very basic meaning:

- `static`: default
- `relative`: moves relative to original position
- `absolute`: positioned relative to nearest positioned ancestor
- `fixed`: fixed relative to viewport
- `sticky`: behaves like relative until scroll threshold

### `overflow`

```css
overflow: hidden;
overflow: auto;
overflow: scroll;
```

Controls what happens when content exceeds the box.

---

## 14. Flexbox basics

Flexbox is widely used for 1-dimensional layout.

Example:

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 16px;
}
```

Common properties:

### On container

- `display: flex`
- `flex-direction`
- `justify-content`
- `align-items`
- `gap`
- `flex-wrap`

### On item

- `flex`
- `align-self`

Example:

```html
<div class="container">
  <div>1</div>
  <div>2</div>
  <div>3</div>
</div>
```

---

## 15. Grid basics

CSS Grid is powerful for 2-dimensional layout.

Example:

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 16px;
}
```

Useful when you need rows and columns together.

---

## 16. Units in CSS

Common units:

- `px`: pixels
- `%`: percentage
- `em`: relative to parent font size
- `rem`: relative to root font size
- `vw`: viewport width
- `vh`: viewport height

Example:

```css
font-size: 1rem;
width: 50%;
height: 100vh;
```

---

## 17. Colors in CSS

Ways to define color:

```css
color: red;
color: #ff0000;
color: rgb(255, 0, 0);
color: rgba(255, 0, 0, 0.5);
```

Common in real projects:

- hex
- rgb/rgba
- sometimes hsl

---

## 18. CSS specificity

When multiple CSS rules target the same element, the browser decides which one wins.

General priority:

1. inline style
2. id selector
3. class / attribute / pseudo-class
4. element selector

Example:

```css
p {
  color: blue;
}

.text {
  color: green;
}

#main-text {
  color: red;
}
```

If one element matches all three, `#main-text` usually wins.

Also:

- later rules can override earlier rules when specificity is the same
- `!important` forces priority, but should be used carefully

---

## 19. Inheritance

Some CSS properties inherit from parent elements, some do not.

Often inherited:

- `color`
- `font-family`
- `font-size`

Often not inherited:

- `margin`
- `padding`
- `border`
- `width`

Example:

```css
body {
  color: #333;
  font-family: Arial, sans-serif;
}
```

Children often inherit these text styles automatically.

---

## 20. Responsive basics

Responsive design means the page adapts to different screen sizes.

### Viewport meta

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

This is essential on mobile.

### Media query

```css
@media (max-width: 768px) {
  .container {
    flex-direction: column;
  }
}
```

This means when screen width is 768px or below, apply different styles.

---

## 21. Semantic HTML

Semantic HTML means using tags that describe meaning, not just appearance.

Good examples:

- `header`
- `nav`
- `main`
- `section`
- `article`
- `footer`
- `button`

Instead of using too many generic `div`s.

Benefits:

- better structure
- easier maintenance
- better accessibility
- better SEO

---

## 22. Accessibility basics

A few important basics:

- use semantic HTML where possible
- images should have meaningful `alt`
- form inputs should have `label`
- buttons should use `<button>` instead of clickable `div`
- keep text readable and contrast clear

Example:

```html
<label for="email">Email</label>
<input id="email" type="email" />
```

---

## 23. Typical relationship between HTML, CSS, and JavaScript

In a frontend app:

- HTML builds the structure
- CSS styles the structure
- JavaScript adds behavior and interactivity

Example:

- HTML creates a button
- CSS makes it look nice
- JavaScript handles click event

---

## 24. A small full example

### HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Simple Card</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <div class="card">
    <h1>Hello</h1>
    <p>This is a simple card example.</p>
    <button>Read More</button>
  </div>
</body>
</html>
```

### CSS

```css
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f4f4f4;
}

.card {
  width: 300px;
  margin: 40px auto;
  padding: 20px;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.card h1 {
  margin-top: 0;
}

.card button {
  padding: 10px 16px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
}
```

---

## 25. What you should understand first

When learning HTML/CSS, focus on these basics first:

1. HTML structure and common tags
2. class vs id
3. block vs inline
4. CSS selectors
5. box model
6. normal flow
7. Flexbox
8. responsive basics
9. semantic HTML
10. accessibility basics

If these are solid, later topics like animation, advanced layout, component libraries, and framework styling become much easier.

---

## 26. Common beginner misunderstandings

### 1) HTML is not a programming language
It is a markup language for structure.

### 2) CSS is not only “beautifying”
It also controls layout, spacing, responsiveness, and visual hierarchy.

### 3) `div` is not enough for everything
Semantic tags matter.

### 4) Width issues are often box model issues
Padding, border, and box sizing matter.

### 5) Alignment is often easier with Flexbox
Instead of using strange margin hacks everywhere.

---

## 27. One-line summary

- **HTML defines structure**
- **CSS defines style and layout**
- Together they form the foundation of frontend development

---

## 28. Suggested next topics

After HTML/CSS basics, a good next path is:

1. JavaScript basics
2. DOM and BOM
3. Event loop
4. Flexbox and Grid in depth
5. Responsive design in practice
6. Browser rendering process
7. Framework basics (Vue / React)

---

## 29. Memory hooks

You can remember them like this:

- HTML = skeleton
- CSS = skin + clothes
- JavaScript = behavior + interaction

Or:

- HTML says **what it is**
- CSS says **how it looks**
- JavaScript says **what it does**
