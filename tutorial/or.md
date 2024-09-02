# Or

Sometimes, we want to specify several entry conditions and find the documents that satisfy any of the conditions.
In this case, we can use `$or`.

```rust
collection.find(doc! { "$or": [{ "Age": 3 }, { "Height": 190 }]}).unwrap()
```

In the example above, we retrieve the documents that have `Age` equal to `3` or have `Height` equal to `190`.
Additionally, we can add more such conditions as many as we like.

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

    let docs_found = collection
        .find(doc! {
            "$or": [
                { "Age": 3 },
                { "Height": 190 },
            ],
        })
        .unwrap();
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
        "66b61a9ec02e7e0e4b35e0a0",
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
        "66b61a9ec02e7e0e4b35e0a2",
    ),
})
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
