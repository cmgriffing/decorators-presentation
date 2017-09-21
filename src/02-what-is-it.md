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
Bares most similarity to Python decorators and is also the likely source of the name "Decorators"
</div>

## The Spec Proposal

**Stage-2 (draft)**: Authored by Yehuda Katz of Ember fame
    
- [http://tc39.github.io/proposal-decorators/](http://tc39.github.io/proposal-decorators/)
- [https://github.com/wycats/javascript-decorators](https://github.com/wycats/javascript-decorators)

<div class="notes">

According to the tc39 process:

Stage-2:

- formal description of syntax and semantics
- decription must be as complete as possible
- Two experimental implementations. but one of them can be in a transpiler

* Only incremental changes are expected from now on.

</div>

## Availability
### TypeScript

Currently uses Stage-0 version of spec

### Babel

* [Stage-0 Legacy transform](https://github.com/loganfsmyth/babel-plugin-transform-decorators-legacy)

* [Stage-2 Transform (Work In Progress as a Babel Proposal) ](https://github.com/babel/proposals/issues/11)

<div class="notes">

Both TypeScript and Babel currently only support the Stage-0 version of the spec.

- Babel Stage-2 transform is in progress.
- Legacy (Stage-0) transform will be Babel 7 default. (mimics Babel 5 decorator behavior)

</div>

## Angular Examples

![](assets/angular2-decorators.jpg)

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
