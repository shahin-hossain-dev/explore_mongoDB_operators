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

  ```
  db.test.find({age: {$gte: 21}}).sort({age: 1})
  ```

  - এখানে chaining করে age property এর উপর ভিত্তি করে sort করা হয়েছে, যদি ascending প্রয়োজন হয় তাহলে value 1 এবং যদি descending প্রয়োজন হয় তাহলে -1 দিতে হবে।

- implicit and -> `{age: {$gt: 18, $lt: 30}}`

  - filed এর মধ্যে multiple operator দিয়ে implicit and logic তৈরী করা হয়। যেমন এখানে, age field এর জন্য greater than 18 and less than 30 এর সকল ডাটা গুলো আসবে।

- multi filed data get:

  ```
  db.test.find(
    {gender: "Female", age: { $gt: 17, $lt:30}},
    {age: 1, gender: 1}).sort({age: 1})
  ```

  - এখানে multiple filed যুক্ত করা হয়েছে, যাদের gender Female and যাদের ‍ age 17 থেকে বড় এবং 30 থেকে ছোট হবে।, `{age:1, gender: 1}` শুধু এই দুই field এর data গুলো আসবে।

- operator in -> `$in`

  ```
  db.test.find(
    {
    gender: "Female",
    age: {$in: [23, 26, 30, 18, 22]},
    interests: {$in: ["Gaming", "Cooking"]}
    }, [field find and comparison operator]
  )
  ```

  - `$in` operator এর মাধ্যমে field এর যে যে value গুলো ‍array এর দিবে শুধু সেগুলোর ডাটা পাওয়া যাবে।

- operator not in -> `$nin`

  ```
  db.test.find(
  {gender: "Female", age: {$nin: [23, 26]}} //field find and comperison operator
    )
  ```

  - `$nin` operator এর মাধ্যমে field এর যে value গুলো দেয়া হবে সেগুলো বাদে বাকি গুলোর ডাটা পাওয়া যাবে।

### Logical Query Operator

- operator and -> `$and`

  ```
    db.test.find({$and: [
  {age: {$lt: 30}},
  {age: {$gt: 18}},
  {gender: "Male"}
  ]})
  ```

  - `$and` operator হলো explicit, logical `$and` এর মাধ্যমে ‍ specific field(property) multiple ভাবে define করা যায়। যা এই operator ছাড়া করা যায় না।

- Operator or -> `$or`

  ```
  db.test.find({$or: [
  {'skills.name': "JAVASCRIPT"},
  {"skills.name": "PYTHON"},
  {"skills.level": "Intermidiate"}
  ]})
  ```

  - logical `$or` এর মাধ্যমে ‍ specific field(property) multiple ভাবে define করা যায়। তবে একই কাজ `$in` operator দিয়েও করা যায়।

- operator not -> `$not`
  ```
  db.test.find({age: {$not: {$eq: 30}}})
  ```
  - `$not` এর সাথে সবসময় অন্য query add করে কাজ করতে হয়, এটি একা একা কাজ করতে পারে না।
  - `$not` query করার সময় document এ যদি field নাও থাকে তাহলে বা `null` থাকে ঐ document ও পাবে।

### Element Query Operators

- Operator -> `$exists`

  ```
  db.test.find({company: {$exists: true}})
  ```

  - `$exists` operator boolean use করে document এর property যদি exist থাকে তাহলে ঐ document গুলো পাওয়া যাবে অথবা যাবে না, কিন্তু এই property value এর উপর depend করে না। property আছে কিনা সেটা চেক করে data provide করে।

- Operator -> `$type`

  -

  ```
  db.test.find({age: {$type: "string"}})
  ```

  - `$type` operator use করে একটি নির্দিষ্ট type এর data পাওয়ার জন্য ব্যবহার করা হয়।

### Array Query Operators

- Oprator -> `$size`

  ```
  db.test.find(
    {friends: {$size: 4}}).projection({friends: 1}
  )
  ```

  - কোনো field থেকে নির্দিষ্ট array size এর ‍elements গুলো পেতে এই opartor use করা হয়।

- Operator -> `$all`

  ```
  db.test.find(
    {interests: {$all: ["Cooking", "Writing", "Reading"]}}
  )
  ```

  - Array এর মধ্যে নির্দিষ্ট field এর value অনুযায়ী all data পাওয়ার জন্য `$all` operator.

- Operator -> `$elemMatch`

  ```
  db.test.find(
    {skills:
      {$elemMatch: {name: "JAVASCRIPT", level: "Expert"}}
    }
  )
  ```

  - Object এর মধ্যে নির্দিষ্ট field এর value অনুযায়ী all data পাওয়ার জন্য `$elemMatch` operator.

