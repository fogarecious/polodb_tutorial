# Updating At Most One Document

In contrast to [update_many](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.update_many), we can use [update_one](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.update_one) to update at most one document.

```rust
collection.update_one(doc! {"Color": "Blue"}, doc! {"$set": {"State": "Sold out"}}).unwrap();
```

The example above selects documents with `Color` `Blue` and at most one of them will have entry `"State": "Sold out"` added.

The complete code is here:

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
        .update_one(doc! {"Color": "Blue"}, doc! {"$set": {"State": "Sold out"}})
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
UpdateResult { modified_count: 1 }
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
        "66e3f08117e7db0ddfb6ec9a",
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
        "66e3f08117e7db0ddfb6ec9b",
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
        "66e3f08117e7db0ddfb6ec9c",
    ),
})
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
