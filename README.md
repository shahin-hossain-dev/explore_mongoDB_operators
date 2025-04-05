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

- operator not -> `$not`
  - `db.test.find({age: {$not: {$eq: 30}}})`
  - `$not` এর সাথে সবসময় অন্য query add করে কাজ করতে হয়, এটি একা একা কাজ করতে পারে না।
  - `$not` query করার সময় document এ যদি field নাও থাকে তাহলে বা `null` থাকে ঐ document ও পাবে।

### Element Query Operators

- Operator -> `$exists`

- `db.test.find({company: {$exists: true}})`

  - `$exists` operator boolean use করে document এর property যদি exist থাকে তাহলে ঐ document গুলো পাওয়া যাবে অথবা যাবে না, কিন্তু এই property value এর উপর depend করে না। property আছে কিনা সেটা চেক করে data provide করে।

- Operator -> `$type`
  - `db.test.find({age: {$type: "string"}})`
  - `$type` operator use করে একটি নির্দিষ্ট type এর data পাওয়ার জন্য ব্যবহার করা হয়।

### Array Query Operators

- Oprator -> `$size`
  - `db.test.find({friends: {$size: 4}}).projection({friends: 1})`
  - কোনো field থেকে নির্দিষ্ট array size এর ‍elements গুলো পেতে এই opartor use করা হয়।
- Operator -> `$all`
  - `db.test.find({interests: {$all: ["Cooking", "Writing", "Reading"]}})`
  - Array এর মধ্যে নির্দিষ্ট field এর value অনুযায়ী all data পাওয়ার জন্য `$all` operator.
- Operator -> `$elemMatch`
  - `db.test.find({skills: {$elemMatch: {name: "JAVASCRIPT", level: "Expert"}}})`
  - Object এর মধ্যে নির্দিষ্ট field এর value অনুযায়ী all data পাওয়ার জন্য `$elemMatch` operator.

### Upadate Operator

- operator -> `$set`
  - `db.test.updateOne(
{_id: ObjectId("6406ad63fc13ae5a40000065")},
{$set: {
    age: 20
}}
)`
  - `$set` operator দিয়ে field এ নতুন value দিয়ে field value update করা হয়। `$set` এর মাধ্যম্যে পূর্বের value replace হয়ে নতুন value add হবে।
- Operator `$addToSet`

  - `db.test.updateOne(
{_id: ObjectId("6406ad63fc13ae5a40000065")},
{$addToSet: {
    languages: 'Bangla'
}}
)`
  - `addToSet` Operator use করে array document update করে, array কে replace না করে নতুন করে element যুক্ত করে, element exist হলে document update করে না।

- Operator -> `$each`

  - `db.test.updateOne(
{_id: ObjectId("6406ad63fc13ae5a40000065")},
{$addToSet: {
    languages: {$each: ['English', "Latin"]}
}}
)`
  - Array এর মধ্যে multiple element set করার জন্য `$each` operator use করতে হয়।

- Operator -> `$push`

  - `db.test.updateOne(
{_id: ObjectId("6406ad63fc13ae5a40000065")},
{$push: {
    languages: {$each: ['English', "Latin"]}
}}
)`
  - Array এর duplicate element add করতে হলে `$push` operator use করতে হবে। ফলে element exist করুক না করুক element add করে দিবে।
  -

- Operator -> `$unset`

  - `db.test.updateOne(
{_id: ObjectId("6406ad63fc13ae5a40000065")},
{$unset: {age: ''}}
)`
  - কোনো field কে remove করে দেওয়ার জন্য `$unset` operator use করা হয়।

- Operator -> `$pop`

  - `db.test.updateOne(
 {_id: ObjectId("6406ad63fc13ae5a40000065")},
{$pop: {languages: -1}}
 )`
  - array field এর প্রথম অথবা শেষ element কে remove করা জন্য `$pop` operator use করা হয়। প্রথম element হলে -1, শেষ element হলে 1.

- Operator -> `$pull`

  - `db.test.updateOne(
  {_id: ObjectId("6406ad63fc13ae5a40000065")},
{$pull: {languages:"English"}}
  )`
  - array field থেকে specific একটা element কে remove করতে চাইলে `pull` operator ব্যবহার করতে হবে।

- Operator -> `$pullAll`
  - db.test.updateOne(
    {\_id: ObjectId("6406ad63fc13ae5a40000065")},
    {$pullAll: {languages: ["Latin", "Thai"]}}
    )
  - array field থেকে multiple element remove করতে চাইলে `$pullAll` operator use করতে হবে।
