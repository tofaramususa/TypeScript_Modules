# What Indexed Types Are For

Indexed types allow you to look inside other types. They're a useful tool when accessing array/tuple values, object values, and more! We're going to see much more complicated uses for indexed types, but for this challenge, let's just focus on the basics.

## How To Use Indexed Types

### Arrays

Just like how you can use a number index to grab an element of an array:

```typescript
const cars = ['Bugatti', 'Ferarri', 'Lambo', 'Porsche', 'Toyota Corolla'];
const secondCar = cars[1];
```

You can do exactly the same thing with types:

```typescript
type Cars = ['Bugatti', 'Ferarri', 'Lambo', 'Porsche', 'Toyota Corolla'];
type SecondCar = Cars[1];
//   ^?
```

Notice that TypeScript evaluates the literal value `"Ferarri"`. It's not just `string`!

### Objects

The same applies to objects:

```typescript
const donations = {
  Bono: 15_000_000,
  'J.K. Rowling': 160_000_000,
  'Taylor Swift': 45_000_000,
  'Elton John': 600_000_000,
  'Angelina Jolie and Brad Pitt': 100_000_000,
};
const eltonDonations = donations['Elton John'];
```

And (you guessed it!) object types:

```typescript
type Donations = {
  Bono: 15_000_000;
  'J.K. Rowling': 160_000_000;
  'Taylor Swift': 45_000_000;
  'Elton John': 600_000_000;
  'Angelina Jolie and Brad Pitt': 100_000_000;
};

type EltonDonations = Donations['Elton John'];
//   ^?
```

Notice that TypeScript evaluates the literal value for Elton's donations. It's not just `number`!

### Strings

If you're getting excited that you might be able to do the same for strings, I have somewhat bad news for you, unfortunately.

The following is valid TypeScript:

```typescript
const question = 'Have the humans delivered their ultimate cup of coffee?';
const firstCharacter = question[0];
```

And this is also valid:

```typescript
type Question = 'Have the humans delivered their ultimate cup of coffee?';
type FirstCharacter = Question[0];
//   ^?
```

But perhaps you notice a difference from the above examples that returned a literal type. Here, with TypeScript strings, the resultant value is just `string` and not a more specific constant value like `"H"` (the first character of the string type). That means that while it's not a syntax error to index a string type, it also effectively does nothing since it will always result in `string`.

In fact, TypeScript doesn't even check (or care about) the specific value you index with. You'll always get back `string`:

```typescript
type Empty = '';
type IndexEmpty = Empty[9001];
//   ^?
```

Not a big deal or anything, but just something to be aware of in case you were expecting a different behavior.

*spoiler alert:* there actually **are** ways to index a string and return a particular character, but it ends up involving some quite advanced type machinery.

## Solving This Challenge

This one should feel easy to pass. Let the tests guide you.

And, remember, while this challenge is pretty straightforward to complete, we're soon going to be doing some pretty advanced work that relies heavily on indexed types.

Onward!

### My Solution:

```typescript
type Cars = ["Bugatti", "Ferarri", "Lambo", "Porsche", "Toyota Corolla"];

type Donations = {
  Bono: 15_000_000;
  'J.K. Rowling': 160_000_000;
  'Taylor Swift': 45_000_000;
  'Elton John': 600_000_000;
  'Angelina Jolie and Brad Pitt': 100_000_000;
};

type TheCoolestCarEverMade = Cars[4];
type TruckDriverBonusGiver = Donations['Taylor Swift'];
