# Any One In An Array

We can specify an array of values and retrieve the documents with the entry that satisfies any of these values.

```rust
collection.find(doc! {"Age": {"$in": [3, 10, 21]}}).unwrap()
```

The example above finds the documents that has `Age` being `3`, `10` or `21`.

The complete code is presented below:

```rust
use polodb_core::{bson::doc, Database};

fn main() {
    let db = Database::open_memory().unwrap();
    let collection = db.collection("name_of_the_collection");

    let docs = [
        doc! {
            "Name": "Alice",
            "Age": 21,
            "Height": 190,
        },
        doc! {
            "Name": "Bob",
            "Age": 20,
            "Height": 180,
        },
        doc! {
            "Name": "Cat",
            "Age": 3,
        },
    ];
    collection.insert_many(docs).unwrap();

    let docs_found = collection.find(doc! {"Age": {"$in": [3, 10, 21]}}).unwrap();
    for doc in docs_found {
        println!("{:#?}", doc.unwrap());
    }
}
```

Output:

```text
Document({
    "Name": String(
        "Alice",
    ),
    "Age": Int32(
        21,
    ),
    "Height": Int32(
        190,
    ),
    "_id": ObjectId(
        "66ba27972b81c79e2d5dad2d",
    ),
})
Document({
    "Name": String(
        "Cat",
    ),
    "Age": Int32(
        3,
    ),
    "_id": ObjectId(
        "66ba27972b81c79e2d5dad2f",
    ),
})
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
