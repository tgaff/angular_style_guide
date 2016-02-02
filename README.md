# comparison of styles


## Examples:

### data- attributes

Use `data-` attributes instead of regular angular attributes.

Avoid:
```html
 <div ng-controller="MainCtrl">
```
Recommended:
```html
 <div data-ng-controller="MainCtrl">
```

### controller as syntax

Use controller as syntax, which promotes use of dot syntax to indicate where variables come from.

Avoid:
```js
<div ng-controller="CustomerController">
    {{ name }}
</div>
```

Recommended:
```html
<div ng-controller="CustomerController as customer">
    {{ customer.name }}
</div>
```

### define named functions for each component first
Declare named functions and build the module afterward.  This does have the downside of excessive chaining, but since we're using named functions it's readable.  We also 

Avoid:
```js
angular
  .module('app', [])
  .controller('MainCtrl', function MainCtrl () {

  })
  .service('SomeService', function SomeService () {

  });
```

Recommended:
```js
function MainCtrl () {

}
function SomeService () {

}
angular
  .module('app', [])
  .controller('MainCtrl', MainCtrl)
  .service('SomeService', SomeService);
 ```
