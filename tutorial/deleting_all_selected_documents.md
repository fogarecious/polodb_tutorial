# Deleting All Selected Documents

The method [delete_many](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.delete_many) finds documents and delete them.

```rust
collection.delete_many(doc! {"Category": "Blue box"}).unwrap();
```

The example above selects documents with entry `"Category": "Blue box"` and deletes them.

Here is the complete code:

```rust
use polodb_core::{bson::doc, Database};

fn main() {
    let db = Database::open_memory().unwrap();
    let collection = db.collection("name_of_the_collection");

    let docs = [
        doc! {
            "Category": "Blue box",
            "Price": 1,
        },
        doc! {
            "Category": "Blue box",
            "Price": 2,
        },
        doc! {
            "Category": "Yellow box",
            "Price": 3,
        },
    ];
    collection.insert_many(docs).unwrap();

    let result = collection
        .delete_many(doc! {"Category": "Blue box"})
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
DeleteResult { deleted_count: 2 }
Document({
    "Category": String(
        "Yellow box",
    ),
    "Price": Int32(
        3,
    ),
    "_id": ObjectId(
        "66e3fa369d5d8926ea15f837",
    ),
})
```

The conditions passed to [delete_many](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.delete_many) are the same as we used for [find](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.find).

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
