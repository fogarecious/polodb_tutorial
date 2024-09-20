# Deleting At Most One Document

Similar to [find_one](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.find_one) and [update_one](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.update_one), we have [delete_one](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.delete_one), which deletes at most one selected document.

```rust
collection.delete_one(doc! {"Category": "Blue box"}).unwrap();
```

The example above selects documents with entry `"Category": "Blue box"` and deletes the first selected document.

The complete code is shown below:

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
        .delete_one(doc! {"Category": "Blue box"})
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
DeleteResult { deleted_count: 1 }
Document({
    "Category": String(
        "Blue box",
    ),
    "Price": Int32(
        2,
    ),
    "_id": ObjectId(
        "66e3fb3c82994f4cca2de956",
    ),
})
Document({
    "Category": String(
        "Yellow box",
    ),
    "Price": Int32(
        3,
    ),
    "_id": ObjectId(
        "66e3fb3c82994f4cca2de957",
    ),
})
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
