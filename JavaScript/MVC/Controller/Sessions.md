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
