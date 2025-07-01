# TypeScript Interview Questions

## Fundamentals
1. ### **What is TypeScript?**  
   *TypeScript is a superset of JavaScript that adds static typing to the language. It is an open-source programming language developed and maintained by Microsoft. TypeScript is designed for large-scale JavaScript application development, providing developers with tools to write more reliable and maintainable code*

2. ### **What are the differences between JavaScript and TypeScript?**  
   ![Js and Ts difference](./images/js-ts-diff.png)

3. ### **What are the advantages of TypeScript over JavaScript?**  
   *Below are some of the advantages of typescript over javascript*
   - TypeScript is able to find compile time errors at the development time only
   - TypeScript is strongly-typed or supports static typing
   - TypeScript compilers can compile the .ts files into ES3,ES4 and ES5

## Basic Types
4. ### **What are the primitive types in TypeScript?**  
    - **Built-in types:** String
        - Number
        - Boolean
        - Null
        - Undefined
        - Any
        - Void
        - Symbol  
    - **User-defined types:** Arrays
        - Enums
        - Classes
        - Interfaces

5. ### **What is the difference between never, unknown, and any?**  
    - **never:**  
        - Represents values that never occur  
        - Used for functions that always throw or never return  
        - **Example:**
            ```ts
            function throwError(message: string = 'What the hell is going on?'): never {
                throw new Error(message)
            }
            ```

    - **unknown:**  
        - Represents values we know nothing about  
        - Requires type checking before use  
        - **Example:**
            ```ts
            let userInput: unknown

            // Type assertion
            let userName: string = userInput as string

            // Type checking
            if (typeof userInput === 'string') {
                userName = userInput
            }
            ```

    - **any:**  
        - Opts out of type checking  
        - Used for dynamic content or migration  
        - **Example:**
            ```ts
            let myValue: any = 42

            // No type checking is performed
            let result: string = myValue // No error at compile-time
            ```

## Variables & Functions
6. ### **What are the different keywords to declare variables in TypeScript?**  
   *Like JavaScript, TypeScript has var, let, const*

7. ### **Explain the arrow function syntax in TypeScript.**  
   *It's a short way to create a function*

8. ### **Provide the syntax of a function with the type annotations.**  
   *Functions are blocks of code to perform a specific code. Functions can optionally take one or more arguments, process them, and optionally return a value*

   **Example:**
   ```ts
    // primitives
    let userName: string = "Alice";
    let userAge: number = 30;
    let isActive: boolean = true;

    // arrays
    let numbers: number[] = [1, 2, 3, 4, 5]; // Array of numbers
    let names: string[] = ["John", "Jane", "Peter"]; // Array of strings

    // objects
    let person: { name: string; age: number; city?: string } = {
        name: "Bob",
        age: 25,
    };

    // etc...
   ```

9. ### **What are anonymous functions? Provide their syntax in TypeScript**  
   *An anonymous function in TypeScript is a function defined without a name. These functions are often used inline, as arguments to other functions (callbacks), or assigned to variables*

   **Example:**
   ```ts
    // function assigned to add is anonymous
    const add = function (a: number, b: number): number {
        return a + b;
    };

    console.log(add(5, 3)); // Output: 8
   ```

10. ### **What are the rest parameters and arguments in TypeScript?**  
    *Rest parameters allows a function to take all arguments as one array*

    **Example:**
    ```ts
    function restF(...args: number[]) {
        return args.join('')
    }
    ```

11. ### **What is parameter destructuring?**  
    *It's a way to unpack the object provided as an argument to function*

    **Example:**
    ```ts
    const {name, age} = {name: 'deeng', age: 1} // in objects
    const [first, second, ...others] = [1, 2, 3, 4, 5, 6] // in array
    ```

12. ### **Provide the TypeScript syntax to create function overloads.**  
    *It allows us to create multiple functions with the same name but different arguments. Typescript itself defines by argument*

    **Example:**
    ```ts
    // Overload signatures
    function combine(a: number, b: number): number;
    function combine(a: string, b: string): string;

    // Implementation signature (must be compatible with all overloads)
    function combine(a: any, b: any): any {
    if (typeof a === 'number' && typeof b === 'number') {
        return a + b; // Performs addition for numbers
    } else if (typeof a === 'string' && typeof b === 'string') {
        return a + b; // Performs concatenation for strings
    }
    throw new Error("Invalid arguments: 'combine' expects either two numbers or two strings.");
    }

    // Usage examples
    console.log(combine(5, 10)); // Output: 15 (number)
    console.log(combine("Hello, ", "World!")); // Output: "Hello, World!" (string)

    // This would result in a TypeScript error:
    // combine(5, "World!"); // Argument of type 'string' is not assignable to parameter of type 'number'.
    ```

