# explore_mongoose

- install mongodb community server
- install mongodb sell

### How to set mongoes sell as a window command

- install mongodb sell
- copy the mongodb file path location C:\Program Files\MongoDB\Server\8.0\bin
- click window button open edit environment variable > advanced > environment variable > path > new > paste > ok
- open new cmd prompt check mongodb -> mongod --version
- open mongo sell ->cmd: mongosh
- if all ok now enjoy

## Mongodb query command ( insert,insertOne, find, findOne, field filtering, project)

- single data insert করার জন্য `insertOne({name : "shahin"})`
- multiple data insert করার জন্য `insertMany([{},{}])`
- collection এর single data পেতে `findOne({name: "shahin"})`
- collection এর all data পেতে "find({age: 23})"

### Filed filtering

- যদি কোনো এক বা একাধিক object থেকে data filter করে নির্দিষ্ট property প্রয়োজন হয় তাহলে Option দিয়ে field filtering করতে হয়।
  - `find({age: "23"}, {name: 1, age: 1, gender: 1})`
  - এখানে ২য় object হলো options, name কে 1 দ্বারা true করে দেয়া হয়েছে, এখন Object এর মধ্য থেকে শুধু ঐ property গুলো আসবে।
- Filed filtering with chaining
  - `find({age: 23}).project({name: 1, age: 1, gender: 1})`
  - এখানে chaining করে project method এর মাধ্যমে একই ভাবে ডাটা পাওয়া যাবে ।
  - তবে `findOne()` এর ক্ষেত্রে project chaining use করা যাবে না।
