# Why Generic Arguments Need Defaults

Technically speaking, no program absolutely requires default arguments. It's a convenience feature for the humans writing programs.

Sometimes you have a value in mind for an argument and you don't want to force users of your library to constantly provide the same value over and over again. That's the situation where default arguments come in handy.

## How To Create Default Type Arguments

### First: A Refresher On Function Defaults

Let's take the case of a run-of-the-mill logging function. The logger always needs a message to log, but the log level might be something you want to be optional:

```typescript
type LogLevel = 'debug' | 'info' | 'notice' | 'warning' | 'error' | 'critical';

const log = (message: string, level: LogLevel = 'info') => {
  // application logic
};

log('this has an explicit debug log level', 'debug');
log('this has an implicit info log level');
```

You can do exactly this kind of thing for generic types! This is yet another parallel between functions and generic types!

### Default Generic Arguments

```typescript
type Log<Message, Level = 'info'> = {
  message: Message;
  level: Level;
};

type ExplicitDebugLog = Log<'explicit debug', 'debug'>;
type ImplicitInfo = Log<'implicit info'>;
```

Doesn't that look super similar!? A lot of the same rules apply in types that apply to function argument defaults. For example, you can't have a required argument following a default argument.

One notable exception is that there's no TypeScript value you can pass that will work like `undefined` does for JavaScript default arguments:

```typescript
const greet = (name = 'Stranger') => {
  console.log(`Hello ${name}!`);
};

greet(); // Hello Stranger!
greet(undefined); // Hello Stranger!
greet('Mr. Monkey'); // Hello Mr. Monkey!
```

In TypeScript, even if you provide `never` or `unknown` or `any`, the value will be inserted instead of the default.

## Solving This Challenge

Your goal is to create some types that have the correct default argument.

The second type, `TSConfig`, should feel a bit difficult, but if you get stuck, feel free to check out the hint below:

**Hint**: Start with a literal object as the parameter default. Use indexed types. The error you'll see is because of a missing generic constraint.

### My Solution:

```typescript
type ApiRequest<T, U = 'GET'> = {
  data: T;
  method: U;
};

type TSConfig<T = { strict: true }> = T;
