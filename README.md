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
