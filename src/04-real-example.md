## A Real Example: Angular's Component decorator

## Component (usage)

```javascript
import { Component, Input } from '@angular/core';
import { Hero } from './hero';
@Component({
  selector: 'hero-child',
  templateUrl: './hero-child.component.html',
  styleUrls: ['./hero-child.component.scss']
})
export class HeroChildComponent {
  // ...
}
```

<div class="notes">
Here we see the template url and style urls.
</div>

## After compiling

![](assets/component-metadata.jpg)

## Logging the component itself

<div class="notes">

When debugging your component implementation things like the selector, template, and styling would just be noise when trying to debug actual functionality.

You might also notice that this has the template and styling as an inline string instead of the file references from the decorator.

We can assume that this is how Angular is "bundling" templates during the js build process.

The scss is also transformed into css with the variables and mixins already reconciled.
</div>

---
