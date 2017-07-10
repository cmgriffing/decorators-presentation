## A Real Example: Angular's Input decorator

## Input (usage)

```javascript
import { Component, Input } from '@angular/core';
import { Hero } from './hero';
@Component({
  selector: 'hero-child',
  template: `
    <h3>{{hero.name}} says:</h3>
    <p>I, {{hero.name}}, am at your service, {{masterName}}.</p>
  `
})
export class HeroChildComponent {
  @Input() hero: Hero;
  @Input('master') masterName: string;
}
```

<div class="notes">
I borrowed this usage code from the Angular Tour of Heroes tutorial.

There is a lot going on here. Let us ignore @Component for now and concentrate on Input.

In Angular, an Input is a value or Prop passed down from a parent component.
</div>

## Input (implementation)

```javascript
// the input decorator from @angular/angular/packages/core/src/metadata/directives.ts
export const Input: InputDecorator =
    makePropDecorator('Input', (bindingPropertyName?: string) => ({bindingPropertyName}));
```

```javascript

// the makePropDecorator utility method from @angular/angular/packages/core/src/util/decorators.ts
export function makePropDecorator(
    name: string, props?: (...args: any[]) => any, parentClass?: any): any {
  const metaCtor = makeMetadataCtor(props);

  function PropDecoratorFactory(...args: any[]): any {
    if (this instanceof PropDecoratorFactory) {
      metaCtor.apply(this, args);
      return this;
    }

    const decoratorInstance = new (<any>PropDecoratorFactory)(...args);

    return function PropDecorator(target: any, name: string) {
      const meta = Reflect.getOwnMetadata('propMetadata', target.constructor) || {};
      meta[name] = meta.hasOwnProperty(name) && meta[name] || [];
      meta[name].unshift(decoratorInstance);
      Reflect.defineMetadata('propMetadata', meta, target.constructor);
    };
  }

  if (parentClass) {
    PropDecoratorFactory.prototype = Object.create(parentClass.prototype);
  }

  PropDecoratorFactory.prototype.toString = () => `@${name}`;
  (<any>PropDecoratorFactory).annotationCls = PropDecoratorFactory;
  return PropDecoratorFactory;
}
```

<div class="notes">
There is a lot going on here. I don't even fully understand everything that is happening here yet.

However, one thing that stands out to me is the use of the word Metadata in some of the function names.

One purpose of this decorator is to make sure Angular is taking note of the fact that the html element for this component will be expecting attributes called hero and master.

It does this so that it can warn you at compile time whether an expected attriubute is missing from the usage in the template.

There is probably even more going on here but I want to concentrate on the metadata part.
</div>

---
