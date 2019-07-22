# Intro to Node.js

## Outline
* Identify the components of the MEAN stack
* Run JavaScript outside of the browser with `node`
* Use `require` to import Node.js modules
* Explain why you might want to use JavaScript for your backend

## Lesson

### Identify the components of the MEAN stack

If you've been developing for a while, it is likely that you've heard of a "MEAN Stack" or "MERN Stack". But what do those terms mean? What is a stack?

A stack, quite simply, is a set of tools commonly used together to build a full web application- from the front end that runs in a users browser *all the way* to the database you'll use to store data on your server. Each tool is built on top of the other, making it a "stack".

> **Key Definition:** "stack"
> A list of the large tools (languages/frameworks) used to build both the backend and frontend of a web application

"Ruby on Rails" is considered a stack because it helps you manage everything from the front end, with ERB, to the database, with ActiveRecord. The LAMP stack is another common stack which uses Linux, Apache, MySQL, and PHP (or Pearl), each of which represent a different "level" in the tools that a LAMP developer would use to build an application.

The MEAN stack also an acronym. It stands for:

* MongoDB
* Express
* Angular
* Node.js

Replace Angular with React and you get the MERN stack:

* MongoDB
* Express
* React
* Node.js

Let's work through this stack in order:

##### MongoDB

MongoDB is a database. Like postgres or sqilte3, it's job is to store (or persist) data for you. Unlike postgres or sqlite, MongoDB is a "NoSQL" database, a database that does not use SQL. This means that many tools we're use to, like joins, are not available out of the box. MongoDB has it's uses, normally in very large applications that need to save data *very* quickly. But, as it does not support joins, maintaining relationships in Mongo is *really* hard, so it isn't ideal for most general application development, which is why we won't go into depth on it in this course.

##### Express

Express is used to manage HTTP routing- how your server will respond to specific HTTP (fetch) requests.

It's used in both the MEAN and MERN stacks, and is one of the most common tools to use with Node, so we'll dedicate an entire lesson to exploring what it is and how to use it. 

For now, think of express as replacing the routes and controllers of your standard Rails app.

##### React / Angular

React and Angular are frontend tools that can be used to build dynamic interfaces. You would use these to display the data that your Express backend manages for you.

##### Node.js

Node.js is nothing more than a way to run JavaScript without using a browser- it is the tool onwhich express  and many, many other tools is built, and will serve as the focus for this lesson.



### Run JavaScript outside of the browser with `node`

If you've used Ruby or Python before, you're probably familiar with terminal commands that look like this:

```
|> ruby app.rb
```

or this:

```
|> python app.py
```

These commands would take a file written in ruby or python, and actually run the code in those file. You can run ruby and python this way because at somepoint you installed an **interpreter**- a program which can read code in a specific language and execute it.

Because JavaScript was developed to be used in the browser, it didn't originally have an interperter that could be used from the terminal like that. If you wanted to run JavaScript, you had to do it in the browser.

That changed in 2008, when some ambitious devs took Googles JavaScript engine for the Chrome browser, built a CLI for it, and released it as Node.js. Node ships with some built in tools for things like file system management, networking, etc- but it's first and foremost a way to run JavaScript from the terminal.

Enough theory! Let's code some stuff.

Open `index.js` with your code editor, and write the following inside the file:

```javascript
// index.js
console.log("Hello World")
```

Now, open that location in your terminal. If we want to run the JavaScript file, without loading it in a browser somehow, we would use the `node` command from Node.js!

If you don't have Node.js installed, you can read up on how to install it here: <https://nodejs.org/en/download/package-manager/>

Not sure if you have it installed? Try running `node -v` in your terminal. If it spits back a number, you're good to go!

`node` is a terminal command which you can give a filepath, to have it execute a JavaScript file. Try running: 

```javascript
|> node index.js
```

You should see "Hello World" appear in the terminal. You've run JavaScript with Node.js!

>**Key Definition:** `node`
> A terminal command which accepts a JS filepath as an argument and runs that file with node.js



### Use `require` to import Node.js Modules

Node.js has a built in function named `require`. You can use it to import data from another JavaScript file or an `npm` package (a project dependency).

Open `data.js`. You should see something like this: 

```javascript
// data.js
module.exports = [
    {
      "revenue": 43,
      "expenses": 702
    }, ...
```

That `module.exports = ` is a way for data.js to provide a variable, in this case an array, for any other file to import.

Go back to `index.js`, and add this line to the top:

```
// index.js
const report = require('./data.js')
console.log("Hello World")

```

Use `console.log` to see what `report` is in the terminal. You should see the array from the other file. We can share arrays, numbers, strings, objects, or even functions between files using `module.exports` and `require`.



### Explain why you might want to use JavaScript for your backend

So why are we bothering with this? Why do we want to write JavaScript for our backend? There are some good reasons, but before we go into them, let's be perfectly clear on something: **Node.js and the MEAN/MERN stack is not inherintly better than any other stack**. Like we said at the beginning of this lesson, stacks are just sets of tools. The best devs know to choose the right tool for the right job. 

Here are some of Node.js's most promenent strengths: 

##### Isomorphism

This is a scary word for a simple concept- if we write JavaScript for our backend, and we write JavaScript for our frontend, we can share code between both the front and backend! Imagine a helper function or a class that you could import into both your backend and frontend- it would be much easier to reuse code and uphold the DRY (Don't repeat yourself) principle of coding.

> **Key Definition:** Isomorphism
>  Running the same logic on the server and in the browser

##### Realtime Applications

Socket.io, a tool we will learn about in a future lesson, is one of the most popular libraries for building realtime apps- applications where data is updated on the page in realtime, without having to refresh the browser. Think about when you're on Facebook or YouTube- you don't have to refresh the page to see new posts or comments when they're created- they show up automatically, becaue YouTube and Facebook use special tools to ensure that data updates in "realtime". Realtime features can be built within pretty much any backend tool- Rails has a procedure for implementing realtime features, and Python actually has it's own implementation of Node.js's socket.io. With that said, it is still quite a bit easier to get up and running with sockets in JavaScript than most other backend languages.



These two advantages do not mean that Node.js is automatically the best choice for your backend - Ruby and Python have different strengths that might be more valuable for your specific use case. For example, Ruby has one of the best ORMs ever built in ActiveRecord- if you're going to have lot's of relationships in your application, ActiveRecord is going to be **extremely** helpful in managing those relationships for you. Nothing in Node will even come close to providing the support for database relationships that ActiveRecord does! Python has packages for machine learning and data science that make it a much more valuable tool for apps that require those features.

We're learning Node.js to explore the similaraties between Node and Ruby, to gain more insight into fundamental web development concepts that will apply in any stack or language you choose to learn in the future. We're also excited to provide support for Node.js if the opportunity arises to use it in a project. But it is **imperitive** that we resist the temptation to make arbitrary decisions about what tools are "better" just because we may like one more at the moment. All tools have strengths and weaknesses, and Node.js is no exception.



## Check Your Understanding

Use basic JavaScript methods, `console.log` , `require` and `node` to calculate the average profit (revenue minus expenses) for the data set in `data.js`.