# JavaScript Object — Key & Value Types Summary

---

## PART 1: KEY Types

In a plain JavaScript object, keys can only be **String** or **Symbol**.
All other types are **automatically converted to a string**.

### Key Type Behavior Table

| Key Type | Accepted? | What Actually Happens | Example Result |
|---|---|---|---|
| `string` | ✅ Native | Stays as-is | `"name"` |
| `number` | ⚠️ Converted | Becomes a string | `1` → `"1"` |
| `boolean` | ⚠️ Converted | Becomes a string | `true` → `"true"` |
| `object` | ⚠️ Converted | Becomes `"[object Object]"` | `{a:1}` → `"[object Object]"` |
| `array` | ⚠️ Converted | Becomes string of elements | `[1,2]` → `"1,2"` |
| `null` | ⚠️ Converted | Becomes `"null"` | `null` → `"null"` |
| `undefined` | ⚠️ Converted | Becomes `"undefined"` | `undefined` → `"undefined"` |
| `Symbol` | ✅ Native | Stays as Symbol (unique, hidden) | `Symbol("id")` |

### Key Examples

```javascript
const obj = {}

obj["name"]      = "string key"   // ✅ normal
obj[1]           = "number key"   // ⚠️ key becomes "1"
obj[true]        = "boolean key"  // ⚠️ key becomes "true"
obj[{a:1}]       = "object key"   // ⚠️ key becomes "[object Object]"
obj[[1,2]]       = "array key"    // ⚠️ key becomes "1,2"
obj[null]        = "null key"     // ⚠️ key becomes "null"
obj[undefined]   = "undef key"    // ⚠️ key becomes "undefined"
obj[Symbol("id")]= "symbol key"   // ✅ stays as Symbol

console.log(Object.keys(obj))
// ["name", "1", "true", "[object Object]", "1,2", "null", "undefined"]
// ↑ Symbol is hidden and NOT shown here!
```

---

## PART 2: VALUE Types

JavaScript object values are **completely flexible** — any type is allowed.

### Value Type Table

| Value Type | Allowed? | Example |
|---|---|---|
| `string` | ✅ Yes | `{ name: "John" }` |
| `number` | ✅ Yes | `{ age: 30 }` |
| `boolean` | ✅ Yes | `{ active: true }` |
| `null` | ✅ Yes | `{ data: null }` |
| `undefined` | ✅ Yes | `{ data: undefined }` |
| `object` | ✅ Yes | `{ address: { city: "LA" } }` |
| `array` | ✅ Yes | `{ scores: [1, 2, 3] }` |
| `function` | ✅ Yes | `{ greet: () => "Hello" }` |
| `Symbol` | ✅ Yes | `{ id: Symbol("id") }` |
| `BigInt` | ✅ Yes | `{ big: 9007199254740991n }` |
| `NaN` | ✅ Yes | `{ val: NaN }` |
| `Infinity` | ✅ Yes | `{ val: Infinity }` |

### Value Examples

```javascript
const obj = {
  str:       "Hello",                    // string
  num:       42,                         // number
  float:     3.14,                       // number (float)
  bool:      true,                       // boolean
  nothing:   null,                       // null
  notSet:    undefined,                  // undefined
  nested:    { city: "LA" },             // object
  list:      [1, 2, 3],                  // array
  fn:        () => "I am a function",    // function
  sym:       Symbol("unique"),           // Symbol
  big:       9007199254740991n,          // BigInt
  nan:       NaN,                        // NaN
  inf:       Infinity,                   // Infinity
}
```

---

## PART 3: Full Comparison — Object vs Map

| Feature | Plain Object `{}` | `Map` |
|---|---|---|
| Key: string | ✅ | ✅ |
| Key: Symbol | ✅ | ✅ |
| Key: number | ⚠️ Converted to string | ✅ Stays as number |
| Key: object | ⚠️ Converted to string | ✅ Stays as object |
| Key: any type | ❌ | ✅ |
| Value: any type | ✅ | ✅ |
| Key order guaranteed | ⚠️ Mostly yes (ES2015+) | ✅ Always insertion order |
| Easy size check | ❌ `Object.keys(obj).length` | ✅ `map.size` |
| JSON serializable | ✅ `JSON.stringify()` | ❌ Not directly |

---

## PART 4: Quick Rule of Thumb

> - **String/Symbol keys, any values** → Use plain **object `{}`**
> - **Any type as key** → Use **`Map`**
> - **Unique hidden key** → Use **`Symbol`**
> - **Large integers** → Use **`BigInt`** as value
> - **Nothing / empty value** → Prefer **`null`** over `undefined` for clarity

---

## PART 5: Common Pitfalls

### ⚠️ Object as key — silent overwrite
```javascript
const obj = {}
obj[{a: 1}] = "first"
obj[{b: 2}] = "second"  // overwrites! both keys → "[object Object]"
console.log(obj)         // { "[object Object]": "second" }
```

### ⚠️ undefined value still creates the key
```javascript
const obj = { name: undefined }
console.log("name" in obj)  // true ← key EXISTS even though value is undefined
console.log(obj.name)       // undefined
```

### ⚠️ Symbol keys are invisible to normal methods
```javascript
const sym = Symbol("id")
const obj = { [sym]: 123, name: "John" }

console.log(Object.keys(obj))   // ["name"]  ← sym is hidden!
console.log(Object.values(obj)) // ["John"]  ← sym value is hidden!

// To see Symbol keys:
console.log(Object.getOwnPropertySymbols(obj)) // [Symbol(id)]
```
