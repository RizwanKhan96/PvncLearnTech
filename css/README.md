# CSS Architecture Documentation

## Overview

PVNCC Learning Technologies uses a **modular, scalable CSS architecture** split into three organized files:

```
css/
├── global.css      (Design tokens & base styles)
├── components.css  (Reusable components)
├── responsive.css  (Media queries & breakpoints)
└── README.md       (This file)
```

## File Structure

### 1. **global.css** - Design System Foundation
**Purpose:** Central place for all design tokens and base element styles

**Contains:**
- CSS custom properties (variables) for colors, typography, spacing, etc.
- Reset and base element styles (h1-h6, p, a, lists, forms, tables)
- Accessibility utilities (skip links, focus states, screen reader text)
- Font face declarations

**Examples:**
```css
:root {
    --color-primary: #003D7A;      /* Navy blue */
    --color-accent: #D4AF37;       /* Gold */
    --space-md: 1rem;              /* 16px */
    --font-size-lg: 1.125rem;      /* 18px */
}
```

**Key Variables:**
- Colors: `--color-primary`, `--color-accent`, `--color-success`, etc.
- Spacing: `--space-xs` through `--space-3xl`
- Typography: `--font-size-*`, `--font-weight-*`, `--line-height-*`
- Effects: `--shadow-*`, `--radius-*`, `--transition`

---

### 2. **components.css** - Reusable Components
**Purpose:** Component-specific styling for UI elements

**Contains:**
- Header and navigation styles
- Page headers
- Cards and grids
- Buttons and forms
- Alerts and badges
- Footer
- Resource cards (for library page)
- Search/filter toolbars

**Naming Convention:** BEM (Block Element Modifier)
```css
.card              /* Block - main component */
.card__title       /* Element - part of card */
.card:hover        /* State - interaction state */
.card--featured    /* Modifier - variant of card */
```

**Examples:**
```html
<article class="card">
  <h3 class="card__title">Title</h3>
  <p class="card__description">Description</p>
  <a href="#" class="card__link">View</a>
</article>
```

---

### 3. **responsive.css** - Responsive Design
**Purpose:** Mobile-first responsive breakpoints

**Breakpoints:**
```css
@media (max-width: 480px)    /* Small devices */
@media (min-width: 640px)    /* Tablets */
@media (min-width: 1024px)   /* Desktops */
@media (min-width: 1280px)   /* Wide screens */
```

**Also includes:**
- Print styles
- High contrast mode
- Reduced motion support

---

## HTML Usage

**All pages must link CSS files in this order:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Page Title</title>
    
    <!-- Link CSS files in this order -->
    <link rel="stylesheet" href="css/global.css">
    <link rel="stylesheet" href="css/components.css">
    <link rel="stylesheet" href="css/responsive.css">
</head>
<body>
    <!-- No inline styles! -->
</body>
</html>
```

**❌ NEVER do this:**
```html
<!-- BAD - inline styles -->
<div style="color: blue; padding: 20px;">
```

**✅ ALWAYS do this:**
```html
<!-- GOOD - use CSS classes -->
<div class="card">
```

---

## Design Tokens

### Colors

**Brand Colors:**
```css
--color-primary: #003D7A;         /* Navy blue */
--color-primary-dark: #002952;    /* Darker navy */
--color-primary-light: #1E5B99;   /* Lighter navy */
--color-accent: #D4AF37;          /* Gold */
--color-accent-dark: #B8942E;     /* Dark gold */
```

**Status Colors:**
```css
--color-success: #0F8A3D;         /* Green */
--color-warning: #F59E0B;         /* Amber */
--color-info: #0073B1;            /* Blue */
```

**Grayscale (50-900):**
```css
--color-gray-50: #F9FAFB;         /* Almost white */
--color-gray-900: #111827;        /* Almost black */
```

### Spacing Scale

```css
--space-xs: 0.25rem;    /* 4px   */
--space-sm: 0.5rem;     /* 8px   */
--space-md: 1rem;       /* 16px  */
--space-lg: 1.5rem;     /* 24px  */
--space-xl: 2rem;       /* 32px  */
--space-2xl: 3rem;      /* 48px  */
--space-3xl: 4rem;      /* 64px  */
```

### Typography

```css
--font-size-xs: 0.75rem;      /* 12px  */
--font-size-sm: 0.875rem;     /* 14px  */
--font-size-base: 1rem;       /* 16px  */
--font-size-lg: 1.125rem;     /* 18px  */
--font-size-xl: 1.25rem;      /* 20px  */
--font-size-2xl: 1.5rem;      /* 24px  */
--font-size-3xl: 1.875rem;    /* 30px  */
--font-size-4xl: 2.25rem;     /* 36px  */

