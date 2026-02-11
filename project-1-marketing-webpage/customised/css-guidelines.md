# CSS GUIDELINES 

### NOTES ON STRUCTURE
1. top to bottom flow - organise in order elements appear on the page
2. specifity increases downward - general styles at top
3. group related styles - keep componet styles together
4. use comments effectively - section headers to naviage

## 1. IMPORTS AND FONTS 

## 2. CSS VARIABLES (custom properties) 
 e.g., 

:root {
    -- primary-color: #333
    -- spacing-unit: 8px;
}


Custom properties (sometimes referred to as CSS variables or cascading variables) are entities defined by CSS authors that represent specific values to be reused throughout a document. They are set using the @property at-rule or by custom property syntax (e.g., --primary-color: blue;). Custom properties are accessed using the CSS var() function (e.g., color: var(--primary-color);).

Complex websites have very large amounts of CSS, and this often results in a lot of repeated CSS values. For example, it's common to see the same color used in hundreds of different places in stylesheets. Changing a color that's been duplicated in many places requires a search and replace across all rules and CSS files. Custom properties allow a value to be defined in one place, then referenced in multiple other places so that it's easier to work with. Another benefit is readability and semantics. For example, --main-text-color is easier to understand than the hexadecimal color #00ff00, especially if the color is used in different contexts.

Custom properties defined using two dashes (--) are subject to the cascade and inherit their value from their parent. The @property at-rule allows more control over the custom property and lets you specify whether it inherits its value from a parent, what the initial value is, and the type constraints that should apply.

Note: Variables do not work inside media queries and container queries. You can use the var() function in any part of a value in any property on an element. You cannot use var() for property names, selectors, or anything aside from property values, which means you can't use it in a media query or container query.

The selector given to the ruleset (<section> elements in the example above) defines the scope in which the custom property can be used. For this reason, a common practice is to define custom properties on the :root pseudo-class, so that it can be referenced globally:

[mdn](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Cascading_variables/Using_custom_properties)

Using the @property at-rule
The @property at-rule allows you to be more expressive with the definition of a custom property with the ability to associate a type with the property, set default values, and control inheritance. The following example creates a custom property called --logo-color which expects a <color>:

css

Copy
@property --logo-color {
  syntax: "<color>";
  inherits: false;
  initial-value: #c0ffee;
}
If you want to define or work with custom properties in JavaScript instead of directly in CSS, there is a corresponding API for this purpose. You can read about how this works in the CSS Properties and Values API page.

Referencing custom properties with var()
Regardless of which method you choose to define a custom property, you use them by referencing the property in a var() function in place of a standard property value:

css

Copy
details {
  background-color: var(--main-bg-color);
}



## 3. RESET/NORMALISE

## 4. BASE STYLES 
e.g., html, body, h1, p, a

## 5. LAYOUT 
e.g., container, grid, flex-wrapper

## 6. COMPONENTS (in order page appearance) 
e.g., .header, nav, hero, card, footer

## 7. UTILITIES 
e.g., text-center, hidden, sc-only

## 8. MEDIA QUERIES

---

### NAMING CONVENTIONS

## BEM (BLOCK, ELEMENT, MODIFIER)
- BLOCK e.g., card
    - a standalone component
    - doesn't depend on where it's used and makes sense alone
    - e.g., background, border, spacing, base typography 
- ELEMENT e.g., card_title
    - child of block 
    - part of the block
    - has no meaning outside the block, depends on it
    - never style it as if it's reusable anywhere
- MODIFIER e.g., card--featured, card--dark (double hyphen implies modification, same component and structure, different appearance or state)
    - variation
    - changes appearance or behaviour
    - never exists alone
    - do not redefine structure or add new elements
    - only tweak values (colour, size, emphasis)

## USE SEMANTIC NAMES, NOT PRESENTATIONAL
    - e.g., .hero, .cta, .testimonial vs red-box, left-column, big-text
    - think of it as a role rather than an outfit

--

### COMMON CLASS NAME PATTERNS

## Layout
.container, .wrapper, .grid, .flex-container

## Navigation 
.nav, .menu, .navbar, .sidebar

## Content sections
.hero, .header, .footer, .main, .section

## Components
.card, .button, .form, .modal, .dropdown

## States
.is-active, .is-hidden, .is-loading

## Utilities
.text-center, .mt-2, .hidden

--

### COMMENT SECTIONS

/* ===================================
   MAJOR SECTION
   =================================== */

/* Subsection
   --------------------------- */

/* Single line comment for properties */

--

### WHEN TO COMMENT?

- Section breaks
- Complex calculations
- Browser hacks
- Non-obvious decisions
- Magic numbers

### RECOMMENDED PROPERTY ORDER 

.example {
  /* 1. POSITIONING */
  position: absolute;
  top: 0;
  left: 0;
  z-index: 10;
  
  /* 2. DISPLAY & BOX MODEL */
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 200px;
  margin: 10px;
  padding: 20px;
  
  /* 3. BORDERS */
  border: 1px solid black;
  border-radius: 5px;
  
  /* 4. BACKGROUND */
  background-color: white;
  background-image: url('...');
  
  /* 5. TYPOGRAPHY */
  font-family: Arial;
  font-size: 16px;
  line-height: 1.5;
  color: black;
  text-align: center;
  
  /* 6. VISUAL EFFECTS */
  opacity: 0.9;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  
  /* 7. ANIMATIONS */
  transition: all 0.3s ease;
  transform: translateX(10px);
}

### Common File Splitting Patterns

#### Pattern 1: By Function

```
styles/
├── main.css          (imports all others)
├── reset.css         (normalize/reset)
├── variables.css     (custom properties)
├── typography.css    (fonts, headings, text)
├── layout.css        (grid, containers, positioning)
├── components.css    (buttons, cards, forms)
└── utilities.css     (helper classes)
```

#### Pattern 2: By Page Section

```
styles/
├── main.css
├── header.css
├── hero.css
├── about.css
├── contact.css
└── footer.css
```

#### Pattern 3: By Component (for large apps)

```
components/
├── button/
│   ├── button.html
│   ├── button.css
│   └── button.js
├── card/
│   ├── card.html
│   ├── card.css
│   └── card.js
```

### 