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
angular
  .module('app', [])
  .controller('MainCtrl', MainCtrl)
  .service('SomeService', SomeService);


function MainCtrl () {

}
function SomeService () {

}
 ```

### always pass objects, not values

ng-model="obj.foo"
vs. 
ng-model="foo"


### Factories vs. services

Use Factories


## Directives

### inject vs. inline annotation
Use $inject vs. inline annotation
PhoneListCtrl.$inject = ['$scope', '$http'];
https://docs.angularjs.org/tutorial/step_05

### use gulp or grunt once we get to mean
Use ng-annotate for Gulp or Grunt
*Use restrict (but not for students)
