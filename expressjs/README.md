#           Express.js Interview Questions

1) ### [**What is Express.Js?**](https://www.geeksforgeeks.org/introduction-to-express/)
    Express is a small framework that sits on top of Node.js’s web server functionality to simplify its APIs and add helpful new features. It makes it easier to organize your application’s functionality with middleware and routing; it adds helpful utilities to Node.js’s HTTP objects; it facilities the rendering of dynamic HTTP objects

2) ### **Why use Express.Js?**
    Its simplicity, minimalism, flexibility and scalability characteristics. It provides easy to set up for middlewares and routing

3) ### **Mention a few features of Express.js.**
    Routing, Middleware, HTTP Utility Methods, Static File Serving, Security

4) ### [**Explain the structure of an Express JS application?**](https://www.geeksforgeeks.org/how-to-structure-my-application-in-express-js/)
    * **Entry point:** It’s a starting point of the application where you set up your server, connect to your database, add middleware, and define the main routes
    * **Routes directory:** It contains files for the app’s routes
    * **Controllers directory:** It contains files that define the logic to handle requests for a specific route
    * **Models directory:** It used for creating the schema models for the different data
    * **Middleware directory:** It contains custom middleware functions that you can use in your routes
    * **Views directory:** It contains your view templates
    * **Public directory:** It contains static files that are served directly by the server such as images, css files, and javascript files

5) ### [**Why should you separate the Express app and server?**](https://www.geeksforgeeks.org/why-express-app-and-server-files-kept-separately/)
    The server is responsible for initializing the routes, middleware, and other application logic whereas the app has all the business logic that will be served by the routes initiated by the server. This provides the modularity and flexibility and makes the codebase more easier to maintain and test.

6) ### **Define the concept of the test pyramid.**
    The Test Pyramid consist of three levels:
    * Unit Tests
    * Integration Tests
    * and End-toEnd (E2E) Tests

7) ### [**Explain what CORS is in Express JS?**](https://www.geeksforgeeks.org/how-to-allow-cors-in-express/)
    CORS refers to a middleware that enables Cross Origin Resource Sharing for your application. This allows the application to control which domains can access your resources by setting HTTP headers

8) **What is middleware?**  
    Middleware comes in between your request and business logic. It is mainly used for logs, rate limit, routing, authentication etc.. There are also third-party middleware such as body-parser etc...

9) ### **What are the types of middleware?**
    There are five types of Middleware in Express.js
    * Application level
    * Router level
    * Error handling
    * Built-in
    * Third party

10) ### [**How can you deal with error handling in Express.js?**](https://www.geeksforgeeks.org/explain-error-handling-in-express-js-using-an-example/)
    When an error occurs, you can pass it to the next middleware or route handler using the next() function. You can also add an error handling middleware to your application that will be executed whenever an error occurs

11) **Explain Express.js life cycle?**  
    1\. Request Received  
    2\. Routing  
    3\. Middleware  
    4\. Route Handler Execution  
    5\. Response Sent  
    6\. Error Handling  
    7\. Request End  

    The request lifecycle in Express.js is a structured flow from the request being received, through routing and middleware, to finally sending a response. Middleware plays a crucial role in controlling this flow, and error handling ensures that unexpected issues are managed gracefully  