### Upadate Operator

- operator -> `$set`

  ```
  db.test.updateOne(
    {_id: ObjectId("6406ad63fc13ae5a40000065")},
    {$set: {
        age: 20
    }}
  )
  ```

  - `$set` operator দিয়ে field এ নতুন value দিয়ে field value update করা হয়। `$set` এর মাধ্যম্যে পূর্বের value replace হয়ে নতুন value add হবে।
  - `$set` operator দিয়ে array of object এর specific object ধরে update করা যায়।

  ```
  db.test.updateOne(
    {_id: ObjectId("6406ad63fc13ae5a40000065"), 'education.major': "Art"},
    {$set: {"education.$.major": 'CSE'}}
  )
  ```

  - এখানে id দিয়ে specifici element select করে, `'education.major': "Art"` দিয়ে specific object কে ধরে, `$set` operator use করে, `{"education.$.major": 'CSE'}` এভাবে field ধরে update করতে হবে। .$. হলো position operator.

- Operator `$addToSet`

  ```db.test.updateOne(
  {_id: ObjectId("6406ad63fc13ae5a40000065")},
  {$addToSet: {
      languages: 'Bangla'
  }}
  )
  ```

  - `addToSet` Operator use করে array document update করে, array কে replace না করে নতুন করে element যুক্ত করে, element exist হলে document update করে না।

- Operator -> `$each`

  ```
  db.test.updateOne(
  {_id: ObjectId("6406ad63fc13ae5a40000065")},
  {$addToSet: {
      languages: {$each: ['English', "Latin"]}
  }}
  )
  ```

  - Array এর মধ্যে multiple element set করার জন্য `$each` operator use করতে হয়।

- Operator -> `$push`

  ```db.test.updateOne(
  {_id: ObjectId("6406ad63fc13ae5a40000065")},
  {$push: {
      languages: {$each: ['English', "Latin"]}
  }}
  )
  ```

  - Array এর duplicate element add করতে হলে `$push` operator use করতে হবে। ফলে element exist করুক না করুক element add করে দিবে।

- Operator -> `$unset`

  ```db.test.updateOne(
  {_id: ObjectId("6406ad63fc13ae5a40000065")},
  {$unset: {age: ''}}
  )
  ```

  - কোনো field কে remove করে দেওয়ার জন্য `$unset` operator use করা হয়।

- Operator -> `$pop`

  ```
  db.test.updateOne(
  {_id: ObjectId("6406ad63fc13ae5a40000065")},
  {$pop: {languages: -1}}
  )
  ```

  - array field এর প্রথম অথবা শেষ element কে remove করা জন্য `$pop` operator use করা হয়। প্রথম element হলে -1, শেষ element হলে 1.

- Operator -> `$pull`

  ```
  db.test.updateOne(
  {_id: ObjectId("6406ad63fc13ae5a40000065")},
  {$pull: {languages:"English"}}
  )
  ```

  - array field থেকে specific একটা element কে remove করতে চাইলে `pull` operator ব্যবহার করতে হবে।

- Operator -> `$pullAll`

  ```
  db.test.updateOne(
    {_id: ObjectId("6406ad63fc13ae5a40000065")},
    {$pullAll: {languages: ["Latin", "Thai"]}}
    )
  ```

  - array field থেকে multiple element remove করতে চাইলে `$pullAll` operator use করতে হবে।

## Aggrigation Pipeline Operator

- Operator -> `$match`

  ```
  db.test.aggregate([
  {$match: {age: {$gte: 30}, gender: "Male"}},
  {$project: {age: 1, gender: 1, name: 1, }}
  ])
  ```

  - `$match` operator হলো find operator এর মতো। কিন্তু $match stage আকারে কাজ করে।

- Operator -> `$project`

  ```
  db.test.aggregate([
  {$match: {age: {$gte: 30}, gender: "Male"}},
  {$project: {age: 1, gender: 1, name: 1, }}
  ])
  ```

  - `$project` operator project method এর মতো কাজ করে কিন্তু aggregation এর মধ্যে এটি stage আকারে কাজ করে।

