# Service Portal: Angular Style Guide

## Purpose

A sensible & opinionated Angular style guide for teams using Service Portal.

*Based off of the [Angular 1 Style Guide](https://github.com/johnpapa/angular-styleguide/tree/master/a1) by [@john_papa](http://twitter.com/john_papa) and up-to-date with Angular 1.5 components.*

## Table of Contents

  1. [IIFE](#iife)
  1. [Modules](#modules)
  1. [Components](#components)
  1. [$onInit](#oninit)
  1. [One-way Binding](#one-way-binding)
  1. [Bindable Members At Top](#bindable-members-at-top)
  1. [ControllerAs Syntax](#controller-as-syntax)
  1. [Defer Logic to Services](#defer-logic-to-services)
  1. [Single Responsibility](#single-responsibility)
  1. [Named Controllers](#named-controllers)
  1. [File Naming](#file-naming)
  1. [Linting](#linting)

## IIFE

  Where possible, wrap components in an (IIFE) Immediately Invoked Function Expression. This removes variables from the global namespace, thus preventing variable collisions and providing an enclosed scope.

  ```javascript
  (function() {
    'use strict';

    function eventsService() {}

    angular
      .module('pe-timeline')
      .service('eventsService', eventsService);
  })();
  ```

  - Note: IIFE's are best applied in UI scripts.

**[Back to top](#table-of-contents)**

## Modules

  Set a module only once in it's own file.

  ```javascript
    angular.module('pe-timeline', []);
  ```

  Get instances of the module this way.

  ```javascript
    angular.module('pe-timeline');
  ```

**[Back to top](#table-of-contents)**

## Components

  Angular 1.5 brings the new .component() helper method, which allows developers to write in an Angular 2 style and make upgrading to Angular 2 an easier task. Here are the advantages from the Angular documentation:

  * simpler configuration than plain directives
  * promote sane defaults and best practices
  * optimized for component-based architecture
  * writing component directives will make it easier to upgrade to Angular 2

  ```javascript
  (function() {
    'use strict';

    var hamburgerMenu = {
      template: [
        '<button type="button" data-target="#nav-bar">',
        '<span class="sr-only">${Toggle nav}</span>',
        '<span class="icon-bar"></span>',
        '<span class="icon-bar"></span>',
        '<span class="icon-bar"></span>',
        '</button>'
      ].join('')
    };

    angular
      .module('sec-ops')
      .component('hamburgerMenu', hamburgerMenu);
  })();
  ```

**[Back to top](#table-of-contents)**

## $onInit

Angular 1.5 brings the $onInit method. This is a good place to put initialization code for your controller. From the documentation:

*Called on each controller after all the controllers on an element have been constructed and had their bindings initialized (and before the pre & post linking functions for the directives on this element).*

  ```javascript
  function TabSelectionController() {
    var c = this;

    c.$onInit = function() {
      c.selection = 1;
      c.isVisible = false;
    };
  }
  ```

  Another great use case for utilizing $onInit, is when you need a place to fire off an immediately invoked function.

  ```javascript
  c.$onInit = function() {
    activateCharts();
    setDefaults();
  };
  ```

**[Back to top](#table-of-contents)**

## One-way Binding

  Angular 1.3 delivered a new performance enhancing feature called one-time binding. From the Angular documentation:

  *One-time expressions will stop recalculating once they are stable, which happens after the first digest if the expression result is a non-undefined value.*

  ```html
  <div class="panel-heading">{{::options.title}}</div>
  ```

  The syntax can easily be applied inside an ng-repeat as well:

  ```html
  <ul>
    <li ng-repeat="user in ::c.users"></li>
  </ul>
  ```
  - Note: Be careful using one-way data-binding in areas where the data could fluctuate in the future.

**[Back to top](#table-of-contents)**

## File Naming

  Keep it simple by going lowercase with dashes. Use the feature or widget to name the file, separated by a period with the file type following it and ending with the file extension.

  Here are a list of examples.

  ```
  people-card.server.js
  people-card.module.js
  people-card.component.js
  people-card.service.js
  people-card.directive.js
  people-card.filter.js
  people-card.spec.js
  people-card.html
  people-card.scss
  ```

  Read more on the topic, from the man John Papa.

  [https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md#naming](https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md#naming)

**[Back to top](#table-of-contents)**