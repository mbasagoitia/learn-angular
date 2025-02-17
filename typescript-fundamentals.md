# Typescript Fundamentals

Superset of JS. Includes additional features not included by most browers, so must be transpiled to JS at runtime.

Benefits:

- Strong/static typing that is optional
- Object-oriented features (classes, interfaces, constructors, access modifiers, fills, properties, generics)
- Compile-time errors
- Access to more tools

## How to Install TS

- sudo npm install -g typescript
- check installation with tsc --version

## Compile TS to JS

- tsc <filename.ts>
- Whenever you call ng serve, this process is done under the hood by angular

## Types

- number (includes integers and floating point numbers)
- boolean
- string
- any
- arrays, which are declared as the type of data being stored, such as number[] or string[] or any[]
- enum, which organizes related constants
    - ex. enum Color { Red, Green, Blue }; <- each entry implicitly has an integer value starting from 0. It is a good idea to set these manually, but you don't have to. For example, enum Color { Red = 0, Green = 1, Blue = 2 }
    - let backgroundColor = Color.Red

- Types are inferred based on initialization, and will throw an error if you try to reassign to a different type
- If a variable is not assigned a value at initialization, type is any. It will not throw an error if you later assign it a value, then assign another value of a different type. Use type annotations when doing this!
    - let a: number;

## Type Assertions

If we have declared a variable without an explicit type (intialized but not assigned it), we can assert the type when we use it later to get intellisense suggestions by including the type in <> before the name of the variable or use as keyword. Note that this type assertion does not change the type of the variable at runtime and doesn't restructure the object in memory.

    - let message;
    - message = "abc"
    - let endsWithC = (<string>message).endsWith("c")
    - let alternativeWay = (message as string).endsWith("c")

## Arrow Functions

let logMessage = (message) => console.log(message)

## Custom Types

Sometimes we may need to pass an object to a function that is expecting certain values to be in the object, such as { x: 1, y: 2 }. If that object contains different types, no error will be thrown. We have several options.

- Inline annotation: let drawPoint = (point: { x: number, y: number }) => {
    // algorithm to draw point
}
    - This works fine for simple use cases but is more verbose

- Interfaces--we define the structure of an object. Enhances reusability across functions.

    - interface Point {
        x: number,
        y: number
    }

    - let drawPoint = (point: Point) => {
        // algorithm
    }

## Classes

Groups variables (properties) and functions (methods) that are highly related. Helps with cohesion principle. We can include the implementation of methods in the class, whereas we only include the function signature/description in interfaces.

class Point {
    private _x: number;
    private _y: number;

    constructor(x?: number, y?: number) { <- you can add the question mark to indicate that parameters are optional
        this._x = x;
        this._y = y;
    }

    draw() {
        // console.log(this.x + ", " + this.y) <- remember to use the this keyword when referring to properties on the object
    }

    getDistance(another: Point) {
        // ...
    }
}

When defining an object of a custom type, we need to explicitly allocate memory to it. We do this by initializing the object with the new Class() method.

### Creating objects and calling methods

let point: Point = new Point(); <- TS can infer this is a point object, so this can be written as let point = new Point();

let point = new Point(1, 2) <- x and y are assigned from constructor
point.draw()
point.getDistance()

### Constructor Method

Method that (usually) has parameters and is called at initialization. You can only have one constructor in TS.

To prevent fields and methods from being changed after initialization (such as point.x = 4), we can use **access modifiers,** which can be applied to members of a class to control its access from the outside.

Access modifiers include:

- private
- public
- protected

By default, all members are public. You will not be able to access or modify private members from outside the class.

A simpler way to define and assign the constructor is to include access modifiers in the declaration and omit the assignment of this.member:

constructor(private _x?: number, public _y?: number) {

}

Note that you need to include the public keyword if you define the constructor this way.

### Setters and Getters

If you need to be able to see the private members of a class (but not modify them), it is best to define a method in the class (which has access to private members) such as:

getX() {
    return this._x;
}

If we want users to be able to change the value of private members of a class, we should define a setter method that can be called instead of directly modifying the member directly:

setX(value) {
    this._x = value;
}

Setter methods are useful because it also allows us to have validation and checks before changing the value.

A cleaner syntax to use getter and setter methods is to use the "get" and "set" keywords, such as:

get x() {
    //...
}

set x(value) {
    //...
}

and now we can access these getter and setter methods with point.x and point.x = 10. This calls the getter and setter methods under the hood with a cleaner syntax.

Note: we prefix the existing field with an underscore so it doesn't clash with the naming of the getters and setters: _x and _y

### Property vs Field

A property looks like a field from the outside, but internally it is a method in the class; usually a getter and/or setter.

# Modules

It is highly likely that in real programs, we will not write all of the code in one file, like main.ts. We want to modularize our code by separating it into different modules/files.

## Exporting and Importing Modules

To make a module accessible in other files, add the export keyword before the name of the class:

export class Point {
    // class definition...
}

To import a module for use in another file, add a line at the top of the file:

import { Point } from './module-name' <- relative path to module