- Operator -> `$addField`

  ```
  db.test.aggregate([
  {$addFields: {course: "Level 2"}},
  ])
  ```

  - এই operator use করে pipeline এর প্রতিটা data এর মধ্যে field add করা যায়। কিন্তু শুধু `$addField` দিয়ে collection এর মধ্যে data কে modifiy করা যায় না। এটা শুধু pipleline এর data এর মধ্যে field add হবে। যদি collection এর মধ্যে data কে modify করতে হয়। তাহলে `$marge` operator use করতে হবে। এবং pipeline এর data গুলো দিয়ে আলাদা collection তৈরী করতে হয় তাহলে `$out` operator use করতে হবে।

- Operator -> `$merge`

  ```db.test.aggregate([
  {$addFields: {course: "Level 2"}},
  {$merge: "test"}
  ])
  ```

  - এখানে test collection এর সকল object data গুলোর মধ্যে course field add করে `$merge` operator use করে, test collection এর সাথে pipeline এর data merge করে দেয়া হয়েছে।

- Operator -> `$out`

  ```db.test.aggregate([
  {$addFields: {course: "Level 2"}},
  {$out: "pipeline_collection"}
  ])
  ```

  - এখানে test collection এর সকল object data গুলোর মধ্যে course field add করে `$out` operator দিয়ে new collection তৈরী হয়ে যাবে।

- Operator -> `$group`

  ```
    db.test.aggregate([
  { $group:{
  _id: "$address.country",
  count: {$sum: 1},
  users: {$push: '$$ROOT'}
  }}
  ])
  ```

  - `$group` operator stage তৈরী করে all document এর মধ্যে group করা যায়। `_id` দিয়ে একটি field declare করতে হবে, ঐ id এর উপর ভিত্তি করে documnet গুলো group হয়ে যাবে।
  - `$group` operator এর মধ্যে কিছু accoumulator operator use করা হয় যেমন: `$sum`, `$count`, `$push`,

  - `$sum` দিয়ে প্রতিটা group এ কত গুলো data আছে তা যোগ করে count করা যায়।
  - `$push` operator দিয়ে group এ কোন field show করবে তা push করা যায়। `{$push: '$$ROOT'}` group wise সকল data গুলো ‍show করবে। কিন্তু নির্দিষ্ট কিছু field show করাতে হলে `$project` stage use করতে হবে।

  ```
  db.test.aggregate([
  {$group: {
      _id: null,
      totalSalary: {$sum: '$salary'},
      minSalary: {$min: "$salary"},
      maxSalary: {$max: "$salary"},
      avgSalary: {$avg: "$salary"}
  }},
  ])
  ```

- `$group` operator এর আরেকটি ব্যবহার হলো `_id: null` দেয়া হয় তাহলে collection এর সকল document কে পাবে। এখানে accoumulator operator

  - `$sum` দিয়ে সকল‍ salary field কে যোগ করা হয়েছে।
  - `$mim` দিয়ে সব গুলোর মধ্যে minimum salary বের করা হয়েছে।
  - `max` দিয়ে maximum salary বের করা হয়েছে।
  - `avg` দিয়ে average salary বের করা হয়েছে।
    এবং field গুলোকে operation করে নতুন field এ রাখা হচ্ছে।

- Operator -> `$project`

  ```
  db.test.aggregate([
  { $group: {
    _id: "$address.country",
    count: {$sum: 1},
    users: {$push: '$$ROOT'}
    }},
  {$project: {
    'users.name': 1,
    'users.age': 1,
    'users.gender':1}}
    ])
  ```

  - এখানে country group এর users এর data গুলোর মধ্যে ‍ specific ৩টা field এর data show করবে।

  ```
    db.test.aggregate([
      {$group: {
          _id: null,
          totalSalary: {$sum: '$salary'},
          minSalary: {$min: "$salary"},
          maxSalary: {$max: "$salary"},
          avgSalary: {$avg: "$salary"}
      }},
      {$project: {
      total: "$totalSalary",
          minSalary: 1,
          max: "$maxSalary",
      avgerage: "$avgSalary",
          differenceMinMax: {$subtract: ["$maxSalary", "$minSalary"]}
      }},
      ])
  ```

  - `$project` operator এর আরেকটি ব্যবহার হলো new field দিয়ে আগের field এ `$fieldName` ব্যবহার করে declare করতে হয়। তাহলে পূর্বের value new field এ বসে যাবে।
  - `$substract` use করে একটি field থেকে আরেকটি field কে বিয়োর করা হয়েছে।

