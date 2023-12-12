<img src="https://i.imgur.com/IoI44Cy.jpg">
 
# Jasmi's Express Practice Lab 
---
## Instructions

Fork and clone this lab inside of your homework folder. Once finished, be sure to create a pull request.

## Intro

The Intro to Express lesson, with all of that new information, can be a lot to understand. 

It's natural, in fact, **expected**, to feel "uncomfortable" and confused by Node.js & Express at this point.

As always, the journey toward competence requires practice - so let's get on with it!

## Exercise

The goal of the exercise is to put in a rep doing everything that you did during the Into to Express lesson!

However, instead of To Dos, we're going to be dispalying menu items and prices from Jasmi's! 

## Exercise

Begin by creating a folder and cd into it:

```
mkdir jasmis
cd jasmis
```

Create a package.json using this command:

```
npm init
```

Open the project's folder in VS code:

```
code .
```

Open an integrated terminal in VS Code and use npm to install Express:

```
npm i express
```

Crate a  server.js module:

```
touch server.js
```

Within the server.js, let's add some things.

First, let's import the functionality of our express app by requiring the epxress module:

```
const express = require('express');
```

Next, let's create an instance of express and use it to create the main functionality of our app:

```
const app = express();
```

Let's define a get request that returns a message to the user when they browse to the root route:

```
app.get('/', (req, res) => {
  res.send('Welcome to Jasmis!');
});
```
What's written above is arrow syntax.  It's the same as writing an anonymous callback function with the function keyword, as in the lesson earlier, so don't let it confuse you.

This:

```
app.get('/', (req, res) => {
  res.send('<h1>Welcome to Jasmis!</h1>');
});
```

Is the same as this:

```
app.get('/', function(req, res) {
  res.send('<h1>Welcome to Jasmis!</h1>');
});
```

You can write it either way, but Michael and I like the more modern arrow syntax :) 

Whatever makes the most sense to you is fine though. 

Okay, lastly let's tell the app to listen on port 3000 for incoming HTTP requests from clients, such as our browser:

```
app.listen(3000, () => {
  console.log('Listening on port 30001');
});
```

Now let's run the app:

```
nodemon server 
```

If you browse to localhost:3000 in your window, you should see "Welcome to Jasmis!" dipslayed in the browser window. 

The next step is to set up some view templates to render in our browser.

We're going to use EJS, just as we did in the lesson.

We'll create the views directory and within that we'll create a file called home.ejs.

```
mkdir views
touch views/home.ejs
```

Open the home.ejs template and then use the Emmet abbreviation syntax to generate HTML boilerplate:

```
!
```

The following should be generated for you:

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" 
      content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>First Express</title>
</head>
<body>
    
</body>
</html>
```

Add a welcome message within the body:

```
<body>
  <h1>Welcome to Jasmi's!</h1>
</body>
```

This next part is going to be all you!  Use the readme from the intro to express lesson if you have to.  Your job is to update the app.get route to render the home.jsx template.  Recall that we can use the render method to help us out here.

```
app.get('/', (req, res) => {
  //Use the render method to render the home template 
});
```

You'll notice there's an error when we navigate to localhost:3000.  That's okay!  It's a very descriptive error that says that no default view engine was specified.  Let's configure our app to use ejs as the view engine.  We also need to tell our app where to look to render ejs templates, or views, as they are also called.  Add the following to your server.js beneath where we create the instance of our express app:

```
const app = express();

app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, 'views'));
```

Because we are using the path module, we need to import it at the top of our server.js file/module:

```
const express = require('express');
const path = require('path');
```

Lastly, let's install ejs as a dependency for our app:

```
npm i ejs 
```

Awesome!  If everything is set up correctly you should still see the "Welcome to Jasmi's!" message when navigating to localhost:3000.

Now for the fun bit.  

We're going to create a data folder and within that we're going to create a jasmi-menu.js file/module that exports the data for our app.

Run the following two commands in your integrated terminal:

```
mkdir data
touch data/jasmi-menu.js
```

Open up the jasmi-menu file/module and add the following:

```
const menuItems = [
  {name: 'Big J', price: 2.400},
  {name: 'Special J', price: 2.500},
  {name: 'Mega J', price: 2.900},
  {name: 'Triple J', price: 2.700},
  {name: 'Spicy Chickee Chicken', price: 2.300},
]
```

Sweet!  Next, at the bottom of the jasmi-menu module, we let's define a funciton called getAll and export it. 

```
//A function that returns the menuItems 
const getAll = () => {
  return menuItems;
}

//Include the function in the modules exports object
module.exports = { getAll }
```

Alright, now that that's done, let's import the data within our server.js so that we can access it in our routes:

```
const path = require('path');

// require the To Do "database"
const database = require('./data/jasmi-menu');
```

Okay, now the real work begins.  Show us what you've got!  

1.  Create a new GET route for the endpoint '/menuItems' in your server.js.

2.  Within the callback function for this route, render an index template.  You'll also have to create the template in a later step.  Remember, it will be nested in a folder called todos within the views folder.  The file structure is views => menuItems => index.ejs

3.  Within the locals object (the second argument passed to res.render) include a key value pair where the name is menuItems and the value is the result of calling the getAll method from the database module being imported at the top of server.js.  Remember you need to use dot notation to access this method.  The method must also be invoked using parens `()`.  

4.  Now that the route is defined and a function is written to handle the logic for this route, the next step is to create a menuItems folder in the views folder/directory.  After the folder is created, create a file called index.ejs inside of it.

5.  Finally, open up the index.ejs view template and create some HTML boilerplate.  In the boyd, you'll need to iterate over the menuItems that we passed to the template as part of the locals object. You may need to refer back to the lesson readme for this part, as the syntax can be quite challenging to remember at first.  Basically you'll want to use the forEach method to iterate over all of the menuItems and for each item display the name within an `<h1>` tag and the price within a `<p>` tag.  Make sure to review the difference between the `<% %>` and `<%= %>` tags.  When you open the browser and navigate to `localhost:3000/menuItems`, you should a list of menu items and their prices. 

Alright, that was a lot and you're probably hungry!  

Remember, this takes practice and gets much easier over time.  

Take a break and grab a burger from Jasmi's to refuel for tomorrow!  

### This lab is a deliverable
