
###  mongodb
```queiries
> use students
switched to db students

> db.studentData.insertOne({ name: "Divya", age: 22, city: "Gudur" })
{
  acknowledged: true,
  insertedId: ObjectId("66c4a7a1f29610a41a44a001")
}

> db.studentData.insertMany([
  { name: "Ravi", age: 24, city: "Chennai" },
  { name: "Meena", age: 21, city: "Hyderabad" }
])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("66c4a7a1f29610a41a44a002"),
    '1': ObjectId("66c4a7a1f29610a41a44a003")
  }
}

> db.studentData.find({})
{ _id: ObjectId("66c4a7a1f29610a41a44a001"), name: "Divya", age: 22, city: "Gudur" }
{ _id: ObjectId("66c4a7a1f29610a41a44a002"), name: "Ravi", age: 24, city: "Chennai" }
{ _id: ObjectId("66c4a7a1f29610a41a44a003"), name: "Meena", age: 21, city: "Hyderabad" }

> db.studentData.find({ city: "Gudur" })
{ _id: ObjectId("66c4a7a1f29610a41a44a001"), name: "Divya", age: 22, city: "Gudur" }

> db.studentData.find({ age: { $gt: 20 } })
{ _id: ObjectId("66c4a7a1f29610a41a44a001"), name: "Divya", age: 22 }
{ _id: ObjectId("66c4a7a1f29610a41a44a002"), name: "Ravi", age: 24 }
{ _id: ObjectId("66c4a7a1f29610a41a44a003"), name: "Meena", age: 21 }

> db.studentData.find({ age: { $lt: 25 } })
{ _id: ObjectId("66c4a7a1f29610a41a44a001"), name: "Divya", age: 22 }
{ _id: ObjectId("66c4a7a1f29610a41a44a002"), name: "Ravi", age: 24 }
{ _id: ObjectId("66c4a7a1f29610a41a44a003"), name: "Meena", age: 21 }

> db.studentData.find({ age: { $gt: 20 }, city: "Gudur" })
{ _id: ObjectId("66c4a7a1f29610a41a44a001"), name: "Divya", age: 22, city: "Gudur" }

> db.studentData.find({ $and: [ { age: { $gt: 20 } }, { city: "Gudur" } ] })
{ _id: ObjectId("66c4a7a1f29610a41a44a001"), name: "Divya", age: 22, city: "Gudur" }

> use employees
switched to db employees

> db.employees.insertMany([
  { name: "Arjun", salary: 32000, department: "HR" },
  { name: "Sneha", salary: 42000, department: "IT" }
])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("66c4a7a1f29610a41a44a004"),
    '1': ObjectId("66c4a7a1f29610a41a44a005")
  }
}

> db.employees.find({ salary: { $gte: 30000 } })
{ _id: ObjectId("66c4a7a1f29610a41a44a004"), name: "Arjun", salary: 32000 }
{ _id: ObjectId("66c4a7a1f29610a41a44a005"), name: "Sneha", salary: 42000 }

> use users
switched to db users

> db.users.find({ age: { $gt: 25 } })
{ _id: ObjectId("66c4a7a1f29610a41a44a006"), name: "Rakesh", age: 35 }

> db.users.find().sort({ createdAt: -1 })
[
  { _id: ObjectId("66c4a7a1f29610a41a44a007"), name: "Sneha", createdAt: ISODate(...) },
  { _id: ObjectId("66c4a7a1f29610a41a44a008"), name: "Arjun", createdAt: ISODate(...) }
]

> db.users.find({}, { _id: 0, name: 1, email: 1 })
[
  { name: "Sneha", email: "sneha@example.com" },
  { name: "Arjun", email: "arjun@example.com" }
]

> db.users.find({
    $or: [
      { city: "Bangalore" },
      { age: { $gt: 30 } }
    ]
})
[
  { _id: ObjectId("66c4a7a1f29610a41a44a006"), name: "Rakesh", age: 35 },
  { _id: ObjectId("66c4a7a1f29610a41a44a009"), name: "Sneha", city: "Bangalore" }
]

> db.users.deleteMany({ active: false })
{ acknowledged: true, deletedCount: 2 }

> db.users.updateOne(
  { username: "john_doe" },
  { $set: { email: "john.doe@example.com" } }
)
{ acknowledged: true, matchedCount: 1, modifiedCount: 1 }

> use books
switched to db books

> db.books.find({
  author: "Chetan Bhagat",
  publishedYear: { $gt: 2010 }
})
{ _id: ObjectId("66c4a7a1f29610a41a44a00a"), title: "Half Girlfriend", publishedYear: 2012 }

> use customers
switched to db customers

> db.customers.countDocuments({ city: "Delhi" })
42

> use logs
switched to db logs

> db.logs.find().skip(10).limit(5)
[
  { _id: ObjectId("66c4a7a1f29610a41a44a00b"), event: "login" },
  { _id: ObjectId("66c4a7a1f29610a41a44a00c"), event: "logout" }
]

> use products
switched to db products

> db.products.find().sort({ price: 1 })
[
  { _id: ObjectId("66c4a7a1f29610a41a44a00d"), name: "Notebook", price: 20 },
  { _id: ObjectId("66c4a7a1f29610a41a44a00e"), name: "Headphones", price: 500 }
]
