# Cheatsheet

## Index

<br>

[Init](#Install)

[Arrow-Functions](##Arrow-Functions)

[Prerequisites](#Prerequisites)

[Deconstructing](#De-constructing)

[Object Orientated Programing](#OOP)

[Promise](##Promise-)

[Promise-all](##Promise-all)

[ES6 Classes](#Es6_Classes)

[Express](#Express)

[Express_Yourself](#Express_Yourself)

[Routes](#Routes)

[MySQL](#MySQL)

[ORM](#Object-relational-mapping)

[Sequelize](#sequelize)

[Models](#Models)

[CRUD](#CRUD)

[Async-Await](#Async-Await)

[Restfull-Routes](#Restfull-Routes)

[Password-Hashing](#Password-Hashing)

[Relationships](#Relationships)

[Sessions](#Sessions)

[Cookies](#Cookies)

[MVC](#MVC)

[REVIEW](#REVIEW)

<br>

# Create full stack Directory

<ol>

<li> touch readme.md server.js .gitignore .env .eslintrc.json .eslintignore </li><br>

<li>mkdir config controllers db models public seeds utils views</li><br>

<li>mkdir controllers/api public/css public/js views/layouts</li><br>

<li>touch config/connection.js controller/homeRoutes.js controller/index.js controller/api/index.js db/schema.sql models/index.js public/css/style.css public/js/index.js seeds/seed.js </li><br>
<!-- <li></li><br> -->
</ol>

# Install

npm init ( Add related Data )

npm i bcrypt [Docs](https://www.npmjs.com/package/bcrypt)

Need to download express [Download](https://nodejs.org/en/download/)

npm i express [Docs](https://www.npmjs.com/package/express)

npm i express-sessions [Docs](https://www.npmjs.com/package/express-session)

npm i express-handlebars [Docs](https://www.npmjs.com/package/express-handlebars)

npm i mysql2 [Docs](https://www.npmjs.com/package/mysql)

npm i sequelize [Docs](https://www.npmjs.com/package/sequelize)

npm i connect-session-sequelize [Docs](https://www.npmjs.com/package/connect-session-sequelize)

## Arrow-Functions

```javascript
() => {}

Const Data = () => {}

Const Data = Callback((req, res) => {
  let do_somthing = Somthing_good
  res.status().json(do_somthing)
})
```

## rest and spread

rest

...rest get all items without having to pass them in individually

```javascript
// And the rest
const songs = ["Creep", "Everlong", "Bulls On Parade", "Song 2", "What I Got"];
const newSongs = [...songs];
console.log(newSongs);
// Logs all songs
```

Spread - [Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

## De-constructing

```javascript
const js = {
  name: "JavaScript",
  type: "programming language",
  version: "ES6",
  tools: {
    frameworks: {
      framework1: "AngularJS",
      framework2: "Vue.js",
    },
    libraries: {
      library1: "jQuery",
      library2: "React",
    },
  },
};
const { framework1, framework2 } = js.tools.frameworks;
```

## OOP

```javascript
function Animal(raining, noise) {
  this.raining = raining;
  this.noise = noise;
  this.makeNoise = () => {
    if (this.raining === true) {
      console.log(this.noise);
    }
  };
}

const dogs = new Animal(true, "Woof!");
const cats = new Animal(false, "Meow!");

dogs.makeNoise();
cats.makeNoise();

const massHysteria = (dogs, cats) => {
  if (dogs.raining === true && cats.raining === true) {
    console.log("DOGS AND CATS LIVING TOGETHER! MASS HYSTERIA!");
  }
};

massHysteria(dogs, cats);
```

## Promise-

```javascript
const choresDone = true;

// Promise
const willGetSwitch = new Promise((resolve, reject) => {
  // Check for a desireable outcome, if so resolve the promise
  if (choresDone) {
    const reward = {
      name: "Nintendo Switch",
      desired: true,
    };
    resolve(reward);
    // Otherwise reject the promise
  } else {
    const issue = new Error("Child did not finish chores as promised");
    reject(issue);
  }
});
// Another promise to call only if we get the reward
const playGames = (reward) => {
  const message = `I am playing games on my new ${reward.name}`;
  return Promise.resolve(message);
};

willGetSwitch
  .then(playGames)
  .then((resolved) => console.log(resolved))
  .catch((err) => console.error(err));
```

## Promise-all

```javascript
// Promise resolved right away
const p1 = new Promise((resolve, reject) => {
  const time = 0;
  if (time < 0) {
    reject(new Error("Something went wrong"));
  } else {
    resolve("Resolved right away");
  }
});
console.log("Status of p1:", p1);

// Promise resolved after one second
const p2 = new Promise((resolve, reject) => {
  const time = 1000;
  if (time < 0) {
    reject(new Error("Something went wrong"));
  } else {
    setTimeout(() => {
      resolve("Resolved after 1 second");
    }, time);
  }
});
console.log("Status of p2:", p2);

// Promise resolved after three seconds
const p3 = new Promise((resolve, reject) => {
  const time = 3000;
  if (time < 0) {
    reject(new Error("Something went wrong"));
  } else {
    setTimeout(() => {
      resolve("Resolved after 3 seconds");
    }, time);
  }
});
console.log("Status of p3:", p3);

// After all three are resolved, Promise.all() returns the results
Promise.all([p1, p2, p3])
  .then((values) => {
    console.log("\nThe returned array from our Promise.all() call:");
    console.log(values);
  })
  .catch((err) => new Error(err));
```

# Es6_Classes

### Item.js

```javascript
class Item {
  constructor(title, price) {
    this.title = title;
    this.price = price;
  }
}

module.exports = Item;
```

### Order.js

```javascript
class Order {
  constructor(item) {
    this.item = item;

    this.id = Math.floor(Math.random() * 99) + 1;
  }
}

module.exports = Order;
```

### Restraunt.js

```javascript
const Order = require("./order");
const Item = require("./item");
class Restaurant {
  constructor(name) {
    this.name = name;
    this.orders = [];
    this.revenue = 0;
  }
  takeOrder(order) {
    this.revenue += order.item.price;
    this.orders.push(order);
    console.log(`Added #${order.id} to the queue`);
    this.printRevenue();
  }
  printRevenue() {
    console.log(`${this.name} has made ${this.revenue} so far!`);
  }
  prepareOrders() {
    const prepareInterval = setInterval(() => {
      if (this.orders.length === 0) {
        console.log("Finished cooking all orders!");

        clearInterval(prepareInterval);
      } else {
        const order = this.orders.shift();

        console.log(`#${order.id} has been prepared.`);
      }
    }, 1000);
  }
}
const restaurant = new Restaurant("McJared's");
const items = [
  new Item("Burger", 5.99),
  new Item("Soda", 3.5),
  new Item("Chips", 2.0),
];
const orders = items.map((item) => new Order(item));
orders.forEach((order) => restaurant.takeOrder(order));
restaurant.prepareOrders();
```

# Express

Server.js

```javascript
const http = require("http");
const PORT = 8080;
const handleRequest = (request, response) => {
  response.end(`It Works!! Path Hit: ${request.url}`);
};
const server = http.createServer(handleRequest);
server.listen(PORT, () => {
  console.log(`Server listening on: http://localhost:${PORT}`);
});
```

## Serving html via path and fs

```javascript
// Dependencies
const http = require("http");
const fs = require("fs");

// Set our port to 8080
const PORT = 8080;

// Create a function for handling the requests and responses coming into our server
const handleRequest = (req, res) => {
  // Here we use the fs package to read our index.html file
  fs.readFile(`${__dirname}/index.html`, (err, data) => {
    if (err) throw err;
    // We then respond to the client with the HTML page by specifically telling the browser that we are delivering
    // an html file.
    res.writeHead(200, { "Content-Type": "text/html" });
    res.end(data);
  });
};
// Create our server
const server = http.createServer(handleRequest);

// Starts our server
server.listen(PORT, () => {
  console.log(`Server is listening on PORT: ${PORT}`);
});
```

## Express_Yourself

```javascript
// If extended is false, you can not post "nested object"
// If extended is true, you can do whatever way that you like.
app.use(express.urlencoded({ extended: true }));
app.use(express.json());
```

> - What is Middleware? It is those methods/functions/operations that are called BETWEEN processing the Request and sending the Response in your application method.

> - When talking about express.json() and express.urlencoded() think specifically about POST requests (i.e. the .post request object) and PUT Requests (i.e. the .put request object)
>   You DO NOT NEED express.json() and express.urlencoded() for GET Requests or DELETE Requests.

> - You NEED express.json() and express.urlencoded() for POST and PUT requests, because in both these requests you are sending data (in the form of some data object) to the server and you are asking the server to accept or store that data (object), which is enclosed in the body (i.e. req.body) of that (POST or PUT) Request

> - Express provides you with middleware to deal with the (incoming) data (object) in the body of the request.

> - a. express.json() is a method inbuilt in express to recognize the incoming Request Object as a JSON Object. This method is called as a middleware in your application using the code: app.use(express.json());

> - b. express.urlencoded() is a method inbuilt in express to recognize the incoming Request Object as strings or arrays. This method is called as a middleware in your application using the code: app.use(express.urlencoded());

> - ALTERNATIVELY, I recommend using body-parser (it is an NPM package) to do the same thing. It is developed by the same peeps who built express and is designed to work with express. body-parser used to be part of express. Think of body-parser specifically for POST Requests (i.e. the .post request object) and/or PUT Requests (i.e. the .put request object)

# Routes

Basic Routes

Basic app demonstrating Node and Express with vanilla javascript.

```javascript
app.get("/", (req, res) => res.send("Html or text or whaatever"));

app.get("/api/Getitem", (req, res) => res.json(Item));

app.post("/api/tables", (req, res) => {
  // Note the code here. Our "server" will respond to requests and let users
  //   know if they have a table or not.
  // req.body is available since we're using the body parsing middleware
  if (tableData.length < 5) {
    tableData.push(req.body);
    res.json(true);
  } else {
    waitListData.push(req.body);
    res.json(false);
  }
});
```

# MySQL

```sql
-- Delete Database if it exists
DROP DATABASE IF EXISTS database_1;
-- Create brand new database
CREATE DATABASE database_1;
```

Create Table

```sql
-- Primary key is id
CREATE TABLE new_table(
id INTEGER(11) AUTO_INCREMENT NOT NULL,
-- Create author id int
  item1 INTEGER(11),
-- VARCHAR max char 100 long
  item2 VARCHAR(100),
  PRIMARY KEY (id)
)
```

Insert data into database

```sql
INSERT INTO new_table (item1, item2) values ('New', 'Data');
```

Selecting from DB

```sql
SELECT * FROM new_table;
```

Sql Joins - Inner, Left, Right.

```sql

```

# Object-relational-mapping

```md
An object-relational mapper (ORM) is a code library that automates the transfer of data stored in relational database tables into objects that are more commonly used in application code.
```

## sequelize

```javascript
const Sequelize = require("sequelize");
// Create a connection object
const sequelize = new Sequelize(
  // Database name
  "database_db",
  // User
  "USERNAME", //root
  // Password
  "DATABASE PASSWORD",
  {
    // Database location
    host: "localhost",
    dialect: "mysql",
    port: 3306,
  }
);
module.exports = sequelize;
```

## Models

```javascript
const { Model, DataTypes } = require("sequelize");
const sequelize = require("../config/connection");

// Create a new Sequelize model for books
class Book extends Model {}

Book.init(
  // Define fields/columns on model
  // An `id` is automatically created by Sequelize, though best practice would be to define the primary key ourselves
  {
    title: {
      type: DataTypes.STRING,
    },
    author: {
      type: DataTypes.STRING,
    },
    isbn: {
      type: DataTypes.STRING,
    },
    pages: {
      type: DataTypes.INTEGER,
    },
    edition: {
      type: DataTypes.INTEGER,
    },
    // Will become `is_paperback` in table due to `underscored` flag
    isPaperback: {
      type: DataTypes.BOOLEAN,
    },
  },
  {
    // Link to database connection
    sequelize,
    // Set to false to remove `created_at` and `updated_at` fields
    timestamps: false,
    underscored: true,
    modelName: "book",
  }
);

module.exports = Book;
```

# CRUD

- Create - Read - Update - Delete

## Create - Create

<br>

```javascript
const router = require("express").Router();

// Import the model
const Book = require("../../models/Book");

// CREATE a book
router.post("/", (req, res) => {
  // Use Sequelize's `create()` method to add a row to the table
  // Similar to `INSERT INTO` in plain SQL
  Book.create({
    title: req.body.title,
    author: req.body.author,
    is_paperback: true,
  })
    .then((newBook) => {
      // Send the newly created row as a JSON object
      res.json(newBook);
    })
    .catch((err) => {
      res.json(err);
    });
});

module.exports = router;
```

## Update - Put

<br>

```javascript
router.put("/:isbn", (req, res) => {
  // Calls the update method on the Book model
  Book.update(
    {
      // All the fields you can update and the data attached to the request body.
      title: req.body.title,
      author: req.body.author,
      isbn: req.body.isbn,
      pages: req.body.pages,
      edition: req.body.edition,
      is_paperback: req.body.is_paperback,
    },
    {
      // Gets the books based on the isbn given in the request parameters
      where: {
        isbn: req.params.isbn,
      },
    }
  )
    .then((updatedBook) => {
      // Sends the updated book as a json response
      res.json(updatedBook);
    })
    .catch((err) => res.json(err));
});
```

## Delete - Destroy

```javascript
// Delete route for a book with a matching isbn
router.delete("/:isbn", (req, res) => {
  // Looks for the books based on isbn given in the request parameters and deletes the instance from the database
  Book.destroy({
    where: {
      isbn: req.params.isbn,
    },
  })
    .then((deletedBook) => {
      res.json(deletedBook);
    })
    .catch((err) => res.json(err));
});
```

# Async-Await

- An async function is a function declared with the async keyword, and the await keyword is permitted within them. The async and await keywords enable asynchronous, promise-based behavior to be written in a cleaner style, avoiding the need to explicitly configure promise chains.

```javascript
router.post("/", async (req, res) => {
  const bookData = await Book.create(req.body);

  return res.json(bookData);
});
```

# Restfull-Routes

```javascript
// This route uses async/await with '.catch()' for errors
// and no HTTP status codes
router.get("/", async (req, res) => {
  const userData = await User.findAll().catch((err) => {
    res.json(err);
  });
  res.json(userData);
});

// This route uses async/await with try/catch for errors
// along with HTTP status codes
router.post("/", async (req, res) => {
  try {
    const userData = await User.create(req.body);
    // 200 status code means the request is successful
    res.status(200).json(userData);
  } catch (err) {
    // 400 status code means the server could not understand the request
    res.status(400).json(err);
  }
});
```

# Validation

- Validations and constraints to the User model to prevent bad data from being saved in the database

<br>

```javascript
User.init(
  {
    id: {
      type: DataTypes.INTEGER,
      allowNull: false,
      primaryKey: true,
      autoIncrement: true,
    },
    username: {
      type: DataTypes.STRING,
    },
    email: {
      type: DataTypes.STRING,
      // prevents duplicate email addresses in DB
      unique: true,
      // checks for email format (foo@bar.com)
      validate: {
        isEmail: true,
      },
    },
    password: {
      type: DataTypes.STRING,
    },
  },
  {
    sequelize,
    timestamps: false,
    freezeTableName: true,
    underscored: true,
    modelName: "user",
  }
);
```

# Password-Hashing

Google recommends using stronger hashing algorithms such as SHA-256 and SHA-3. Other options commonly used in practice are bcrypt, scrypt, among many others that you can find in this list of cryptographic algorithms.
[Cryptographic Algorithms](https://en.wikipedia.org/wiki/List_of_algorithms#Cryptography)

```javascript
const router = require("express").Router();
const bcrypt = require("bcrypt");
const User = require("../../models/User");

// CREATE a new user
router.post("/", async (req, res) => {
  try {
    const newUser = req.body;
    // hash the password from 'req.body' and save to newUser
    newUser.password = await bcrypt.hash(req.body.password, 10);
    // create the newUser with the hashed password and save to DB
    const userData = await User.create(newUser);
    res.status(200).json(userData);
  } catch (err) {
    res.status(400).json(err);
  }
});

module.exports = router;
```

# Hooks

- Hooks (also known as lifecycle events), are functions which are called before and after calls in sequelize are executed. For example, if you want to always set a value on a model before saving it, you can add a beforeUpdate hook.

```javascript
const { Model, DataTypes } = require("sequelize");
const sequelize = require("../config/connection");

class User extends Model {}

User.init(
  {
    id: {
      type: DataTypes.INTEGER,
      allowNull: false,
      primaryKey: true,
      autoIncrement: true,
    },
    username: {
      type: DataTypes.STRING,
      allowNull: false,
    },
    email: {
      type: DataTypes.STRING,
      allowNull: false,
      unique: true,
      validate: {
        isEmail: true,
      },
    },
    password: {
      type: DataTypes.STRING,
      allowNull: false,
      validate: {
        len: [8],
      },
    },
  },
  {
    // When adding hooks via the init() method, they go below
    hooks: {
      // Use the beforeCreate hook to work with data before a new instance is created
      beforeCreate: async (newUserData) => {
        // In this case, we are taking the user's email address, and making all letters lower case before adding it to the database.
        newUserData.email = await newUserData.email.toLowerCase();
        return newUserData;
      },
      // Here, we use the beforeUpdate hook to make all of the characters lower case in an updated email address, before updating the database.
      beforeUpdate: async (updatedUserData) => {
        updatedUserData.email = await updatedUserData.email.toLowerCase();
        return updatedUserData;
      },
    },
    sequelize,
    timestamps: false,
    freezeTableName: true,
    underscored: true,
    modelName: "user",
  }
);

module.exports = User;
```

# Instance Methods

```javascript
const { Model, DataTypes } = require("sequelize");
const bcrypt = require("bcrypt");
const sequelize = require("../config/connection");

class User extends Model {
  checkPassword(loginPw) {
    return bcrypt.compareSync(loginPw, this.password);
  }
}

User.init(
  {
    id: {
      type: DataTypes.INTEGER,
      allowNull: false,
      primaryKey: true,
      autoIncrement: true,
    },
    username: {
      type: DataTypes.STRING,
      allowNull: false,
    },
    email: {
      type: DataTypes.STRING,
      allowNull: false,
      unique: true,
      validate: {
        isEmail: true,
      },
    },
    password: {
      type: DataTypes.STRING,
      allowNull: false,
      validate: {
        len: [8],
      },
    },
  },
  {
    hooks: {
      beforeCreate: async (newUserData) => {
        newUserData.password = await bcrypt.hash(newUserData.password, 10);
        return newUserData;
      },
      beforeUpdate: async (updatedUserData) => {
        updatedUserData.password = await bcrypt.hash(
          updatedUserData.password,
          10
        );
        return updatedUserData;
      },
    },
    sequelize,
    timestamps: false,
    freezeTableName: true,
    underscored: true,
    modelName: "user",
  }
);
```

# Relationships

[One to one, one to many](https://sequelize.org/master/manual/assocs.html)

## One to one

```javascript
const Driver = require("./Driver");
const License = require("./License");
// Define a Driver as having one License to create a foreign key in the `license` table
Driver.hasOne(License, {
  foreignKey: "driver_id",
  // When we delete a Driver, make sure to also delete the associated License.
  onDelete: "CASCADE",
});
// We can also define the association starting with License
License.belongsTo(Driver, {
  foreignKey: "driver_id",
});
// We package our two models and export them as an object so we can import them together and use their proper names
module.exports = { Driver, License };
```

## One to many

```javascript
const Driver = require("./Driver");
const License = require("./License");
const Car = require("./Car");

Driver.hasOne(License, {
  foreignKey: "driver_id",
  onDelete: "CASCADE",
});

License.belongsTo(Driver, {
  foreignKey: "driver_id",
});

// Define a Driver as having many Cars, thus creating a foreign key in the `car` table
Driver.hasMany(Car, {
  foreignKey: "driver_id",
  onDelete: "CASCADE",
});

// The association can also be created from the Car side
Car.belongsTo(Driver, {
  foreignKey: "driver_id",
});

module.exports = { Driver, License, Car };
```

# Sessions

```javascript
const path = require("path");
const express = require("express");
// Import express-session
const session = require("express-session");
const exphbs = require("express-handlebars");

const routes = require("./controllers");
const sequelize = require("./config/connection");
const helpers = require("./utils/helpers");

const app = express();
const PORT = process.env.PORT || 3001;

// Set up sessions
const sess = {
  secret: "Super secret secret",
  resave: false,
  saveUninitialized: false,
};

app.use(session(sess));

const hbs = exphbs.create({ helpers });

app.engine("handlebars", hbs.engine);
app.set("view engine", "handlebars");

app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.use(express.static(path.join(__dirname, "public")));

app.use(routes);
sequelize.sync({ force: false }).then(() => {
  app.listen(PORT, () => console.log("Now listening"));
});
```

[Sequalize Sessions](https://www.npmjs.com/package/connect-session-sequelize)

[Helpers]()

# Cookies

```javascript
const session = require("express-session");
const SequelizeStore = require("connect-session-sequelize")(session.Store);
// Set up sessions with cookies
const sess = {
  secret: "Super secret secret",
  cookie: {},
  resave: false,
  saveUninitialized: true,
  store: new SequelizeStore({
    db: sequelize,
  }),
};
app.use(session(sess));
```

# MVC

- Model View Controller

- MVC is short for Model, View, and Controller. MVC is a popular way of organizing your code. The big idea behind MVC is that each section of your code has a purpose, and those purposes are different. ... MVC is a way to organize your code's core functions into their own, neatly organized boxes

- My opinion is its spaghetti code Emulator

## ./views/homepage.handlebars

eg.

```handlebars
{{#if loggedIn}}
  <section class="painting">
    <img src="/images/{{painting.filename}}" alt="{{painting.description}}" />
    <div class="painting-details">
      <h3>{{painting.title}}</h3>
      <p>By: {{painting.artist}}</p>
      <p>Exhibition open until: {{format_date painting.exhibition_date}}</p>
    </div>
  </section>
{{else}}
  <a href="/login">You must login first to view this page</a>
{{/if}}
```

# REVIEW

## MVC-Review

<ul>
  <li>Config</li>
        <ul>
        <li>Connection.js</li>
      </ul>
  <li>Controllers/</li>
          <ul>
        <li>index.js</li>
        <li>homeRoutes.js</li>
      </ul>
  <li>db/
      <ul>
        <li>schema.sql</li>
      </ul>
       <li>models/</li>
          <ul>
        <li>index.js</li>
        <li>user.js</li>
      </ul>
       <li>Public/</li>
          <ul>
          <li>Direct routes</li>
        <li>style.css</li>
        <li>index.html</li>
      </ul>
       <li>seeds/</li>
          <ul>
        <li>All seed data</li>
        <li>userData.json</li>
      </ul>
       <li>utils/</li>
          <ul>
        <li>helper.js</li>
      </ul>
       <li>views/</li>
          <ul>
        <li>layouts/</li>
          <ul>
        <li>main.handlebars</li>
      </ul>
        <li>homepagehandlebars</li>
      </ul>
  </li>
</ul>

- .env
- .gitignore
- package.json
- server.js
