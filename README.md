# explore_mongoDB

- install mongodb community server
- install mongodb sell

### How to set mongoes sell as a window command

- install mongodb sell
- copy the mongodb file path location C:\Program Files\MongoDB\Server\8.0\bin
- click window button open edit environment variable > advanced > environment variable > path > new > paste > ok
- open new cmd prompt check mongodb -> mongod --version
- open mongo sell ->cmd: mongosh
- if all ok now enjoy

### Mongodb query Operator ( insert,insertOne, find, findOne, field filtering, project)

- single data insert করার জন্য `insertOne({name : "shahin"})`
- multiple data insert করার জন্য `insertMany([{},{}])`
- collection এর single data পেতে `findOne({name: "shahin"})`
- collection এর all data পেতে "find({age: 23})"

### Field filtering

- যদি কোনো এক বা একাধিক object থেকে data filter করে নির্দিষ্ট property field প্রয়োজন হয় তাহলে Option দিয়ে field filtering করতে হয়।

  - `find({age: "23"}, {name: 1, age: 1, gender: 1})`
  - এখানে ২য় object হলো options, name কে 1 দ্বারা true করে দেয়া হয়েছে, এখন Object এর মধ্য থেকে শুধু ঐ property গুলো আসবে।

- Filed filtering with chaining
  - `find({age: 23}).project({name: 1, age: 1, gender: 1})`
  - এখানে chaining করে project method এর মাধ্যমে একই ভাবে ডাটা পাওয়া যাবে ।
  - তবে `findOne()` এর ক্ষেত্রে project chaining use করা যাবে না।

### Comparison Query Operators

- equal Operator -> `$eq`

  - `db.test.find({gender: {$eq: "Male"}})` যদি কোনো value এর সমান ডাটা প্রয়োজন হয় তাহলে equal operator use করতে হয়।

- not equal Operator -> `$ne`

  - `db.test.find({age: {$ne: 21}})` যদি কোনো value সমান না এমন ডাটা পাওয়ার জন্য not equal.

- greater than -> `$gt`

  - `db.test.find({age: {$gt: 21}})` যদি value এর থেকে বড় data গুলো পাওয়ার জন্য greater than use করা হয়।

- greater than and equal -> `$gte`

  - `db.test.find({age: {$gte: 21}})` value থেকে বড় এবং সমান ডাটা গুলো পাওয়ার জন্য।

- less than -> `$lt`

  - `db.test.find({age: {$lt: 21}})` যদি value এর থেকে ছোট data পাওয়ার জন্য।

- less than and equal -> `$lte`

  - `db.test.find({age: {$lte: 21}})` যদি value এর থেকে ছোট এবং সমান data পাওয়ার জন্য।

- sort -> `.sort()`

  - `db.test.find({age: {$gte: 21}}).sort({age: 1})
  - এখানে chaining করে age property এর উপর ভিত্তি করে sort করা হয়েছে, যদি ascending প্রয়োজন হয় তাহলে value 1 এবং যদি descending প্রয়োজন হয় তাহলে -1 দিতে হবে।

- implicit and -> `{age: {$gt: 18, $lt: 30}}`

  - filed এর মধ্যে multiple operator দিয়ে implicit and logic তৈরী করা হয়। যেমন এখানে, age field এর জন্য greater than 18 and less than 30 এর সকল ডাটা গুলো আসবে।

- multi filed data get:

  - `db.test.find({gender: "Female", age: { $gt: 17, $lt:30}}, {age: 1, gender: 1}).sort({age: 1})`
  - এখানে multiple filed যুক্ত করা হয়েছে, যাদের gender Female and যাদের ‍ age 17 থেকে বড় এবং 30 থেকে ছোট হবে।, `{age:1, gender: 1}` শুধু এই দুই field এর data গুলো আসবে।

- operator in -> `$in`

  - `db.test.find(
    {
    gender: "Female",
    age: {$in: [23, 26, 30, 18, 22]},
    interests: {$in: ["Gaming", "Cooking"]}
    }, [field find and comparison operator]
)`
  - `$in` operator এর মাধ্যমে field এর যে যে value গুলো ‍array এর দিবে শুধু সেগুলোর ডাটা পাওয়া যাবে।

- operator not in -> `$nin`
  - `db.test.find(
{gender: "Female", age: {$nin: [23, 26]}} //field find and comperison operator
  )`
  - `$nin` operator এর মাধ্যমে field এর যে value গুলো দেয়া হবে সেগুলো বাদে বাকি গুলোর ডাটা পাওয়া যাবে।

### Logical Query Operator

- operator and -> `$and`

  - `db.test.find({$and: [
{age: {$lt: 30}},
{age: {$gt: 18}},
{gender: "Male"}
]})`
  - `$and` operator হলো explicit, logical `$and` এর মাধ্যমে ‍ specific field(property) multiple ভাবে define করা যায়। যা এই operator ছাড়া করা যায় না।

- Operator or -> `$or`
  - `db.test.find({$or: [
{'skills.name': "JAVASCRIPT"},
{"skills.name": "PYTHON"}, 
{"skills.level": "Intermidiate"}
]})`
  - logical `$or` এর মাধ্যমে ‍ specific field(property) multiple ভাবে define করা যায়। তবে একই কাজ `$in` operator দিয়েও করা যায়।
