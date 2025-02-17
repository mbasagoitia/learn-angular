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
    x: number;
    y: number;

    draw() {
        // ...
    }

    getDistance(another: Point) {
        // ...
    }
}