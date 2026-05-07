# Lab #004 - REST API with Middleware

Create a "TODO" REST API service using Express. We'll skip the database layer for now and just log the model logic to the console

## Requirements

1. Create an Express project
2. Create the standard REST endpoints for a "TODO" application to :
   1. Get a list of todo items
   2. Get a single todo item by ID
   3. Create a new todo
   4. Update an existing todo item (full replace)
   5. Partially update an existing todo item (patch)
   6. Delete a todo item
3. Your URLs/routes **must** adhere to the naming structure we discussed in class.  EG: `/api/v1/todos`
4. Use the controller -> service -> repository approach to structure your project.
5. In your service layer, add a unique ID to the document when new items are created.
6. Support a "color" property for your todo items. The rest of the properties are unimportant but create at least three properties that make sense.
7. Add a middleware that will inspect the "color" property and automatically add a "hexColor" property to a todo item when it is being created. Since there are many hex color values, just support the following to keep things simple (you can hardcode this translation in the middleware) :
   1. red - #ff0000
   2. green - #00ff00
   3. blue - #0000ff
8. Add an error handler middleware that will catch all unhandled errors in your application and : 
   1. Return an appropriate HTTP status code
   2. Return a JSON response body with a friendly error message (not a stacktrace)
9. In your repository, print the todo object to the console when it is provided by user input (PUT, POST, PATCH). Hard code a small array of at least three items in your repository, with appropriate properties, to simulate a database. Return this array for the "get all todos" logic and search it to return a single item for "get one todo by ID". Return a 404 if the requested ID does not exist.
10. When updating or deleting a todo item, if the provided ID does not exist in your hardcoded array of items, return a 404.
11. If a todo item is updated or deleted by a user request, it should be updated or deleted from the data in your repository.  That is, if todo item with ID `abc123` exists in your data, I should be able to delete it, and on a subsequent `GET` for ID `abc123` I would receive a `404` since it no longer exists.
12. When creating or updating a todo item, return the final document with an appropriate status code to the user (including the auto-generated ID and the hexColor property) and add it to the list of todo's assigned to your repository instance.
    1. This should have the effect of simulating a database. If you have three todo items in your list, then create a new one, on a subsequent GET call you should have four (including the newly created one). When you update a todo, a subsequent GET request should include the changes.
