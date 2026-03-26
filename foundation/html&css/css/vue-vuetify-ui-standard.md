# Vue 3 + Vuetify UI Standard (Practical Guide)

## 1. Core Principles

- Consistency > Fancy UI
- Use Vuetify as base, DO NOT fight it
- Prefer props over custom CSS
- Use design tokens (spacing, color, typography)
- Keep layout simple and predictable

---

## 2. Layout Standard

### Page Layout

```vue
<v-container fluid>
  <v-row>
    <v-col cols="12" md="8">
      Main Content
    </v-col>
    <v-col cols="12" md="4">
      Sidebar
    </v-col>
  </v-row>
</v-container>
```

Guidelines:
- Use `v-container` for page wrapper
- Use `v-row` + `v-col` for layout
- Follow 12-grid system

---

## 3. Spacing Standard

Use 8px scale:

```text
4px / 8px / 16px / 24px / 32px
```

Vuetify classes:

```html
pa-2   <!-- padding 8px -->
ma-4   <!-- margin 16px -->
gap-4  <!-- gap 16px -->
```

---

## 4. Typography Standard

```css
body {
  font-size: 14px;
  line-height: 1.6;
}
```

Use Vuetify:

```html
<div class="text-h6">Title</div>
<div class="text-body-1">Content</div>
<div class="text-caption">Helper</div>
```

---

## 5. Color Standard

Use Vuetify theme config for colors.

---

## 6. Button Standard

```html
<v-btn color="primary">Submit</v-btn>
```

---

## 7. Form Standard

```html
<v-text-field label="Name" />
<v-select :items="items" label="Type" />
```

---

## 8. Card Standard

```html
<v-card class="pa-4">
  <v-card-title>Title</v-card-title>
  <v-card-text>Content</v-card-text>
</v-card>
```

---

## 9. Responsive Design

```html
<v-col cols="12" md="6" lg="4">
```

---

## 10. One-line Summary

👉 Good Vuetify UI = consistent spacing + simple layout + minimal custom CSS
