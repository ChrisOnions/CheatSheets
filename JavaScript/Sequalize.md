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
