## Metadata

## What is metadata?

Metadata pertains to the code itself rather than the business logic.

eg:

- The name and type of the entity itself
- The name and type of each of its properties
- The name and type of its constructor arguments

## @Component: An Angular-based example

```javascript
@Component({
  selector: 'iv-sale-property-page',
  templateUrl: './sale-property-page.component.html',
  styleUrls: ['./sale-property-page.component.scss']
})
export class SalePropertyPageComponent implements OnInit {
  // ...
}
```

## @Component Metadata

![Component Metadata](assets/component-metadata.jpg)

<div class="notes">

When debugging your component implementation things like the selector, template, and styling would just be noise when trying to debug actual functionality.

You might also notice that this has the template and styling as an inline string instead of the file references from the decorator.

We can assume that this is how Angular is "bundling" templates during the js build process.

The scss is also transformed into css with the variables and mixins already converted.
</div>

---
