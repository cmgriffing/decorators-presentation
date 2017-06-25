## Metadata

## What is metadata?

Metadata pertains to the code itself rather than the business logic.

eg:

- The name and type of the entity itself
- The name and type of each of its properties
- The name and type of its constructor arguments

## A Simple Example: `readonly` properties

```javascript
const notFoo = { bar: 123 };
notFoo.bar = 456;
// notFoo === { bar: 456 }

type Foo = {
  readonly bar;
}

const foo: Foo = { bar: 123 };
foo.bar = 456;
// Error: Left-hand side of assignment expression
//   cannot be a constant or a read-only property
```

## How might `readonly` be implemented without metadata?

Getters/Setters

```javascript
// regular JavaScript
class Foo {
  _bar;
  get bar() {
    return _bar;
  }
  set bar() {
    throw new Error('bar is a readonly property')
  }
}
```

<div class="notes">
The problem? JavaScript has no concept of a private property. The resulting code would still allow something to modify `_bar` at runtime.
</div>

## But Wait...

TypeScript has `private` properties.

If JavaScript doesn't have `private`, how does TypeScript enforce `private` at runtime? Metadata.

## Another try at a custom readonly property

```
class Foo {
  @readonly bar;
  get bar() {
    return _bar;
  }
  set bar() {
    throw new Error('bar is a readonly property')
  }
}

function readonly(target, name, descriptor) {
  
  return descriptor;
}
```

---
