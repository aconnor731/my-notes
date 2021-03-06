# CSS Grids and Flexbox for Responsive Design

### Flexbox

- It is a hack for layouts!
- The first layout elements - but not designed to lay out whole web pages
- the very first layout we were given to work with layouts in CSS
- before that it was table and floats
- Features flex-containers (row) and flex-items (cells). Both are required to work.
- Flexbox has been around since 2009 and it has some issues.
- **Excels at <u>vertical centering</u> and <u>equal heights.</u>**
- Very easy to reorder boxes.
- Major disadvantages:
  - Wasn't designed to be locked down for layouts! Works in 1 dimension only.
  - Browser support and syntax is challenging.
- Think of flexbox as one continuous row.
  - great for apps like Pinterest where images are delivered continuously
- Games:
  - Flexbox Froggy: http://flexboxfroggy.com
  - Flexbox Defense: http://www.flexboxdefense.com

## CSS Grid

### Introducing CSS Grid

- there is no CSS Level 4...CSS the language no longer has levels.
  - https://www.w3.org/TR/css-2015/#css-levels

#### Why CSS Grid?

- Built into CSS specification (now a recommendation)
- all browsers support it
- adoption rates have taken off spectacularly
- No "row" markup required.
- Grid is designed to work in 2 dimensions.
- Use Flexbox for UI elements, but use Grid for major layout.

#### CSS Grid: Browser Compatibility

- full support in all the browsers you expect
- partial support on all of the Microsoft browsers
- No support for mostly mobile browsers
  - she says it does not matter if a mobile browser has CSS Grid or not since on mobile screens, items are stacked vertically

#### Polyfills & Fallbacks

#### Exploring CSS Grid Examples

Space between columns:

- just before column 1:

  ```css
  .col-1 {
      grid-column: 1 / 2;
  }
  ```



![css-grid-2](C:\Users\au3643\repos\my-notes\frontendmasters\CSS Grids and Flexbox for Responsive Web Design\images\css-grid-2.png)



#### Alternate Syntax

- Named grid template areas (header, footer, etc):
  https://gridbyexample.com/examples/#example11

#### Reordering

#### CSS Code Demo

Implicit Grid: when some grid values are provided but not complete, CSS grid implicitly helps by filling in



#### Chapter 11: CSS Grid Grid

```css
.wrapper {
    grid-gap: 2%;
    grid-template-rows: repeat(4, 1fr); /* 4 columns, 1 fraction */
    grid-template-columns: ;
}
```

`repeat(4, 1fr)`: after applying a `grid-gap: 2%`, whatever is left over, divide into 4 equal fractions.

#### Grid Properties Review

You can name your columns in `grid-template-columns/rows`:

- ```css
  grid-template-columns: [col1] 40px [col2] 3fr;
  grid-template-rows: 350px [name] 350px [name] 10%;
  ```

- `grid-gap`:

  - shorthand for `grid-column-gap` and `grid-row-gap`

- `grid-column: 1/3;` is also written as:

  - ```css
    grid-column-start: 1;
    grid-column-end: 3;
    ```

#### Introducing Grid Area

For an empty column:

```css
.wrapper {
    grid-template-areas:
    "sidebar ... header header"
    "sidebar ... article article";
}
```

- can be just one dot (`.`, I used three dots for my own preference)

#### Nesting CSS Grids

There is no reason to use **flexbox-grid** if we are using **CSS-grid**. Just use **CSS-grid**.

Remember there is a parent-child relationship in CSS-grid:

- the `container` is the parent
- direct descendants are `grid-items`

In class example:

```css
.nested {
    display: grid;
    grid-gap: 1em;
    grid-template-columns: auto;
}

@media (min-width: 650px) {
    ...
    
    .nested {
        grid-template-columns: repeat(3, 1fr);
    }
}
```

#### Exercise: Nested CSS Grids

![nested css grids](C:\Users\au3643\repos\my-notes\frontendmasters\CSS Grids and Flexbox for Responsive Web Design\images\nested-grid-exercise.png)

```css
.nested {
    display: grid;
    grid-gap: 1em;
    grid-template-columns: auto;
}

@media (min-width: 650px) {
    ...
    
    .nested {
		grid-template-columns: repeat(3, 1fr);
		grid-template-areas: 
		"aside1 ... aside3";
	}
	.nested aside:first-child {
		grid-area: aside1;
	}
	.nested aside:last-child {
		grid-area: aside3;
	}
}
```

#### Grid Fallbacks

https://rachelandrew.co.uk/css/cheatsheets/grid-fallbacks

If something is originally declared as a `float` item, and later it is declared as a `grid` item, it no longer is a `float`.

`grid` overrides other `display` declared properties.

```css
@supports (display: grid) {
    .grid > div {
        width: auto;
    }
}
```

- checks if browser supports `grid`
- put most modern/forward thinking code inside the `@supports` block and the old code outside of it.
- <u>This site has a lot of useful snippets to make your site more cross-browser oriented</u>

