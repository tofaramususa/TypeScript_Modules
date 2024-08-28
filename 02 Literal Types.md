# The Problem Literal Types Solve

JavaScript, like most programming languages, has a concept of primitive data types. Primitive data types are things like `string`, `number`, and `boolean`.

But TypeScript isn't like most programming languages. It's better. It takes things to the next level by introducing **literal data types**.

You can think of literal data types as being an infinite set of subsets of their primitive counterparts. For example:

## A Practical Use-Case

Literal types can be used to create a rainbow of possibilities. In this case, we've defined a type `RainbowColor` that can only have one of the types specified in a union of literal strings.

```typescript
type RainbowColor = 'red' | 'orange' | 'yellow' | 'green' | 'blue' | 'indigo' | 'violet';
```

Then, we can use this type in a function to ensure bad values are not passed in:

```typescript
function pickColor(color: RainbowColor): void {
  console.log(`I choose the color ${color}!`);
}

// no error: TypeScript is happy!
pickColor('yellow');

// Error: Argument of type 'purple' is not assignable to parameter of type 'RainbowColor'.
pickColor('purple');
// ^?
```

By the way, did you know that purple's not in the rainbow because there's no "purple" wavelength of light? It's true. Our brains fabricate it for us to make sense of paradoxical visual inputs.

## Literal Types for Returns

But wait! There's A LOT more! Literal types are useful for returns, too. Check out this code:

```typescript
type Day = 'Monday' | 'Tuesday' | 'Wednesday' | 'Thursday' | 'Friday' | 'Saturday' | 'Sunday';

const isItPartyTime = (day: Day) => {
  switch (day) {
    case 'Friday':
    case 'Saturday':
    case 'Sunday':
      return 'definitely party time';

    default:
      return 'prolly lay low for now';
  }
};

isItPartyTime('Monday');
// ^?
```

The above example assumes a 4-day workweek since 4-day workweeks are observed to increase employee productivity.

The return type for this function is also a literal type union. Notice that you didn't have to specify the return type anywhere. It just works this way in TypeScript. Nice.

## Why Are Type Literals Even Necessary?

If you're thinking to yourself:

*Why are type literals even necessary? Lots of languages don't have anything like this, and they seem to get along just fine with primitive types like string and number and boolean.*

The TLDR; is: once you pair type unions with literals, you can start discriminating inputs based on one particular literal instance of a type versus another. TypeScript suddenly becomes capable of doing some pretty amazing static analysis on your code that you could never do if all you had were primitive types. If that's unpalatable to you, there's always COBOL. Try that out instead maybe?

## Solving this Challenge

In this prompt, we talked mostly about string literals, but there are more kinds:

- **number literals** (including fractional numbers)
- **boolean literals**
- **function literals**
- **object literals**

Take a look at the tests and see if you can create some type literals that will satisfy the tests.

### My Solution:

```typescript
type LiteralString = 'chocolate chips';
type LiteralTrue = true;
type LiteralNumbers = 1 | 2 | 3 | 4 | 5 | 6;
type LiteralObject = {
  name: 'chocolate chips';
  inStock: true;
  kilograms: 5;
};
type LiteralFunction = (a: number, b: number) => number;

const literalString = 'Ziltoid the Omniscient';
const literalTrue = true;
const literalNumber = Math.random() > 0.5 ? 1 : 2;
const almostPi = 3.14159265358979323846264338327950288419716939937510582097494459230781640628620899862803482534211706798214808651328230664709384460955058223172535940812848111745028410270193852110555964462294895493038196442881097566593344612847564823378678316527120190914564856692346034861045432664821339360726024914127372458700660631558817488152092096282925409171536436789259036001133053054882046652138414695194151160943305727036575959195309218611738193261179310511854807446237996274956735188575272489122793818301194912983367336244065664308602139494639522473719070217986094370277053921717629317675238467481846766940513200056812714526356082778577134275778960917363717872146844090122495343014654958537105079227968925892354201995611212902196086403441815981362977477130996051870721134999999837297804995105973173281609631859502445945534690830264252230825334468503526193118817101000313783875288658753320838142061717766914730359825349042875546873115956286388235378759375195778185778053217122680661300192787661119590921642019891337;
const literalObject = {
  origin: 'string',
  command: 'string',
  item: 'string',
  time: 'string',
};
const literalFunction = (a: number, b: string): string | number => {
  return a + b;
};
