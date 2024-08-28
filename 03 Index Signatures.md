# When Index Signatures Save The Day

It's common in any language to make general-purpose mappings of one type to another type.

Look at this theoretical API response from your company. This is a `/followerCountByUser` endpoint, and we pass in some user we're looking at:

```
https://yourcompany.com/api/v1/followerCountByUser
```

```json
{
  "info": {
    "count": 9001,
    "currentPage": 1,
    "pages": 22
  },
  "results": {
    "user_ddb04d2e-21ff-4c68-9bdc-135c16c8e74a": 0,
    "user_1e118b25-c0b9-4bfc-8d04-901ad8a2eb20": 3,
    "user_7c56283c-6a5e-4d79-bdd0-9c6a3cafd2c4": 15,
    "user_2eac2f5e-4f11-4d36-84b5-9d273816d6f6": 7,
    "user_4b88b4a3-8d42-4fc9-9f73-8db296d9b03d": 88,
    "user_af836d5e-16a2-452d-bec4-694d6cd8e49f": 92,
    "user_610c236f-b3bb-45e9-a09b-1d7e362c7fbb": 14,
    "user_7a8e29f0-d7b0-4b75-9ad2-c8a145073eab": 6,
    "user_eaa914df-4650-4c3b-9a04-723b5a63f297": 764,
    "user_3199b7c6-7a8d-47eb-ae94-4e3457ad7760": 32
    // ... for many more rows in this page
  }
}
```

How would you write a type for your company's endpoint that returned data like this?

In the real world, you're going to have other things going on in types that might distract you. But don't get distracted by the pagination info. Let's zoom in on the `results` object.

`results` seems to be some kind of mapping of user IDs to a follower count. It's an object where the keys are (more or less) random strings and the values are all numbers.

This turns out to be exactly the scenario for TypeScript index signatures!

## How To Use Index Signatures

In our case, here's how it looks:

```typescript
type Results = {
  [userId: string]: number;
};
```

Let's really break this down piece by piece:

1. **`type`** starts a type declaration (we could also have used `interface` here).
2. **`Results`** is the name we're giving to this type.
3. **`=`** and `{` opens a new object type declaration.
4. **`[`** is the TypeScript syntax that says "hey, we're going to start defining a property name now".
5. **`userId`** is completely arbitrary. It's just a name that we picked. It has no impact on the resulting type.
6. **`: string`** this part indicates the type associated with this property.
7. **`]`** ends the property name declaration.
8. **`: number`** specifies that the type of values for this key are `number`.
9. **`}`** signals the end of the object type declaration.

*By the way: a massively misunderstood fact about JavaScript has to do with object keys. JavaScript object keys can only be strings or symbols. THAT'S IT. Period. No other data types are possible to store as object keys.*

Part of the reason this is so commonly misunderstood is because you can index an object with a number, or a boolean, and actually more, and it will often work, which gives the wrong impression. JavaScript will coerce anything you store as an object key to a string.

Unfortunately (and widely seen as a small mistake in TypeScript's design), TypeScript actually allows setting numeric keys (so if you replaced `: string` with `: number` in the type above). This can give you the impression that you can set object keys as numbers, when in fact you cannot.

Just watch out for this sneaky footgun in JavaScript.

So wrapping it all up, our type for this API might look like this:

```typescript
type Info = {
  count: number;
  currentPage: number;
  pages: number;
};

type FollowerCountByUserResults = {
  [userId: string]: number;
};

type FollowerCountByUser = {
  info: Info;
  results: FollowerCountByUserResults;
};
```

Or, we could always inline everything (this works just fine with index signatures):

```typescript
type FollowerCountByUser = {
  info: {
    count: number;
    currentPage: number;
    pages: number;
  };
  results: {
    [userId: string]: number;
  };
};
```

## Solving This Challenge

Take a look at the tests. You'll see some objects. Try to make types (using index signatures) that match those objects.

### My Solution:

```typescript
type GroceryList = {
  [itemName: string]: number;
};

type InappropriateActionBySituation = {
  [action: string]: string[];
};

type CharactersById = {
  [id: number]: {
    id: number;
    name: string;
    status: string;
    species: string;
  };
};
