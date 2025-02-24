# Components

3 steps to use a component:

1. Create a component
2. Register it in a module
3. Add an element in HTML markup

## Creating a Component

Naming convention for components: component-name.component.ts

Start by creating a TypeScript class and add the component decorator to mark it as an Angular component. Pass an object of properties to the function to tell Angular how the component works (such as css selectors, html template to render, templateUrl (external template), styleUrls, etc.)

import { Component } from 'angular/core'

@Component({
    selector: 'courses',
    template: '<h2>Courses</h2>'
})
export class CoursesComponent {

}

## Registering a Component in a Module

Import the component and include it in the module you are using it in by adding its name to the **declarations** array in the module's decorator.

## Add an element in HTML markup

Anywhere you have an element with the selector name you assigned, Angular will render the html template you provided. You can use your custom html element as <courses></courses>

You can add this component in an html file like app.component.html

# Using Angular CLI to Generate Components

command: ng g c <component-name>

- This generates the directory with the component name and ts, css, html, and spec.ts files with boilerplate code inside of it. It also updates app.module and registers the component.