--font-weight-normal: 400;
--font-weight-medium: 500;
--font-weight-semibold: 600;
--font-weight-bold: 700;
```

---

## Common Components

### Header
```html
<header class="header">
  <div class="header__top">...</div>
  <div class="header__main">
    <div class="header__content">
      <div class="header__branding">...</div>
      <nav class="nav">...</nav>
    </div>
  </div>
</header>
```

### Cards
```html
<article class="card">
  <div class="card__icon">📚</div>
  <h3 class="card__title">Title</h3>
  <p class="card__description">Description</p>
  <a href="#" class="card__link">View More →</a>
</article>
```

### Buttons
```html
<a href="#" class="btn btn--primary">Primary Button</a>
<a href="#" class="btn btn--secondary">Secondary Button</a>
```

### Alerts
```html
<div class="alert">
  <div class="alert__content">
    <div class="alert__icon">⚠️</div>
    <div class="alert__body">
      <h3 class="alert__title">Title</h3>
      <p class="alert__description">Description</p>
    </div>
  </div>
</div>
```

### Footer
```html
<footer class="footer">
  <div class="footer__container">
    <div class="footer__grid">...</div>
    <div class="footer__bottom">...</div>
  </div>
</footer>
```

---

## Best Practices

### ✅ DO

- Use CSS custom properties for all colors, spacing, and typography
- Use semantic HTML class names (`.card`, `.button`, not `.blue-box`)
- Follow BEM naming for clarity
- Add comments before sections
- Keep media queries in `responsive.css`
- Use flexbox and grid for layouts
- Test on multiple screen sizes

### ❌ DON'T

- Add inline styles (`style="color: blue"`)
- Use `!important` (except accessibility overrides)
- Hard-code colors (use CSS variables instead)
- Create component-specific CSS files
- Mix spacing units (use rem consistently)
- Forget mobile-first design
- Break BEM naming conventions

---

## Maintenance & Updates

### Updating the Design System

**To change brand colors:**
1. Edit `global.css` `:root` section
2. Change only the variable value
3. Changes cascade everywhere automatically

**Example:**
```css
/* Before */
--color-primary: #003D7A;

/* After */
--color-primary: #004A9B;  /* All navy blues update instantly */
```

### Adding New Components

1. Create the component in `components.css`
2. Use existing variables (colors, spacing, etc.)
3. Follow BEM naming
4. Document with HTML examples
5. Test at all breakpoints

### Files That Reference CSS

```
index.html          → links all 3 CSS files
resources.html      → links all 3 CSS files
calendar.html       → links all 3 CSS files
support.html        → links all 3 CSS files
about.html          → links all 3 CSS files
guides/            → All guide pages link same CSS
```

---

## Resources

- [CSS Custom Properties (MDN)](https://developer.mozilla.org/en-US/docs/Web/CSS/--*)
- [BEM Methodology](http://getbem.com/)
- [WCAG Accessibility Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- [Mobile-First Design](https://www.nngroup.com/articles/mobile-first-web-design/)

---

## Questions?

Contact: Learning Technologies Team  
Email: helpdesk@pvnccdsb.on.ca
