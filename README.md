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
We are going to establish our application's route through the various express methods that we know
