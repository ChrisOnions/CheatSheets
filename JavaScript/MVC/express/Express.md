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
