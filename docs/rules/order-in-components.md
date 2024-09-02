# ember/order-in-components

🔧 This rule is automatically fixable by the [`--fix` CLI option](https://eslint.org/docs/latest/user-guide/command-line-interface#--fix).

<!-- end auto-generated rule header -->

Note: this rule will not be added to the `recommended` configuration because it enforces an opinionated, stylistic preference.

## Configuration

<!-- begin auto-generated rule options list -->

| Name    | Type  |
| :------ | :---- |
| `order` | Array |

<!-- end auto-generated rule options list -->

```js
const rules = {
  'ember/order-in-components': [
    2,
    {
      order: [
        'spread',
        'service',
        'property',
        'empty-method',
        'single-line-function',
        'multi-line-function',
        'observer',
        'constructor'
        'init',
        'didReceiveAttrs',
        'willRender',
        'willInsertElement',
        'didInsertElement',
        'didRender',
        'didUpdateAttrs',
        'willUpdate',
        'didUpdate',
        'willDestroy',
        'willDestroyElement',
        'willClearRender',
        'didDestroyElement',
        'action',
        'actions',
        'method'
      ]
    }
  ]
};
```

If you want some of properties to be treated equally in order you can group them into arrays, like so:

```js
order: [
  'service',
  'property',
  ['single-line-function', 'multi-line-function'],
  'observer',
  'constructor',
  'init',
  'didReceiveAttrs',
  'willRender',
  'willInsertElement',
  'didInsertElement',
  'didRender',
  'didUpdateAttrs',
  'willUpdate',
  'didUpdate',
  'willDestroy',
  'willDestroyElement',
  'willClearRender',
  'didDestroyElement',
  'action',
  'actions',
  ['method', 'empty-method'],
];
```

### Custom Properties

If you would like to specify ordering for a property type that is not listed, you can use the custom property syntax `custom:myPropertyName` in the order list to specify where the property should go.

### Additional Properties

You can find the full list of properties [here](../../lib/utils/property-order.js#L10).

## Description

You should write code grouped and ordered in this way:

1. Services
2. Default values
3. Single line computed properties / getters & setters
4. Multiline computed properties / getters & setters
5. Observers
6. Lifecycle Hooks (in execution order)
7. Actions
8. Custom / private methods

## Examples

```js
const {
  Component,
  computed,
  inject: { service },
} = Ember;
const { alias } = computed;

export default Component.extend({
  // 1. Services
  i18n: service(),

  // 2. Properties
  role: 'sloth',

  // 3. Empty methods
  onRoleChange() {},

  // 4. Single line Computed Property
  vehicle: alias('car'),

  // 5. Multiline Computed Property
  levelOfHappiness: computed('attitude', 'health', function () {
    const result = this.attitude * this.health * Math.random();
    return result;
  }),

  // 6. Observers
  onVehicleChange: observer('vehicle', function () {
    // observer logic
  }),

  // 7. Lifecycle Hooks
  init() {
    // custom init logic
  },

  didInsertElement() {
    // custom didInsertElement logic
  },

  willDestroyElement() {
    // custom willDestroyElement logic
  },

  // 8. All actions
  actions: {
    sneakyAction() {
      return this._secretMethod();
    },
  },

  // 9. Custom / private methods
  _secretMethod() {
    // custom secret method logic
  },
});
```

```js
import { action } from "@ember/object";
import { inject as service } from '@ember/service';
import { tracked } from "@glimmer/tracking";
import Component from '@glimmer/component';

export default class ExampleClass extends Component {
  // 1. Services
  @service() i18n;

  // 2. Properties
  @tracked fooBar;
  role = 'sloth';

  // 3. Empty methods
  onRoleChange() {},

  // 4. Single line getters/setters or Computed property
  @alias('car') get vehicle() {}

  // 5. Multiline getters/setters or Computed property
  @computed('attitude', 'health')
  get levelOfHappiness() {
    const result = this.attitude * this.health * Math.random();
    return result;
  }

  // 6. Observers
  @observer('vehicle')
  onVehicleChange() {
    // observer logic
  }

  // 7. Lifecycle Hooks
  constructor(owner, args) {
    // custom constructor logic
  }

  willDestroy() {
    // custom willDestroy logic
  }

  // 8. Actions
  @action
  sneakyAction() {
    return this._secretMethod();
  }

  // 9. Custom / private methods
  _secretMethod() {
    // custom secret method logic
  }
}
```
