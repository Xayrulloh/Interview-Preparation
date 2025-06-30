# Nest.js Interview Questions

1. ## **How does the architecture of a Nest.js application differ from other Node.js frameworks like Express.js?**

   Nest.js is a popular Node.js framework that uses modern JavaScript and
   TypeScript features to build scalable and efficient applications. The
   architecture of a Nest.js application is based on the principles of the
   Model-View-Controller (MVC)
   [design pattern](https://anywhere.epam.com/en/blog/less-popular-javascript-design-patterns)
   and draws inspiration from Angular's architecture. Here's an overview of the
   architecture of a Nest.js application:

   - **Modules**: The application is divided into multiple modules, each
     responsible for a specific set of features. Each module contains its own
     set of controllers, services, and providers.

   - **Controllers**: Controllers are responsible for handling incoming HTTP
     requests and returning the appropriate HTTP responses. Controllers are
     linked to a specific route and can have multiple endpoints.

   - **Services**: Services are responsible for performing business logic and
     interacting with the data layer. Services can be shared across multiple
     modules and can have dependencies injected using the built-in dependency
     injection system.

   - **Providers**: Providers are a type of service that can be instantiated
     multiple times within a module. Providers can be used to create custom
     classes, factories, or utilities that can be used across the application.

   - **Middleware**: Nest.js supports middleware, which are functions that are
     executed before or after a request is handled by a controller. Middleware
     can be used to perform operations like logging, authentication, or error
     handling.

   Nest.js also includes built-in support for features like dependency
   injection, middleware, and WebSocket support, which can help simplify
   application development. Additionally, Nest.js integrates well with other
   popular Node.js libraries like TypeORM and GraphQL, making it a popular
   choice for building scalable web applications.

2. ## **How do you ensure that your Nest.js applications are scalable and maintainable? What techniques or best practices do you follow?**

   **Use modular architecture**: Nest.js encourages a modular architecture that
   separates different parts of the application into modules. Each module should
   have a clear and specific responsibility, and modules can be easily added or
   removed as needed. This makes the application more scalable and easier to
   maintain.

   **Dependency injection**: Nest.js uses dependency injection, which makes it
   easy to write testable and maintainable code. By using dependency injection,
   you can easily replace dependencies with mock objects during testing, and you
   can change the behavior of the application without changing the code.

   **Use pipes and filters**: Pipes and filters are powerful tools in Nest.js
   that allow you to validate and transform data as it moves through the
   application. By using pipes and filters, you can ensure that data is valid
   and consistent, which makes the application more scalable and maintainable.

   **Use Interceptors**: Interceptors are middleware functions that can be used
   to modify the behavior of HTTP requests and responses. By using interceptors,
   you can add common functionality, such as logging or error handling, to the
   application without duplicating code.

   **Use guards:** Guards are middleware functions that can be used to control
   access to resources in the application. By using guards, you can ensure that
   only authorized users can access sensitive data or perform certain actions.

   **Use async/await:** Nest.js makes heavy use of async/await, which allows you
   to write asynchronous code in a synchronous style. This makes the code easier
   to read and maintain, and it allows you to write scalable applications that
   can handle large amounts of traffic.

   **Use Swagger/OpenAP**I: Nest.js integrates easily with Swagger/OpenAPI,
   which is a tool for documenting and testing APIs. By using Swagger/OpenAPI,
   you can ensure that your API is well-documented, which makes it easier for
   developers to use, and it allows you to test your API automatically.

   **Use TypeScript**: Nest.js is written in TypeScript, which is a superset of
   JavaScript that adds static typing and other features to the language. By
   using TypeScript, you can catch errors at compile-time rather than run-time,
   which makes the code more robust and easier to maintain.

3. ## **Can you describe the role of modules in a Nest.js project?**

   In Nest.js, modules are a fundamental building block of the application
   architecture. Modules help to organize and structure the codebase into
   smaller, more manageable units, which can be developed, tested, and deployed
   independently.

   A module can be seen as a container for a specific feature or domain of the
   application. Each module can have its own controllers, services, providers,
   and other related components, which are encapsulated within the module's
   scope.

   Modules can also be used to define the dependencies and relationships between
   different parts of the application. For example, a module can import other
   modules to access their functionality or export its own functionality for use
   by other modules.

   Some of the key roles of modules in Nest.js include:

   - **Encapsulation**: Modules encapsulate related functionality, making it
     easier to reason about and maintain the codebase.
   - **Dependency management**: Modules define the dependencies of a feature or
     domain, ensuring that the necessary components are available and properly
     configured.
   - **Reusability**: Modules can be reused in other applications or projects,
     providing a modular and reusable architecture.
   - **Testability**: Modules can be tested in isolation, allowing for easier
     and more thorough testing of individual features or domains.

   Overall, modules provide a powerful mechanism for structuring and organizing
   the codebase in a modular and maintainable way, which is essential for
   developing robust and scalable applications.

4. ## **What is dependency injection ?**

   Dependency Injection (DI) in NestJS is a core concept that allows you to
   manage dependencies efficiently. It uses the built-in **NestJS IoC (Inversion
   of Control) container** to inject dependencies wherever needed. NestJS
   follows a **modular approach** and leverages TypeScript decorators like
   @Injectable(), @Inject(), and @Module() to facilitate DI.

   Here's how Dependency Injection works in Nest.js:

   - **IoC Container:**  
     \- Nest.js has an IoC container that manages the instantiation and
     injection of dependencies  
     \- The container maintains a registry of providers, which are classes or
     values that can be injected into other components.

   - **Providers:**  
     \- A provider is a class or a value that Nest.js can inject into other
     components.  
     \- Providers are decorated with @Injectable() to indicate that they can be
     injected.

     ```ts
     import { Injectable } from '@nestjs/common'

     @Injectable()
     export class MyService {
       // Service implementation
     }
     ```

   - **Injection**:  
     \- Dependencies are injected into components through their constructors.  
     \- Use the @Inject() decorator or rely on TypeScript's type system for
     automatic injection.

     ```ts
     import { Injectable, Inject } from '@nestjs/common'
     import { MyService } from './my.service'

     @Injectable()
     export class MyController {
       constructor(private readonly myService: MyService) {}

       // Controller logic using myService
     }
     ```

   - **Scope:**  
     \- Providers can have different scopes, such as SINGLETON, REQUEST, or
     TRANSIENT.  
     \- The default scope is SINGLETON, meaning a single instance is created and
     shared across the entire application.

     ```ts
     import { Injectable, Scope } from '@nestjs/common'

     @Injectable({ scope: Scope.REQUEST })
     export class MyRequestScopedService {
       // Service implementation
     }
     ```

   - **Modules:**  
      \- Nest.js applications are organized into modules.  
      \- Modules define the context for the IoC container, and dependencies are
     usually scoped to a specific module.

     ```ts
     import { Module } from '@nestjs/common';
     import { MyController } from './my-controller';
     import ( MyService } from './my-service';

     @Module({
      controllers: [MyController],
      providers: [MyService],
     })
     export class MyModule {}
     ```

   By embracing Dependency Injection, Nest.js encourages a modular and scalable
   architecture. It simplifies testing, promotes code reusability, and makes it
   easier to manage and maintain large codebases. The framework's IoC container
   automates the process of creating and wiring up dependencies, allowing
   developers to focus on building features rather than managing object
   lifetimes and dependencies manually.

5. ## **What is provider?**

   A provider is a term used to describe a class or a value that Nest.js can
   inject into other components (such as controllers, services, or other
   providers). Providers are a fundamental concept in the Nest.js dependency
   injection system.

6. ## **What are decorators in Nest.js?**

   In Nest.js, decorators are a way to enhance or modify the behavior of
   classes, class members (properties and methods), and parameters. Decorators
   are a feature of TypeScript and are widely used in Nest.js to define various
   metadata and configurations for different parts of the application.

   Here are some common use cases of decorators in Nest.js:

   - **Class Decorators:**  
     \- Class decorators are applied to class declarations. They can be used to
     modify the behavior or add metadata to a class.  
     \- Example: @Module, @Controller, @Injectable

     ```ts
     @Module({
       controllers: [AppController],
       providers: [AppService]
     })
     export class AppModule {}
     ```

   - **Method Decorators:**  
     \- Method decorators are applied to methods within a class. They are often
     used to modify the behavior of route handlers in controllers.  
     \- Example: @Get, @Post, @Patch

   - **Property Decorators:**  
     \- Property decorators are applied to properties of a class. They are
     commonly used to define dependency injection tokens for properties.  
     \- Example: @Inject, @Optional

     ```ts
     @Injectable()
     export class MyService {
       @Inject('MY_TOKEN' ) private readonly myToken: string:
     }
     ```

   - **Parameter Decorators:**  
     \- Parameter decorators are applied to parameters of a method or
     constructor. They can be used to define metadata for dependency
     injection.  
     \- Example: @Req, @Body

     ```ts
     @Controller('cats')
     export class CatsController {
       @Post()
       create(@Body() createCatDto: CreateCatDto) {
         return 'This action adds a new cat'
       }
     }
     ```

   - **Custom Decorators:**  
     \- Developers can create custom decorators to encapsulate common patterns
     or behaviors. Custom decorators are functions that return another function,
     which is the actual decorator applied to the target.

     ```ts
     function MyCustomDecorator() {
       return function (target: any, propertyKey: string) {
         // Custom logic here
       }
     }
     class MyClass {
       @MyCustomDecorator()
       myProperty: string
     }
     ```

   Decorators in Nest.js play a crucial role in simplifying the configuration,
   metadata management, and behavior customization within the framework. They
   contribute to the overall readability and maintainability of Nest.js
   applications.

7. ## **What are DTOs (Data Transfer Objects) in Nest.js**

   DTOs are used to define the shape of data sent and received by APIs, helping
   to validate and document data structure

8. ## **Explain the concept of Exception Filters in Nest.js**

   Exception Filters are used to handle exceptions and transform them into
   meaningful error responses, they can be globally using exception filters or
   at the route level using the @UseFilters decorator

9. ## **Explain the concept of Pipes in Nest.js**

   Pipes are used for data transformation and validation before it reaches the
   route handler

10. ## **What are pipes and filters?**

    **Pipes:**  
     Pipes in Nest.js are a way to transform input data before it reaches the route
    handler or after it leaves the route handler. They are used to validate and transform
    data. Pipes can be applied to parameters at the controller level, method level,
    or globally.  
     There are several built-in pipes in Nest.js, and you can also create custom
    pipes. Examples of built-in pipes include:

    **ValidationPipe** \- Automatically performs validation on incoming request
    payloads using validation decorators.

    **ParseIntPipe** \- Converts a string to an integer

    **ParseBoolPipe** \- Converts a string to a boolean

    **Filters:**  
     Filters in Nest.js are used to handle exceptions globally. When an unhandled
    exception occurs during the execution of a route handler, filters can be used
    to customize the response that is sent back to the client. Filters are applied
    at the global level or can be scoped to specific controllers or routes.

    There are a few types of filters in Nest.js, including exception filters,
    which handle unhandled exceptions.

    ```ts
    import { Catch, ExceptionFilter, ArgumentsHost } from '@nestjs/common'

    @Catch(MyException)
    export class MyExceptionFilter implements ExceptionFilter {
      catch(exception: MyException, host: ArgumentsHost) {
        const response = host.switchToHttp().getResponse()
        response.status(500).json({
          statusCode: 500,
          message: 'Something went wrong'
        })
      }
    }
    ```

11. ## **Explain the role of Guards in Nest.js**
    Guards are used to control access to routes and protect them from
    unauthorized access
12. ## **What is the purpose of the Nest.js Guards and Pipes combination and how does it enhance the request processing flow**
    Combining Guards and Pipes allows you to perform authorization and data
    validation in a structured and sequential manner in the request processing
    flow
13. ## **What is Middleware in Nest.js**
    Middleware functions in Nest.js are used to process requests before they
    reach the route handler
14. ## **What is the purpose of Interceptors in Nest.js**

    In Nest.js, an interceptor is a middleware that can intercept incoming
    requests and outgoing responses. Interceptors provide a way to modify the
    request or response objects, execute additional logic, or even terminate the
    request/response cycle prematurely.

    Interceptors can be used to implement cross-cutting concerns, such as
    authentication, logging, error handling, and caching. They are registered
    globally, per module, or per controller and can be synchronous or
    asynchronous.

15. ## **Explain Nest.js lifecycle request**
    1\. Request Received  
    2\. Routing  
    3\. Middleware Execution  
    4\. Guards Execution  
    5\. Interceptors Execution  
    6\. Pipes Execution  
    7\. Controller Execution  
    8\. Response Interceptors  
    9\. Exception Filters  
    10\. Response Sent  
    11\. Request End  
    The NestJs request lifecycle adds additional layers like Guards,
    Interceptors, Pipes and Exception Filters on top of the basic middleware and
    routing mechanisms inherited from Express.js. These layers provide a more
    modular and structured approach to handling requests, making it easier to
    implement cross-cutting concerns like validation, transformation, and error
    handling
