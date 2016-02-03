# Purpose

There are many good styleguides already available for Angular. [here](https://github.com/toddmotto/angular-styleguide) and [here](https://github.com/johnpapa/angular-styleguide)  So, why do we need another one?

This styleguide is different in that it's focused on teaching & learning Angular.  The syntax and structures advocated by other styleguides are great if you're already an Angular guru with plenty of experience, but can be extremely difficult for students new to Angular, and with varying levels of JS knowledge to understand.  When we teach we generally increase complexity over time.  This guide aims to set rules so that we teach proper Angular with a common syntax, while slowly introducing additional syntactical complexity. 

tldr; This style-guide is aimed at students new to Angular, not angular professionals.

## Immediate Guidelines:
These guidelines are suggested for all code given to students.  

### prefix data- on attributes and directives

Use `data-` prefixed attributes instead of raw angular attributes/directives.  These pass HTML validators.

Avoid:
```html
 <div ng-controller="MainCtrl">
```
Recommended:
```html
 <div data-ng-controller="MainCtrl">
```

### controller as syntax

Use Controller as syntax, which promotes the use of dot syntax in HTML to indicate where variables come from.  This also means it is possible to safely use scalars on the controller.  You must also avoid the use of `$scope` and use `this` instead in your controllers.

Avoid:
```html
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

### define named functions for each component 
Declare named functions for controllers and other components. 

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

### use dot chaining to build the app rather than repetition of an app variable
In general multi-line dot-chaining is more prone to error, but since we're also avoiding in-line call-backs, the issue should be greatly reduced and overall readability should remain high.  This also follows what other style-guides suggest. 

Avoid:
```js
var app = angular.module('app', []);
app.controller('MainCtrl', function() {
});
app.factory('SomeFactory', function() {
});
```

Recommended:
```js
angular
  .module('app', [])
  .controller('MainCtrl', MainCtrl)
  .factory('SomeFactory', SomeFactory);
```



### Factories vs. services

Use Factories.  
This conforms with other styleguides.  

> It should be noted that Services are closer to the way we teach controllers and might therefore be easier for students.  An argument could be made for flipping this rule as long as it's done consistently.  

Service Pattern - Avoid:

```js
function UserModel(){
	this.doSomething = function(){
    	//…
  	}
}
```

Factory Pattern - Prefer:
```js
function UserModel(){
	var UserCtrl = {};
	UserCtrl.doSomething = function(){
		//...
	}
 	return UserCtrl;
}
```

### When introducing minification

#### Use $inject vs. inline annotation for dependency injection

Use $inject vs. inline annotation.  

This has better readability and lower likelihood of syntax errors.  Try to keep the `$inject` call near the function it refers to.

Avoid: 
```js
angular
  .module('app')
  .controller('PhoneController', ['$location', '$routeParams', PhoneController]);

function PhoneController($location, $routeParams) {...}
```
Prefer:
```js
angular
  .module('app')
  .controller('PhoneController', PhoneController);

PhoneController.$inject = ['$location', '$routeParams'];
function PhoneController($location, $routeParams) {...}
```

> For a comparison see the [official angular tutorial](https://docs.angularjs.org/tutorial/step_05)

#### Use gulp or grunt with MEAN stack, use asset-pipeline with Rails

If you're following the above use of `$inject` ng-annotate is unnecessary.  However, you should consider using `ng-strict-di` to alert you to missing annotations.  [Reference](https://docs.angularjs.org/api/ng/directive/ngApp)

Prefer:
```js
<div ng-app="ngAppStrictDemo" ng-strict-di>
```




# Introduce later


#### mention (but don't use) $scope in controllers

Since we're using controller-as and `this` in our controllers, `$scope` will only rarely be used.  However, students are going to come across blogs, older code and stackoverflow posts that use `$scope` frequently.  We should mention how this works, at least in writing, but not right away. 

> Note: when using $scope one should always pass objects, not scalars.
> Use `$scope.obj = {}` rather than `$scope.foo = 'adsf'`
