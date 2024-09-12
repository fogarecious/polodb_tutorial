# Increasing Entries

If entry values are numbers, we can add an amount to the values of the selected documents.

```rust
collection.update_many(doc! {"Color": "Blue"}, doc! {"$inc": doc! {"Price": 5}}).unwrap();
```

The example above increases `Price` of the entries with `Color` `Blue` by `5`.

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
            "Price": 10,
        },
        doc! {
            "Type": "Box",
            "Color": "Yellow",
            "Price": 20,
        },
    ];
    collection.insert_many(docs).unwrap();

    let result = collection
        .update_many(doc! {"Color": "Blue"}, doc! {"$inc": doc! {"Price": 5}})
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
        "Box",
    ),
    "Color": String(
        "Blue",
    ),
    "Price": Int32(
        6,
    ),
    "_id": ObjectId(
        "66dac3a6db06a8ddebb868b7",
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
        15,
    ),
    "_id": ObjectId(
        "66dac3a6db06a8ddebb868b8",
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
        20,
    ),
    "_id": ObjectId(
        "66dac3a6db06a8ddebb868b9",
    ),
})
```

Note that negative increments, say `-5`, are also possible.

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
