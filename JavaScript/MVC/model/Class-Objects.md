# Class With OOP

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
