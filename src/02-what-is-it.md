## What are they?

A decorator is:

- an expression
- that evaluates to a function
- that takes the target, name, and decorator descriptor as arguments
- and optionally returns a decorator descriptor to install on the target object

## Similarities in Other Languages

- **Python**: Decorators
- **Java**: Annotations
- **C#**: Attributes

<div class="notes">
Bares most similarity to Python decorators and is also the likely source of the name, decorators
</div>

## The Spec Proposal

**Stage-2 (draft)**: Authored by Yehuda Katz of Ember fame
    
- (http://tc39.github.io/proposal-decorators/)
- (https://github.com/wycats/javascript-decorators)

<div class="notes">

According to the tc39 process:

Stage-2:

- The proposal must now additionally have a formal description of the syntax and semantics of the feature.
- The description should be as complete as possible, but can contain todos and placeholders.
- Two experimental implementations of the feature are needed, but one of them can be in a transpiler such as Babel. (in this case: Babel, Typescript)

* Only incremental changes are expected from now on.

Yehuda's interest?
- Glimmer is written in Typescript
- Yehuda previously wrote about implementing Python decorators in Ruby back in 2009

</div>

## Availability
- TypeScript
- Babel? (kind of, but not really. WIP)

<div class="notes">

- Babel Stage-2 transform is in progress.
- Legacy transform will be Babel 7 default.
    (mimics Babel 5 decorator behavior that is likely to change)

The difference?
The spec may change regarding the execution model. eg: the parameters you receive and order of operations.

The bulk of the spec is unlikely to change.

</div>

## TypeScript Examples

![Angular2 decorators in action](assets/angular2-decorators.jpg)

<div class="notes">
Angular2 makes heavy use of decorators.
</div>

## Types of Decorators (in the spec)

- Class Declaration
- Class Method Declaration
- Class Accessor Declaration (getters/setters)
- Object Literal Method Declaration
- Object Literal Accessor Declaration

---
