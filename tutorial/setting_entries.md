# Setting Entries

We can update existing documents by [update_many](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.update_many).
The method [update_many](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.update_many) takes two parameters: one is for querying documents (like we do in method [find](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.find) before), and the other is for updating the documents found.

```rust
collection.update_many(doc! {"Color": "Blue"}, doc! {"$set": {"Type": "Blue box"}}).unwrap();
```

The example above finds documents with `Color` being `Blue` and updates these documents by setting their `Type` to `Blue box`.
We use `$set` to specify that we would like to replace entries.

The complete code is presented below:

```rust
use polodb_core::{bson::doc, Database};

fn main() {
    let db = Database::open_memory().unwrap();
    let collection = db.collection("name_of_the_collection");
    
    let docs = [
        doc! {
            "Type": "Box",
            "Color": "Blue",
            "Price": 1,
        },
        doc! {
            "Type": "Box",
            "Color": "Blue",
            "Price": 2,
        },
        doc! {
            "Type": "Box",
            "Color": "Yellow",
            "Price": 3,
        },
    ];
    collection.insert_many(docs).unwrap();
    
    let result = collection
        .update_many(doc! {"Color": "Blue"}, doc! {"$set": {"Type": "Blue box"}})
        .unwrap();
    println!("{:?}", result);

    let docs_found = collection.find(None).unwrap();
    for doc in docs_found {
        println!("{:#?}", doc.unwrap());
    }
}
```

Output:

```text
UpdateResult { modified_count: 2 }
Document({
    "Type": String(
        "Blue box",
    ),
    "Color": String(
        "Blue",
    ),
    "Price": Int32(
        1,
    ),
    "_id": ObjectId(
        "66d994c35afa8f112e525341",
    ),
})
Document({
    "Type": String(
        "Blue box",
    ),
    "Color": String(
        "Blue",
    ),
    "Price": Int32(
        2,
    ),
    "_id": ObjectId(
        "66d994c35afa8f112e525342",
    ),
})
Document({
    "Type": String(
        "Box",
    ),
    "Color": String(
        "Yellow",
    ),
    "Price": Int32(
        3,
    ),
    "_id": ObjectId(
        "66d994c35afa8f112e525343",
    ),
})
```

We can also use [update_many](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.update_many) to add new entries.

```rust
let result = collection
    .update_many(doc! {"Color": "Blue"}, doc! {"$set": {"State": "Sold out"}})
    .unwrap();
```

Output:

```text
UpdateResult { modified_count: 2 }
Document({
    "Type": String(
        "Box",
    ),
    "Color": String(
        "Blue",
    ),
    "Price": Int32(
        1,
    ),
    "_id": ObjectId(
        "66d99651207eec89c1c533c0",
    ),
    "State": String(
        "Sold out",
    ),
})
Document({
    "Type": String(
        "Box",
    ),
    "Color": String(
        "Blue",
    ),
    "Price": Int32(
        2,
    ),
    "_id": ObjectId(
        "66d99651207eec89c1c533c1",
    ),
    "State": String(
        "Sold out",
    ),
})
Document({
    "Type": String(
        "Box",
    ),
    "Color": String(
        "Yellow",
    ),
    "Price": Int32(
        3,
    ),
    "_id": ObjectId(
        "66d99651207eec89c1c533c2",
    ),
})
```

:arrow_right:  Next: [Upper Limits / Lower Limits](./upper_limits_lower_limits.md)

:blue_book: Back: [Table of contents](./../README.md)
