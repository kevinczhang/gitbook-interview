# MongoDB

A quick reference guide for common `mongosh` commands and CRUD operations.

### 📁 Database & Collection Management

| **Command**                     | **Description**                                        |
| ------------------------------- | ------------------------------------------------------ |
| `show dbs`                      | List all available databases.                          |
| `use <db_name>`                 | Switch to a database (creates it if it doesn't exist). |
| `db`                            | Show the current database you are using.               |
| `db.createCollection("<name>")` | Manually create a collection.                          |
| `show collections`              | List all collections in the current database.          |
| `db.<collection>.drop()`        | Delete a specific collection.                          |
| `db.dropDatabase()`             | Delete the current database.                           |

### 📝 CRUD Operations

#### Create (Insert)

```sql
// Insert a single document
db.users.insertOne({ name: "Alice", age: 25 });

// Insert multiple documents
db.users.insertMany([
  { name: "Bob", age: 30 },
  { name: "Charlie", age: 35 }
]);
```

#### Read (Find)

```sql
// Get all documents
db.users.find();

// Find with a filter
db.users.find({ name: "Alice" });

// Projection: Show only name, hide _id (1 = show, 0 = hide)
db.users.find({}, { name: 1, _id: 0 });
```

#### Update

```sql
// Update the first match
db.users.updateOne({ name: "Alice" }, { $set: { age: 26 } });

// Update all matches
db.users.updateMany({ age: { $gt: 30 } }, { $set: { status: "Senior" } });

// Remove a field ($unset)
db.users.updateOne({ name: "Bob" }, { $unset: { status: "" } });
```

#### Delete

```sql
// Delete the first match
db.users.deleteOne({ name: "Alice" });

// Delete all matches
db.users.deleteMany({ status: "Senior" });
```

***

### 🔍 Query Modifiers & Operators

#### Comparison Operators

* `$eq` : Equal to
* `$ne` : Not equal to
* `$gt` / `$gte` : Greater than / Greater than or equal
* `$lt` / `$lte` : Less than / Less than or equal
* `$in` : Matches any value in an array

#### Logical Operators

```sql
// Find users who are EITHER age 25 OR name "Bob"
db.users.find({ $or: [{ age: 25 }, { name: "Bob" }] });
```

#### Sorting & Limiting

```sql
// Sort by age (1: Ascending, -1: Descending)
db.users.find().sort({ age: 1 });

// Limit results to 5
db.users.find().limit(5);
```

***

### ⚡ Performance & Indexing

```sql
// Create an index to speed up queries on "email"
db.users.createIndex({ email: 1 });

// Check query performance
db.users.find({ email: "test@test.com" }).explain("executionStats");
```
