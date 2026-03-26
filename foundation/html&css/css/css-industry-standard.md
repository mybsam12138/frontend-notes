# CSS Industry Standards (Web Application & Mobile H5)

## 1. Core Principles

- Consistency > Fancy
- Readability first
- Use spacing system
- Use design tokens (colors, font, spacing)
- Mobile-first design

---

## 2. Typography (Font Standards)

### Web Application

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  font-size: 14px;
  line-height: 1.6;
  color: #333;
}
```

### Mobile H5

```css
body {
  font-family: -apple-system, BlinkMacSystemFont, "Helvetica Neue", Arial, sans-serif;
  font-size: 16px;
  line-height: 1.5;
}
```

### Guidelines

- Desktop: 14px–16px
- Mobile: ≥16px (avoid zoom)
- Title: 18px–24px
- Use `line-height: 1.5~1.8`

---

## 3. Spacing System (VERY IMPORTANT)

Use consistent spacing scale:

```css
:root {
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;
}
```

Usage:

```css
.card {
  padding: var(--space-md);
  margin-bottom: var(--space-lg);
}
```

---

## 4. Color System

```css
:root {
  --color-primary: #1976d2;
  --color-success: #4caf50;
  --color-warning: #ff9800;
  --color-danger: #f44336;

  --text-primary: #222;
  --text-secondary: #666;
  --border-color: #e0e0e0;
  --background: #f5f5f5;
}
```

Guidelines:

- Use limited palette (5–8 colors)
- Maintain contrast (accessibility)
- Avoid pure black (#000)

---

## 5. Layout Standards

### Container

```css
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 16px;
}
```

### Flex Layout (common)

```css
.flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

### Grid Layout

```css
.grid-3 {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 16px;
}
```

---

## 6. Button Style

```css
.button {
  padding: 8px 16px;
  border-radius: 6px;
  border: none;
  cursor: pointer;
  font-size: 14px;
}

.button-primary {
  background: var(--color-primary);
  color: white;
}
```

---

## 7. Input Style

```css
.input {
  padding: 8px 12px;
  border: 1px solid var(--border-color);
  border-radius: 4px;
  font-size: 14px;
}
```

---

## 8. Border & Radius

```css
border: 1px solid #eee;
border-radius: 6px;
```

Guidelines:

- Small UI: 4px
- Card/UI: 6–12px

---

## 9. Shadow (Elevation)

```css
box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
```

Guidelines:

- Use lightly
- Avoid heavy shadow

---

## 10. Responsive Design

### Mobile-first

```css
.container {
  padding: 8px;
}

@media (min-width: 768px) {
  .container {
    padding: 16px;
  }
}
```

---

## 11. Image & Media

```css
img {
  max-width: 100%;
  height: auto;
}
```

---

## 12. Reset / Normalize

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

---

## 13. Accessibility

- Use readable font size
- Ensure contrast
- Use semantic HTML
- Provide hover & focus states

---

## 14. Mobile H5 Special Tips

- Use `rem` or `vw` for scaling
- Avoid fixed width
- Use touch-friendly size (≥44px)
- Avoid hover-only interaction

---

## 15. Best Practices

- Prefer `gap` over margin
- Use CSS variables
- Avoid inline styles
- Keep CSS modular
- Use utility classes if needed

---

## 16. One-line Summary

👉 Good UI = consistent spacing + readable text + clean layout + limited color system
