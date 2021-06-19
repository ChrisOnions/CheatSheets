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
