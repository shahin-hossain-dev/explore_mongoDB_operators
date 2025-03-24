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

## Mongodb query Operator ( insert,insertOne, find, findOne, field filtering, project)

- single data insert করার জন্য `insertOne({name : "shahin"})`
- multiple data insert করার জন্য `insertMany([{},{}])`
- collection এর single data পেতে `findOne({name: "shahin"})`
- collection এর all data পেতে "find({age: 23})"

### Field filtering

- যদি কোনো এক বা একাধিক object থেকে data filter করে নির্দিষ্ট property প্রয়োজন হয় তাহলে Option দিয়ে field filtering করতে হয়।
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
