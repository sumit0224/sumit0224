# Express.js Routes in Detail

## 🔹 Route kya hai?
Express.js me **Route** ek tarika hai client ke request ko handle karne ka.  
Route ke 2 main parts hote hain:
1. **HTTP Method** → `GET`, `POST`, `PUT`, `DELETE`
2. **Path/Endpoint** → `/`, `/users`, `/login`

Aur ek **handler function** hota hai jo response bhejta hai.

---

## 🔹 Basic Syntax
```js
app.METHOD(PATH, HANDLER)
```

- `METHOD` → HTTP method (GET, POST, PUT, DELETE)
- `PATH` → Endpoint path
- `HANDLER` → Function jo request par run hota hai

---

## 🔹 Example: GET Route
```js
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.send("Welcome to Home Page!");
});

app.get("/about", (req, res) => {
  res.send("This is About Page.");
});

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

---

## 🔹 Example: POST Route
```js
app.post("/login", (req, res) => {
  res.send("Login request received");
});
```

---

## 🔹 Route Parameters
```js
app.get("/user/:id", (req, res) => {
  res.send(`User ID is ${req.params.id}`);
});
```
👉 URL: `/user/10` → Response: `User ID is 10`

---

## 🔹 Query Parameters
```js
app.get("/search", (req, res) => {
  const keyword = req.query.q;
  res.send(`You searched for: ${keyword}`);
});
```
👉 URL: `/search?q=express` → Response: `You searched for: express`

---

## 🔹 Multiple Handlers
```js
app.get("/profile", 
  (req, res, next) => {
    console.log("First handler");
    next();
  }, 
  (req, res) => {
    res.send("Second handler - Profile Page");
  }
);
```

---

## 🔹 RESTful API Routes Example
```js
app.get("/items", (req, res) => {
  res.send("Get all items");
});

app.post("/items", (req, res) => {
  res.send("Create new item");
});

app.put("/items/:id", (req, res) => {
  res.send(`Update item with ID: ${req.params.id}`);
});

app.delete("/items/:id", (req, res) => {
  res.send(`Delete item with ID: ${req.params.id}`);
});
```

---

## 🔹 Modular Routing with `express.Router`
### `userRoutes.js`
```js
const express = require("express");
const router = express.Router();

router.get("/", (req, res) => {
  res.send("All users");
});

router.get("/:id", (req, res) => {
  res.send(`User with ID: ${req.params.id}`);
});

module.exports = router;
```

### `server.js`
```js
const express = require("express");
const app = express();
const userRoutes = require("./userRoutes");

app.use("/users", userRoutes);

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

👉 URL: `/users/5` → Response: `User with ID: 5`

---

## ✅ Summary
- Routes = `HTTP Method + Path + Handler`
- `req.params` → URL parameters
- `req.query` → Query string
- `req.body` → POST/PUT request body
- Use `express.Router` for modular routing
