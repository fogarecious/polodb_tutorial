# Removing Entries

We can use `$unset` to remove an entry of selected documents.

```rust
collection.update_many(doc! {"Type": "Box"}, doc! {"$unset": doc! {"Type": ""}}).unwrap();
```

The example above selects documents with `Type` of `Box` and removes the entry `Type` from the documents.

The complete code is shown here:

```rust
use polodb_core::{bson::doc, Database};

fn main() {
    let db = Database::open_memory().unwrap();
    let collection = db.collection("name_of_the_collection");

    let docs = [
        doc! {
            "Category": "Box",
            "Type": "Box",
            "Price": 1,
        },
        doc! {
            "Category": "Box",
            "Type": "Box",
            "Price": 10,
        },
        doc! {
            "Category": "Box",
            "Price": 20,
        },
    ];
    collection.insert_many(docs).unwrap();

    let result = collection
        .update_many(doc! {"Type": "Box"}, doc! {"$unset": doc! {"Type": ""}})
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
    "Category": String(
        "Box",
    ),
    "Price": Int32(
        1,
    ),
    "_id": ObjectId(
        "66e3ee68de29cc9a4a992cf3",
    ),
})
Document({
    "Category": String(
        "Box",
    ),
    "Price": Int32(
        10,
    ),
    "_id": ObjectId(
        "66e3ee68de29cc9a4a992cf4",
    ),
})
Document({
    "Category": String(
        "Box",
    ),
    "Price": Int32(
        20,
    ),
    "_id": ObjectId(
        "66e3ee68de29cc9a4a992cf5",
    ),
})
```

:arrow_right:  Next: [Updating At Most One Document](./updating_at_most_one_document.md)

:blue_book: Back: [Table of contents](./../README.md)
