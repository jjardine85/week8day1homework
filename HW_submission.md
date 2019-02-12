### Questions

1. What is responsible for defining the routes of the `games` resource?

The `games` resource routes are defined in the `create_router.js` file in the server->helpers directory. The `create_router.js` file is imported into the `server.js` file as `createRouter`. Within the `server.js` file a connection is made to the database `games_hub` before a constant is named `gamesCollection` and assigned to the noSQL database collection named `games`. The `gamesCollection` constant is passed to the `createRouter` function as an argument and this value is stored as a new constant named `gamesRouter`. Within the `app.use` method, the specific routes are stated to be `/api/games` in addition to http verbs expressed in the `create_router.js` file.  


2. What are the the responsibilities of server.js?
`server.js` is responsible for initialising the database connection `(mongodb://localhost:27017)`, pointing to the required database `(games_hub)` and collection `(games)`, as well as stating the routes which will be used within the application. It is also responsible for initialising various pieces of middleware such as `express`, `path` and `parser`.


3. What are the responsibilities of the `gamesRouter`?
The `gamesRouter` constant is responsible for taking the appropriate action as requested by the app, creating, reading, updating or deleting information as instructed.


4. What process does the the client (front-end) use to communicate with the server?
The client interacts with the server via a save button and a delete button. A `createGame` method is present within the `GameFormView.js` file. The `createGame` method gathers all data from the input and publishes this on the `GameView:game-submitted` channel to `games.js` model where the request is posted.


5. What optional second argument does the `fetch` method take? And what is it used for in this application? Hint: See [Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) on the MDN docs.
Fetch allows an optional second argument which can accept user specified settings in the form of an object which can be applied to the request. In this instance, the `method`, `body` and `headers` options have been selected but further options are available [As Seen Here](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch). Within this application, these options are specified to indicate that a `POST` method will change the body of a payload to a JSON object. The headers option indicates that the content-type of the posted information will be in JSON format.


6. Which of the games API routes does the front-end application consume (i.e. make requests to)?
Post & delete. When a new game is rendered, a post method is made to save the data to the aforementioned database collection. A delete button is also added with the `_id` of the game when a new game is created. This can be used to delete the instance of a saved game.

7. What are we using the [MongoDB Driver](http://mongodb.github.io/node-mongodb-native/) for?
Allowing interaction between node.js and MongoDB.

## Extension

Why do we need to use [`ObjectId`](https://mongodb.github.io/node-mongodb-native/api-bson-generated/objectid.html) from the MongoDB driver?
The ObjectId value (which is a unique identifier) is essential to track the entries to the MongoDB. Use of the ObjectID ensures the correct entry is updated or deleted (as in this instance).

Draw a diagram showing the dataflow through the application starting with a form submission, ending with the re-rendering of the page. This will involve a multi-direction data-flow with the client posting data to the server and the server sending data back to the client with the response. Detail the client, server and database in the diagram and include the names of the files involved in the process.

Task *** Dataflow Diagram

Form Submission ->

games.js - publish on games:data-loaded
games.js - subscribe on gameview:game-delete-clicked - deleteGame (this.request.delete(gameId)) method from requesthelper
games.js - subscribe on gameview:game-submitted - postGame (this.request.post(game)) method from requesthelper
games_grid_view.js - subscribe on games:data-loaded
games_form_view.js - publish on gameview:game-submitted
game_view.js - publish on gameview:game-delete-clicked
