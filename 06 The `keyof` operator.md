# The Problem `keyof` Solves

The `keyof` operator is used for extracting a union representing the keys (also known as "properties") of a type.

Let's say your audiophile cousin is asking you to digitize her cassette tape collection (she's convinced they "sound better" on cassette... yawn...). So you make an object where you count up how many albums you have for each artist:

```typescript
const casettesByArtist = {
  'Alanis Morissette': 2,
  'Mariah Carey': 8,
  'Nirvana': 3,
  'Oasis': 2,
  'Radiohead': 3,
  'No Doubt': 3,
  'Backstreet Boys': 3,
  'Spice Girls': 2,
  'Green Day': 2,
  'Pearl Jam': 5,
  'Metallica': 5,
  "Guns N' Roses": 2,
  'U2': 3,
  'Aerosmith': 4,
  'R.E.M.': 4,
  'Blur': 3,
  'The Smashing Pumpkins': 5,
  'Britney Spears': 3,
  'Whitney Houston': 3,
};
```

But what if you wanted to extract all these keys as a type?

We could always re-type all of them in a literal union:

```typescript
type Artists = 
  'Alanis Morissette' | 
  'Mariah Carey' | 
  'Nirvana' |
  'Oasis' | 
  'Radiohead' | 
  'No Doubt' | 
  'Backstreet Boys' |
  'Spice Girls' | 
  'Green Day' | 
  'Pearl Jam' | 
  'Metallica' |
  "Guns N' Roses" | 
  'U2' | 
  'Aerosmith' | 
  'R.E.M.' | 
  'Blur' |
  'The Smashing Pumpkins' | 
  'Britney Spears' | 
  'Whitney Houston';
```

But that's pretty rough. You certainly would not want to retype all those artist names. What if you forget one? What if you misspell one?

Great news: you can use `keyof` to solve this problem!

## How To Use `keyof`

`keyof` is special TypeScript syntax that you use before any type.

In our case, we don't have a type to start working with, so we create one with the `typeof` operator:

```typescript
type CasettesByArtist = typeof casettesByArtist;
```

Then we can use `keyof` on our new type to get an alias that represents the union of all keys in our `casettesByArtist` object:

```typescript
type Artists = keyof CasettesByArtist;
```

## What `keyof` Returns

The result of `keyof` is always a union.

Even if there are 0 or 1 objects, it doesn't hurt to think of the result as a union. If there are no elements in the result, the type will be `never` (which is the empty set in "Set theory" terminology). When there's only one key, then the resulting type will be a single primitive or literal type.

## Solving This Challenge

We have a `getCasetteCount` function that should error if it's passed anything other than a valid artist name from your `casettesByArtist` object.

Remember, we don't want to ever have to retype the keys in the `casettesByArtist` object.

### My Solution:

```typescript
type test = typeof casettesByArtist;

type Artist = keyof test;
