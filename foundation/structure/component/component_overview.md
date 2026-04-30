# Component Overview

## 1. Definition

A **component** is a fundamental building block in modern frontend development.

> A component is an abstraction that encapsulates **UI, state, and behavior** into an independent and reusable unit.

---

## 2. Core Characteristics

### 2.1 Encapsulation
A component bundles:
- UI (template / JSX)
- State (data)
- Behavior (logic)

This improves maintainability and isolation.

---

### 2.2 Reusability
Components can be reused across different parts of the application.

Example:
- Button
- Modal
- Table
- Form

---

### 2.3 Composability
Components can be combined to form more complex UIs.

```
App
 ├── Header
 ├── Sidebar
 └── Content
       ├── Card
       └── Table
```

---

### 2.4 Independence
A well-designed component:
- Has clear input (props)
- Has controlled internal state
- Minimizes external dependencies

---

## 3. Component Model

A typical component consists of:

### Input
- Props / Parameters

### Internal State
- Local data / reactive state

### Output
- UI rendering
- Events / callbacks

---

## 4. Why Use Components?

### 4.1 Manage Complexity
Break large UI into smaller, manageable parts.

### 4.2 Improve Maintainability
Changes are localized to specific components.

### 4.3 Enable Reuse
Avoid duplicating UI and logic.

### 4.4 Enhance Readability
Structure reflects business logic.

---

## 5. Concept vs Implementation

### Concept Level (Framework-agnostic)
Component is an abstract design concept.

### Implementation Level (Framework-specific)

#### React
```jsx
function Button() {
  return <button>Click</button>
}
```

#### Vue
```vue
<template>
  <button>Click</button>
</template>
```

#### Angular
```ts
@Component({...})
export class ButtonComponent {}
```

---

## 6. Component vs UI Library

| Aspect | Component | UI Component Library |
|------|----------|---------------------|
| Definition | Concept / building block | Pre-built components |
| Dependency | Independent concept | Depends on framework |
| Purpose | Structure and abstraction | UI reuse and styling |

---

## 7. When to Create a Component?

You should extract a component when:

- The UI is reused
- The logic is independent
- The file becomes too complex
- The part has its own state

---

## 8. Key Takeaway

> A component is not just for reuse, but a core abstraction for structuring UI, managing complexity, and organizing application logic.

---

## 9. One-Line Summary

> Component = UI + State + Behavior (encapsulated unit)
