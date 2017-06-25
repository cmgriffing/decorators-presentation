## A Real Example: Angular's Input method decorator

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

---
