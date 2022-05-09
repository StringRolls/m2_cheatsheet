# **Module 2 applications cheatsheet**

## **package.json**

1 - Make sure that you have `"scripts"`, `"dependencies"` and `"devDependencies"` in your `.json`.

2 - Update every dependency version to the latest. They should be autosggested by VsCode.

3 - Make sure you have `"nodemon"` in your `"devDependencies"` object.

4 - Make sure in your `"scripts"` object you have a command to run your application continuously. A default option for this could be: 
```` JSON
"dev" : "nodemon --ext html,js,hbs,css app.js"
````

5 - **In your terminal**, use  `npm i` or `npm install` to download all your dependencies. Make sure that you are inside the project folder, where your `package.json` is stored.

You are good to go!

<hr>

## **File structure**

There are no strict rules on the structure that your directories must have, but for a general consensus you should have something like this:

``` bash
project
|
├───── bin
|       └───── seeds.js
|
├───── config
|       ├───── cloudinary.js
|       ├───── db.js
|       └───── global.js
|
├───── middleware
|       ├───── midFunction1.js
|       └───── midFunction2.js
|              <etc...>
|
├───── models
|       ├───── schema1.model.js
|       └───── schema2.model.js
|              <etc...>
|
├───── public
|       ├───── images
|       |       ├───── img1.png
|       |       └───── img2.png
|       |               <etc...>
|       |       
|       └───── stylesheets
|               └───── style.css
|
├───── routes
|       ├───── auth.js
|       ├───── routes2.js
|       └───── routes3.js
|              <etc...>
|
├───── views
|       ├───── auth
|       |       ├───── login.hbs
|       |       └───── singup.hbs
|       |      
|       ├───── dir1
|       |       ├───── dir1file1.hbs
|       |       └───── dir1file2.hbs
|       |               <etc...>
|       |
|       ├───── layout.hbs
|       ├───── index.hbs
|       ├───── error.hbs
|       └───── not-found.hbs
|
├───── .gitignore
├───── app.js
├───── package-lock.json
├───── package.json
└───── README.md
```

### **Some notes**
- Division is key! Try to separate the project in order for you to focus on one single thing at a time. For example, you don't want to have your configuration in the same file where your routes are.
- Remember to `require()` every file that you are accessing in other files. Same thing goes for every library that you have to use: it needs to be required in every file where it is being used.
- You can use `project/config/global.js` in order to put all the basic configuration for the app (`app.use()`, `app.set()`, `hbs.registerPartials()`...)
- Use `project/config/db.js` to establish the connection to the database.
- In case you want to seed the database do it through `project/bin/seeds.js`.
- Routes should be well sepparated by theme (authentication, user, etc.)
- You should only use `app.js` to require every file and `app.use()` every router.

<hr>

## **Routing**
We are going to establish our application's route through the various express methods that we know. Please notice that they are named after the http action verbs they respond to.

Basic syntax for EVERY route that you will code goes as follows:
```` js
// GET route
app.get('/', middleware, (req, res) => {
    // Here you specify what happens when you recieve a GET request for this route
});

// POST route
app.post('/', middleware, (req, res) => {
    // Here you specify what happens when a user sends a POST request to this route
});

// Sister route
app
.route('/')
.get( middleware, (req, res) => {
    // code
})
.post( middleware, (req, res) => {
    // code
})
````

Notice that the above code is ALWAYS required when you write a route, what will change is **the code inside the callback** depending on what you want to happen.
<br/>
<br/>

### **Regarding routes and rendering:**
We need to make something very clear that needs to be ingrained in our brains.
````js
app.get('/', (req, res) => {
    User.find()
    .then(dbUsers => res.render('userViews/user-list', { users: dbUsers }))
    .catch(err => console.log(err))
})
````
Using the above code as an example, we need to understand that:
- The string we find before the callback is **the name of our route**.
- On the other hand, the string that we find after the `res.render()` express method is **the name of our `.hbs` file**. It is the file that contains the html structure that we will serve in a certain route as a response to a GET request.

We should never confuse the two of them, and you need to learn by heart which one is which and how to use them. In case we used `res.redirect()` and not `res.render()`, however, we would then specifiy the ROUTE, and not the hbs file. This is because render paints a file, but redirect makes a GET request to a route.

<hr>

## **ExpressJS vs Mongoose**
As we had some trouble differentiating the two, here is the main difference:

- **Express** is a library that helps us build a server for our application. It is related to the routing, the authentication and authorization or the rendering of views. It is the skeleton of the website.
- **Mongoose**, on the contrary, is a library that exclusively helps us connect to MongoDB. In other words, it is the portal to our database. It is related to everything that has to do with the db, and ONLY what has to do with the db. We will only use mongoose when we want to interact with mongo: models, connection and to create, update or retrieve objects from our db. It is the tool that helps us feed dynamic content to our website.

Hopefully this makes it clearer!
