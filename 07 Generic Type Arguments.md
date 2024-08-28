Why We Need Generic Type Arguments
If primitive (and literal) types are data, you can think of generics as functions that operate on that data.

And just like functions often need arguments, we need some way to provide inputs to generic types.

How To Use Generic Arguments
Instead of using parenthesis to pass arguments, with generics we use angled brackets: < and >.

Other than that, there are a lot of similarities between the two concepts.

You can even provide defaults for generic arguments! See the relevant challenge for generic defaults.

There are two separate situations when you'd use this syntax. One is when you're working strictly with types, and another is when you're doing more normal JavaScript-y stuff like with functions and constants.

Universe 1: strictly in the type system
Just take a look:


interface Row<T> {
  label: string;
  value: T;
  disabled: boolean;
}
Note: It's common (and acceptable) in situations like this where we really don't know anything else about the Generic type parameter to use a single letter like T. But the moment you have multiple arguments (or more context for what this type will be) it's a good idea to use more descriptive names.

What this syntax means is that we have a Row type, and we know it will have a value property, but the specific type of that value property is not known until it's used.

We could store numbers in this Row type. If we did, it'd look like this:


type NumberRow = Row<number>;
Or we could store strings:


type StringRow = Row<string>;
Because TypeScript is a structural type system, Row<string> is exactly equivalent (in every way) to if we had written this:


type StringRow = {
  label: string;
  value: string;
  disabled: boolean;
};
But because we used a generic, we didn't have to type all that other stuff out every time.

Multiple Generic Arguments
Just like functions can take multiple arguments, so too can Generics.


type GroceryItem<Name, Price, InStock> = {
  name: Name;
  price: Price;
  inStock: InStock;
};
Now you can pass arguments to this type:


type AvocadoToast = GroceryItem<'Avocado Toast', 12.99, true>;
This is exactly equal to if you had written:


type AvocadoToast = {
  name: 'Avocado Toast';
  price: 12.99;
  inStock: true;
};
Note: you might notice that we're missing types for our type arguments! Right now there's nothing stopping us from sending in wrong values like GroceryItem<number[], boolean, { over: 9000 }>. We'll cover that in a future challenge on generic type constraints.

Solving This Challenge
Similar to what we did with AvocadoToast, create a CapreseSalad type, and fill in the right values to make the tests pass.

Then, create a new generic type for GroceryStore. Let the tests guide you regarding what the final type should look like and what the inputs should be

Code:
type GroceryStore<Name, City> = {
	name: Name,
	city: City,
};

type GroceryItem<Name, Price, InStock> = {
	name: Name,
	price: Price,
	inStock: InStock,
};

type CapreseSalad = GroceryItem<'Caprese Salad', 14.99, true>;