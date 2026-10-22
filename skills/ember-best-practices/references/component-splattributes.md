---
title: Spread ...attributes on the Right Element, in the Right Position
impact: MEDIUM
impactDescription: Callers' attributes and modifiers reach the right element, and none are silently dropped
tags: components, attributes, splattributes, forms, accessibility
---

## Spread ...attributes on the Right Element, in the Right Position

**Impact: MEDIUM (callers' attributes and modifiers reach the right element, and none are silently dropped)**

`...attributes` forwards everything a caller writes on a component that isn't an argument (`class`, `name`, `aria-*`, `data-*`, and modifiers such as `{{on}}`) to the element it's placed on. Put it on the element those are meant for, which isn't always the root. In a field that renders a label, an input and a hint, that's the `<input>`: on the wrapper, `name`, `autocomplete` and `aria-describedby` do nothing. If callers also need to style the wrapper, take its class as an argument.

Where `...attributes` sits among the element's own attributes decides which value wins:

- **Before `...attributes`:** a default the caller can override.
- **After it:** the component's value wins, and an empty value (`undefined`, `null` or `false`) removes the caller's attribute.

`class` is merged either way. As the Ember Guides advise, most attributes go before `...attributes`. Put after it only what the component must control, such as the `id` its `<label for>` points at, or the `value` it takes as `@value`. Anything a caller may also set goes before it, above all an attribute the component sets only sometimes, such as an `aria-describedby` for an optional hint.

**Incorrect (attributes land on the wrapper):**

```glimmer-js
// app/components/text-field.gjs
import Component from '@glimmer/component';
import { guidFor } from '@ember/object/internals';

export class TextField extends Component {
  id = guidFor(this);

  <template>
    <div class="text-field" ...attributes>
      <label for={{this.id}}>{{@label}}</label>
      <input id={{this.id}} value={{@value}} />
    </div>
  </template>
}
```

`<TextField @label="Email" name="email" autocomplete="email" />` puts `name` and `autocomplete` on the `<div>`, where they do nothing: the form doesn't submit the field, and the browser gets no autofill hint.

**Incorrect (an attribute the component sets only sometimes comes after `...attributes`):**

```handlebars
<input ...attributes id={{this.id}} aria-describedby={{if @hint this.hintId}} value={{@value}} />
```

Without `@hint`, `aria-describedby` is `undefined` after `...attributes`, so a caller's `aria-describedby` is removed.

**Correct (on the `<input>`, with only what the component controls after `...attributes`):**

```glimmer-js
// app/components/text-field.gjs
import Component from '@glimmer/component';
import { guidFor } from '@ember/object/internals';

export class TextField extends Component {
  id = guidFor(this);
  hintId = `${this.id}-hint`;

  <template>
    <div class="text-field {{@wrapperClass}}">
      <label for={{this.id}}>{{@label}}</label>
      <input
        aria-describedby={{if @hint this.hintId}}
        ...attributes
        id={{this.id}}
        value={{@value}}
      />
      {{#if @hint}}
        <p id={{this.hintId}}>{{@hint}}</p>
      {{/if}}
    </div>
  </template>
}
```

`name`, `autocomplete` and `{{on "input"}}` now reach the `<input>`, and an `id` attribute can't separate it from its label. A caller's `aria-describedby` is kept when there's no hint, and overrides the hint's when there is one.

Reference: [Ember Guides: Component Arguments and HTML Attributes](https://guides.emberjs.com/release/components/component-arguments-and-html-attributes/)
