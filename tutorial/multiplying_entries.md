# Multiplying Entries

If entry values are numbers, we can multiply selected entry values by a given number.

```rust
collection.update_many(doc! {"Color": "Blue"}, doc! {"$mul": doc! {"Price": 3}}).unwrap();
```

The example above multiplies `Price` by `3` for entries with `Color` `Blue`.

The complete code is shown below:

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
        .update_many(doc! {"Color": "Blue"}, doc! {"$mul": doc! {"Price": 3}})
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
        3,
    ),
    "_id": ObjectId(
        "66e3e9528b1b7b201dcf7391",
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
        30,
    ),
    "_id": ObjectId(
        "66e3e9528b1b7b201dcf7392",
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
        "66e3e9528b1b7b201dcf7393",
    ),
})
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
