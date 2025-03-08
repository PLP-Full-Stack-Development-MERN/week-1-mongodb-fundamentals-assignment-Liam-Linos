Setup MongoDB:
Install MongoDB locally or create a free cluster on MongoDB Atla

Start the MongoDB server locally or connect to the MongoDB Atlas cluster.
For local server:
mongod
For Atlas: Use the connection string provided in the Atlas dashboard.

Verify the installation and connection by running:
mongo --version

Database and Collection Creation:
Create a new database
use library

Inside library, create a collection named books.
db.createCollection("books")

Insert Data:
db.books.insertMany([
  { title: "Book One", author: "Author A", publishedYear: 1999, genre: "Fiction", ISBN: "123-456-7890" },
  { title: "Book Two", author: "Author B", publishedYear: 2005, genre: "Non-Fiction", ISBN: "234-567-8901" },
  { title: "Book Three", author: "Author C", publishedYear: 2015, genre: "Science Fiction", ISBN: "345-678-9012" },
  { title: "Book Four", author: "Author A", publishedYear: 2000, genre: "Fantasy", ISBN: "456-789-0123" },
  { title: "Book Five", author: "Author D", publishedYear: 2018, genre: "Biography", ISBN: "567-890-1234" }
])

Retrieve Data:
db.books.find()

Query books based on a specific author.
db.books.find({ author: "Author A" })

Find books published after the year 2000.
db.books.find({ publishedYear: { $gt: 2000 } })

Update Data:
db.books.updateOne(
  { ISBN: "123-456-7890" },
  { $set: { publishedYear: 2001 } }
)

Add a new field called rating to all books and set a default value.
db.books.updateMany(
  {},
  { $set: { rating: 5 } }
)

Delete Data:
db.books.deleteOne({ ISBN: "567-890-1234" })

Remove all books of a particular genre.
db.books.deleteMany({ genre: "Non-Fiction" })

Data Modeling Exercise:
Create a data model for an e-commerce platform including collections for users, orders, and products.
Users:
{
  _id: ObjectId,
  name: String,
  email: String,
  password: String,
  address: String,
  orders: [ObjectId] // referencing orders
}

Orders:
{
  _id: ObjectId,
  userId: ObjectId, // referencing user
  productList: [
    { productId: ObjectId, quantity: Number }
  ],
  totalAmount: Number,
  status: String,
  orderDate: Date
}

Products:
{
  _id: ObjectId,
  name: String,
  description: String,
  price: Number,
  category: String,
  stockQuantity: Number
}

Implement the structure using MongoDB.
db.createCollection("users")
db.createCollection("orders")
db.createCollection("products")

Aggregation Pipeline:
db.books.aggregate([
  { $group: { _id: "$genre", count: { $sum: 1 } } }
])

Calculate the average published year of all books.
db.books.aggregate([
  { $group: { _id: null, averageYear: { $avg: "$publishedYear" } } }
])


Identify the top-rated book.
db.books.find().sort({ rating: -1 }).limit(1)


Indexing:
Create an index on the author field to optimize query performance.
db.books.createIndex({ author: 1 })


Explain the benefits of indexing in MongoDB:
Indexes improve query performance by allowing the database to quickly locate and retrieve the necessary documents.

Indexes can be created on one or multiple fields to optimize specific queries.

However, indexes also consume memory and can impact write operations, so they should be used thoughtfully.
