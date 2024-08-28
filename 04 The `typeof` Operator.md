# `typeof`: A Bridge Between Worlds

Have we said thank you yet for taking these TypeHero challenges? Well... **THANK YOU!**

You're doing yourself a great service by improving your knowledge of TypeScript. As you dig deeper, on your quest to become a TypeScript wizard, you're going to start noticing that there are almost two worlds: the "JavaScript" world and the "types" world.

| JavaScript world | Types world |
|------------------|-------------|
| variables        | `const`, `let`, function arguments | type aliases, default generic arguments |
| operations       | for loops, while loops, recursion, higher-order functions | recursion, higher-order types |
| runtime artifacts| ✅          | ❌ |
| time of error    | runtime     | compile time |
| constructs       | statements, expressions | expressions |

Perhaps you see a problem this divide might cause. What happens if you have information in JavaScript that you want to bring over to TypeScript?

```markdown
raw data
|              conversion
|              |            types
|              |            |
v              v            v
JavaScript ==> `typeof` ==> TypeScript
```

## How to Use `typeof`

### `typeof` in JavaScript

You might be familiar with `typeof` as a JavaScript operator. It returns a string indicating the type of a JavaScript value.

```javascript
console.log(typeof "Euler's Number");
// -> logs the string `'string'`

console.log(typeof 2.7182);
// -> logs the string `'number'`
```

But that's JavaScript. The `typeof` operator also exists in TypeScript!

### `typeof` in TypeScript

What if we wanted to use some of our data as a type in TypeScript?

```typescript
const name = "Euler's Number";
const value = 2.7182;

// we can use `typeof` for type aliases
type Value = typeof value;

interface FamousNumbers {
  // or we can use it inline
  label: typeof name;
  value: Value;
}

const count = 42;
type Count = typeof count;
```

### `typeof` Is Most Useful For Complex Types

`typeof` is a TypeScript keyword that you put before a JavaScript identifier like a variable name. Let's say you have this function in your codebase:

```typescript
const createPoint = (x: number, y: number) => ({ x, y });
```

You can use `typeof` to extract the type of this JavaScript function and bring it into the realm of TypeScript types:

```typescript
//                        JavaScript stuff
//                        |
//                        v----------
type CreatePoint = typeof createPoint;
//^----------------------
//|
//| TypeScript stuff
```

Later, you're going to learn about ways to do more operations on types. We'll be extracting keys of objects and creating new types for return types and parameters of functions.

## Solving This Challenge

The tests provide you with some data. Try to make all the tests pass by using that data combined with the `typeof` operator.

### My Solution:

```typescript
type Width = typeof width;

const object2 = {
  top: 20,
  right: 30,
  bottom: 40,
  left: 50,
};
type Margin = typeof object2;

const data1 = { category: 'going', value: 1 };
type Data = typeof data1[];

const yscale1 = {
  type: "string",
  domain: [1, 31, 35],
  range: [1, 42, 24],
};

type YScale = typeof yscale1;

const chart = {
  width: 13,
  height: 13,
  margin: {
    top: 20,
    right: 30,
    bottom: 40,
    left: 50,
  },
  data: [{ category: 'going', value: 1 }],
  xScale: {
    type: "string",
    domain: [34, 24],
    range: [34, 24],
  },
  yScale: {
    type: "string",
    domain: [34, 24],
    range: [34, 24],
  },
  xAxis: {
    label: "string",
    tickSize: 24,
  },
  yAxis: {
    label: "string",
    tickSize: 24,
  },
  bar: {
    fill: "string",
  },
};

type D3ChartConfig = typeof chart;
