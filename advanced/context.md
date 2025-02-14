---
title: The Context Object
description: FormKit provides a reactive context object to expose data to slots, rules, and the underlying schema that defines an input.
---

# Context object

FormKit inputs use a reactive object to expose data to slots, rules, and the underlying [schema](/advanced/schema) that defines the input. This is called the `context` object and is found in the each input's [core `node` object](/advanced/core#node) at `node.context`. The context object has the following properties:

<div data-tight>

## `_value`

FormKit inputs have two values — the committed value (`node._value`) and the uncommitted value (`node.value`). At rest, these two values are equivalent, but the uncommitted value is the undebounced raw value of the input.

## `attrs`

An object containing any attributes that will be passed to the internal input element.

## `fns`

A small object of utility functions that are useful when writing schemas.

<client-only>

```js
{
  // Returns the length of a given object
  length: (obj: Record<PropertyKey, any>) => Number,
  // Casts a value to a number
  number: (value: any) => Number,
  // Casts a value to a string
  string: (value: any) => String,
  // Returns the JSON representation of a value
  json: (value: any) => String | false,
}
```
</client-only>

## `handlers`

A small object of common input handlers for use in the schema. Keep in mind that input "features" can replace or add to handlers on an input by input basis.

<client-only>

```js
{
  // sets the state.blurred value to true
  blur: () => void,
  // sets the state.touched value to true
  touch: () => void,
  // Sets the value of the input
  DOMInput: (e: Event) => void
}
```
</client-only>

## `help`

The help text of the input provided by the `help` prop.

## `id`

The unique identifier of the input. This value is auto-generated unless the `id` prop is set.

## `label`

The label of the input provided by the `label` prop.

## `messages`

An object of _visible_ messages (where the type is not `ui` — `ui`). The key of this object is the message name, and the value is a core message object. For example, for an input displaying a single failing validation message, this object would look like:

<client-only>

```js
{
  required_rule: {
    // Determines if the message prevents form submission
    blocking: true,
    // The unique key of this message
    key: 'required_rule',
    // Additional details about the message
    meta: {
      // The name of the validation message (used in message lookups)
      messageKey: 'required',
      // Arguments that can be used in i18n translation
      i18nArgs: [{
        node,
        name: 'email',
        args: []
      }]
    },
    // The "type" of message — generally the plugin that generated it.
    type: 'validation',
    // The value of the message
    value: 'Email is required',
    // If this is a visible message (displayed to end users)
    visible: true
  }
}
```
</client-only>

## `node`

The underlying [core node](/advanced/core) of the current input. This object is not reactive (within the context of Vue).

## `options`

For inputs that accept an options prop, this is a normalized array of option objects.

## `option`

For inputs that accept an options prop, this object is available to [section keys](/essentials/inputs#sections) that are inside the iteration (i.e., the `label` section key on a `checkbox` input with multiple checkboxes). The object contains a `label`, `value`, and sometimes `attrs`:

<client-only>

```js
{
  value: 'foo',
  label: 'Foo',
  attrs: {
    disabled: true
  }
}
```
</client-only>

## `state`

Current state of the input:

<client-only>

```js
{
  // true after the input has had focus and lost it
  blurred: boolean,
  // true after content has been entered by a user
  dirty: boolean,
  // true after the form has attempted submission
  submitted: boolean,
  // true when this input is valid, for groups/lists/forms this is true
  // when all children are valid
  valid: boolean,
}
```
</client-only>

## `type`

The type of the input provided by the `type` prop. This is the value that should be referenced when looking up definitions in a library of inputs. Examples of this value: `text`, `select`, or `autocomplete`.

## `ui`

An object of visible messages (keyed by the `key`) of type `ui` that can be used in the interface. This allows for localized text for use on interface elements.

## `classes`

A Proxy object for requesting classes. This object allows schema authors to request any [section](/essentials/inputs#sections) and get a generative class name. For example `$classes.input` would (by default without additional configuration) return `formkit-input` while `$classes.foobar` would return `formkit-foobar`.

</div>
