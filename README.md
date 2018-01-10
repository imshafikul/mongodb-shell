# mongodb-shell
MongoDB Shell command to read, create, delete and update Data

Please read official documentation and installation guide from MongoDB [official site](https://docs.mongodb.com/getting-started/shell/installation/)

## Show all Database
```
$ show dbs;
```

## Use a Database
```
$ use {your_database_name}
```
## Check Current Database
```
$ db;
```

## Create new user in a Database
```
db.createUser({
    user: "sumon",
    pwd: "sumon",
    roles: ["readWrite"]
});
```

## Create collection [collection is like table in relational database]
```
$ db.createCollection('customers');
// here db reffer the current database
```

## Check all colections in current Database
```
$ show collections;
```
## Add / Insert an item into a collection
```
db.customers.insert({first_name: "Shafikul", last_name: "Islam", age: 26});
```

## On relational database we can only add define field value , in nosql database it is ok add new key and value 
```
db.customers.insert([
    {first_name: "Hridoy", last_name: "Khan", age: 21},
    {first_name: "Simla", last_name: "Akter", age: 26, gender: "female"}
]);
```

## Find all data within a collection
```
db.customers.find();
```
```
// For more readable 
db.customers.find().pretty();
```

## Update an entry 
```
db.customers.update({first_name: "shafikul"}, {first_name: "Shafikul", last_name: "Islam", age: 27, gender: "male"});
// First object for search the item and second object is data need to update
```
## Use $set
```
db.customers.update({first_name: "Hridoy"}, {
  $set: {
    gender: "Male"
  }
});
```
## use $inc {Increment the existing age value with new value}
```
db.customers.update({first_name: "Hridoy"}, {
  $inc: {
    age: 2
  }
});
```
## Use $unset {remove a key}

## If we try update an item , but this is not there in collection, we can add if not exsist {Using additional option upsert}
```
db.customers.update({first_name: "Ethila"}, {
    first_name: "Ethila",
    last_name: "Akter",
    age: 8
},
{
    upsert: true
});
```

## Rename a key within an entry
```
db.customers.update({first_name: "Ethila"}, {
    $rename: {
  "first_name": "nick_name"
    }
});
```

## Remove an item from an collection
```
db.customers.remove({first_name: "Shafikul"});
```
```
//If collection has multiple entry with name "Shafikul",  But we want to delete one item. We can easily handle by add an additional option
db.customers.remove({first_name: "Shafikul"}, {justOne: true});
```

## Remove all within a collection
```
db.customers.remove({});
```

## Find with `or` condition
```
db.customers.find({$or:[{first_name: "Shafikul"},{first_name: "Hridoy"}]});
```

## find with greater then & less then & greater then or equal & less then or equal (`$gt` & `$lt` & `$gte` & `$lte`)
```
db.customers.find({ age: {$gt: 10} });
db.customers.find({ age: {$lt: 30} });
db.customers.find({ age: {$gte: 10} });
db.customers.find({ age: {$lte: 30} });
```

##  Find by nested object value
```
db.customers.find({"address.country": "Bangladesh"});
```

## Find by nested array value
```
db.customers.find({"friends.name": "Shaun"});
```

## Sorting when find
```
db.customers.find().sort({first_name: 1});  
// 1 means ascending order
// -1 for decending order
db.customers.find().sort({first_name: -1});
```

## Count Entry within a collection
```
db.customers.find().count(); 
// count all entry


// count all entry where gender is male
db.customers.find({gender: "male"}).count(); 
```

## Limit 
```
db.customers.find().limit(4); 
// return first 4 entry
```