## Objects & Interfaces
13. ### **How to create objects in TypeScript?**  
    *Objects are collections of keys and values. And the keys must be unique. It's the same as Js to create obj in Ts*

14. ### **How to specify optional properties in TypeScript?**  
    *By using ? after the property name we can specify it as optional*

15. ### **What is an interface in TypeScript, and how is it different from a class?**  
    *In TypeScript, an interface serves as a blueprint for defining how an object should look. It outlines the properties an object should have and their respective types but doesn't include any actual code*

    **Example:**
    ```ts
    interface Person {
        name: string
        age: number
    }

    const me: Person = {
        name: 'Me',
        age: 1
    }

    // the Person interface helps us define what properties a ramu object should have – in this case, a name of type string and an age of type number
    ```

16. ### **What is the difference between type and interface?**  
    *Both type and interface are used to define custom types, but there are subtle differences in their capabilities and use cases*

    - **Declaration Syntax:**
        - **Interface:** *Interfaces are typically used to define object shapes. They can describe the structure of objects, including properties, methods, and index signatures*
        ```ts
        interface Person {
            name: string
            age: number
        }
        ```
        - **Type:** *The type keyword is more versatile. It can be used to define object types, union types, intersection types, and more*
        ```ts
        type Person = {
            name: string
            age: number
        }
        ```

    - **Extending and Implementing:**
        - **Interface:** *Interfaces can extend other interfaces using the extends keyword. They are also used for class implementation*
        ```ts
        interface Animal {
            legs: number
        }

        interface Dog implements Animal {
            breed: string
        }
        ```
        - **Type:** *The type keyword can be used for creating union types, intersection types, and mapped types. However, it cannot be extended or implemented like interfaces*
        ```ts
        type Animal = {
            legs: number
        }
        type Dog = Animal & {
            breed: string
        }
        ```
    
    - **Declaration Merging:**
        - **Interface:** *Interfaces support declaration merging, which allows multiple interface declarations with the same name to be merged into a single declaration*
        ```ts
        interface Car {
            model: string
        }
        interface Car {
            brand: string
        }
        // Merged interface
        // {model: string, brand: string}
        ```
        - **Type:** *The type keyword does not support declaration merging. If you try to declare two types with the same name, it will result in an error*
        ```ts
        type Car = {
            model: string
        }

        // Error: Duplicate identifier
        type Car = {
            brand: string
        }

        ```

    - **Immutability:**
        - **Interface:** *Interfaces are open to extension, meaning you can add new properties when extending an interface*
        ```ts
        interface Person {
            name: string
            age: number
        }

        // Extending the interface
        interface PersonWithAddress extends Person {
            address: string
        }
        ```
        - **Type:** *The type keyword supports mapped types, allowing the creation of new types based on existing ones. However, it is generally considered more closed to modification*
        ```ts
        type Person = {
            name: string
            age: number
        }

        // Creating a new type based on an existing type
        type PersonWithAddress = Person & {
            address: string
        }
        ```

    - **Choosing Between type and interface:**
        - **Interface:**
            - *Defining object shapes, especially for objects that represent instances of a class*
            - *Extending other interfaces or implementing classes*
        - **Type:**
            - *Defining union types, intersection types, or creating complex types that involve mapped types*
            - *Expressing types that cannot be represented using interfaces*
        - *In practice, the choice between type and interface often comes down to personal or team preferences. Some developers prefer the clarity and convention of using interfaces for object shapes, while others appreciate the flexibility and versatility provided by the type keyword. Both type and interface are powerful tools in TypeScript, and you can choose the one that best fits your use case*


17. ### **Declaration merging?**  
   * Declaration merging is a feature in TypeScript that allows you to combine multiple declarations of the same name into a single definition. This is particularly useful with interface (but not with type)*

## Classes & OOP
18. ### **Explain the TypeScript class syntax.**  
    *It's same as JavaScript*

19. ### **What are abstract classes? When should you use one?**  
    *Abstract classes are similar to interfaces in that they specify a contract for the objects, and you cannot instantiate them directly*

20. ### **How to make object properties immutable in TypeScript?**  
    *By using **readonly** keyword before the property name*

21. ### **What are the **'implements'** clauses in TypeScript?**  
    *It's used to check that a class satisfies the contract specified by an interface*

22. ### **Explain the concept of inheritance in TypeScript.**  
    *It allows us to extend from another class and reuse or modify the behavior*