- Operator -> `$unwind`

  ```
   db.test.aggregate([
    { $unwind: "$friends" },
    { $group: { _id: "$friends", count: {$sum: 1} } }
    ])
  ```

  - `$unwind` operator use করে array এর প্রতিটি element কে single element এ রুপান্তর করা হয়। প্রতিটা element নিয়ে আলাদা আলাদা object create হয়।
  - যেমন: `[{id: 1, friend: [a,b,c]}]` -> `[{id: 1, friend: a}, {id: 1, friend: b}, {id: 1, friend:c}]`
  - এখন group করতে চাইলে ‍single element এর উপর group করা যাবে।

  ```
  db.test.aggregate([
    {$unwind: '$interests'},
   {$group: {
    _id: "$age",
    interest: {$push: "$interests"}
    }
   }
  ])
  ```

  - এখানে interests array field কে break করে single elemet এ রুপান্তর করা হয়েছে এবং age এর উপর ভিত্তি করে group করে, প্রতিটি age এর interest গুলো `$push` operator দিয়ে add করে দেয়া হয়েছে।

- Operator -> `$bucket`

  ```
  db.test.aggregate([
      //stage 1
    {$bucket: {
        groupBy: "$age",
        boundaries: [0, 10, 20, 30, 40, 50],
        default: 'remaining',
        output: {
            count: {$sum: 1},
            users: {$push: '$$ROOT'}
        }
    }},

    //stage 2
    {$sort: {count: -1}},

    //stage 3
    {$limit:2},

    //stage 4
    {$project: {"count": 1}}
  ])
  ```

  - `$bucket` operator দিয়ে collection এর মধ্যে নির্দিষ্ট field এর উপর boundary set করে বিভিন্ন ভাগে ভাগ করে document পাওয়া যায়। `$bucket` use করতে কিছু শর্ত পূরণ করতে হবে।
    - groupBy: `$bucket` এর মধ্যে `groupBy` property use করতে হবে। এর মাধ্যমে কোন field এর ভিত্তি করে oparation হবে তা ঠিক করে দেয়।
    - boundaries: `boundaries` property use করতে হবে। কত থেকে কত এর মধ্যে boundary হবে। এখানে [0, 10] = 0 < 10 পযন্ত 0 boundary এর মধ্যে, বাকি গুলো এমন পযায়ক্রমে হবে।
    - default: `default` হলো boundary set করার পরে বাকি যেগুলো থাকবে তা deafult এর মধ্যে set হবে।
    - output: `output` এ define করতে হবে যে কোন field গুলো show করাতে হবে।

- Operator -> `$sort`

  - `$sort` stage এ field এর উপর ভিত্তি করে sort করা যায়।

- Operator -> `$limit`

  - `$limit` stage এ document গুলোকে limit করে পাওয়া যায়। এবং সব সময় `$sort` stage এর পরে করতে হবে।

- Operator -> `$facet`

  ```
  db.test.aggregate([

      {
          $facet: {
              //pipeline-1
              "friendsCount": [
                  //stage-1
                  { $unwind: '$friends' },
                  //stage-2
                  { $group: { _id: '$friends', count: { $sum: 1 } } }
              ],
              //pipeline-2
              "skillsCount": [
                  //stage-1
                  { $unwind: "$skills" },
                  //stage-2
                  { $group: { _id: "$skills", count: { $sum: 1 } } }
              ],
              //pipeline-3
              "interestsCount": [
                  //stage-1
                  {$unwind: "$interests"},
                  //stage-2
                  {$group: {_id: '$interests', count: {$sum: 1} }}
              ]
          }
      }

  ])
  ```

  - `$facet` operator use করে same collection এর উপর একই সময়ে multiple pipeline create করা যায়। এবং প্রতিটা pipeline আলাদা আলাদা output generate করে। প্রতিটা pipeline এর আলাদা আলাদা নাম থাকবে এবং pipeline গুলো মধ্যে multiple stage create করা যাবে।

  - Operator -> `$lookup`

    ```
    db.orders.aggregate([

      {
          $lookup: {
              from: 'test',
              localField: 'userId',
              foreignField: '_id',
              as: 'user'
          }
      }
    ])
    ```

    - `$lookup` operator use করে অন্য collection থেকে referencing এর মাধ্যমে data নিয়ে আসা যায়। অন্য collection একটি ref id এই collection এ রাখা হয় এবং সেই ref Id ধরে data কে নিয়ে আশাই হলো referencing. `$lookup` operato ৪টা প্রপাটির উপর ভিত্তি করে data নিয়ে আসে
      - from: collectionName দিতে হয়
      - localField: এই collection এ reference property কি নামে আছে।
      - foreign: যে collection থেকে data আনা হবে সেখানে property কি নামে আছে।
      - as: কি নামের property তে data গুলো রাখা হবে।