<!-- FIXME should continue from here -->

## Advanced Types
23. **What are Union and Intersection Types?**  
    In TypeScript, union types, marked by |, allow a variable to have values from different types.  
    Intersection types, shown by &, bring together multiple types to form a new type with all properties.

24. **What are type aliases? How do you create one?**  
    If we've variable either string or number. We can create type something string | number and use this type to that variable

25. **What are string literal types?**  
    You can refer to specific string or numbers as types

26. **What are template literal types?**  
    They're like string literal but you can combine them with concrete

27. **What are Conditional Types?**  
    Conditional types in TypeScript help us describe different type mappings based on certain conditions.

28. **What are mapped types, and how do they work?**  
    Mapped types in TypeScript allow you to create new types by changing the properties of existing ones.

29. **List some of the utility types provided by TypeScript and explain their usage.**  
    Partial, Required, Readonly, Record, Promise, Awaited etc...

## Special Types
30. **What is void, and when to use the void type?**  
    Let's say you've a function which returns nothing, that means it's void function

31. **Explain the concept of null and its use in TypeScript.**  
    Null value indicates an absence of value, hence you cannot access any properties on the variable or call a method on it. It's more like it's nothing

32. **What is undefined in TypeScript?**  
    When a variable is declared without initialization it becomes undefined

## Arrays & Tuples
33. **Explain how the arrays work in TypeScript.**  
    We use arrays to store values of the same type. Arrays are ordered and indexed collections of values.

34. **Explain how tuple destructuring works in TypeScript.**  
    Instead of giving one type to array elements we can separate them one by one, this is why we need tuples. And it's works pretty easy like destructuring

## Enums
35. **What is enums?**  
    In TypeScript, enums work similarly to enums in other programming languages, providing a way to define a set of named constants.

## Modern Features
36. **What is optional chaining?**  
    Instead of checking all the way down we can just use a ?. And it returns undefined it's not exist

37. **What is the 'in' operator?**  
    It's used to find if a property is in the specified object

38. **What are TypeScript decorators, and how do they work?**  
    TypeScript decorators are special functions used to modify or add behavior to classes, methods, properties, or parameters at runtime.

## Configuration
39. **What is the purpose of the tsconfig.json file?**  
    It provides the compiler options to compile the project

40. **How to enforce strict null checks in TypeScript?**  
    It's a way to check all possibilities that can be null. And to enforce it we change tsconfig.json file strictNullChecks to true

## Type System
41. **What is meant by type inference?**  
    When you don't provide an explicit type typescript itself defines type

42. **What is meant by contextual typing?**  
    When the typescript compiler uses the location of a variable to infer its type, it's called contextual typing

43. **What is the typeof operator? How is it used in TypeScript?**  
    Like JavaScript, typeof identifies type of value and it's used for it

44. **When would you use type assertion?**  
    Type assertion in TypeScript is a mechanism to tell the compiler that you know more about the type of a value than TypeScript can infer.

## Advanced Concepts
45. **Does TypeScript support static classes? If not, why?**  
    In Typescript you can create any data and functions as simple objects without creating a containing class. Hence typescript doesn't need static classes.

46. **What is the Function type in TypeScript?**  
    Function is a global type in typescript and it has properties like bind, call and apply with other properties.

47. **What is a type declaration file?**  
    It's a file which ends with .d.ts extension providing a way to declare the existence of some types or values without actually providing implementations for those values

48. **Explain the various ways to control member visibility in TypeScript.**  
    public: You can access a public member anywhere outside the class  
    protected: It's visible only to the subclasses  
    private: It's only visible inside the class

49. **What are Type Guards?**  
    **typeof:** check primitive types  
    **keyof:** check is key available in object  
    **instanceof:** check class instances  
    **in:** check if a property exist in an object  
    **is:** User Defined Type Guard

50. **Explain how TypeScript infers types?**  
    TypeScript uses type inference to automatically determine the types of variables based on their assigned values while declaring.

51. **What are generics in TypeScript, and when would you use them?**  
    Generics in TypeScript provide a way to create reusable components and functions while maintaining flexibility in the types they work with.

52. **What is the declare keyword?**  
    The declare keyword in TypeScript is used to inform the compiler that a variable, method, or library is defined externally.

## Enums vs Types
53. **Enums vs type declaration (type and interface)**  
    Enum exists in JS but type declaration erased and used only for TS checks

## Loops
54. **Explain the different variants of the for loop in TypeScript.**  
    for, for in, for of, forEach

## Symbols
55. **Explain the symbol type in TypeScript.**  
    The way to create unique primitive type value