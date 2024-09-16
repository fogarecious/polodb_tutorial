# Renaming Entries

Previously, we use `$set` to change entry values.
To change entry names, we can use `$rename`.

```rust
collection.update_many(doc! {"Price": {"$lte": 10}}, doc! {"$rename": doc! {"Type": "Category"}}).unwrap();
```

The example above selects the documents with `Price` being at most `10` and updates their entry names from `Type` to `Category`.

The complete code is given below:

```rust
use polodb_core::{bson::doc, Database};

fn main() {
    let db = Database::open_memory().unwrap();
    let collection = db.collection("name_of_the_collection");

    let docs = [
        doc! {
            "Type": "Box",
            "Price": 1,
        },
        doc! {
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
        .update_many(
            doc! {"Price": {"$lte": 10}},
            doc! {"$rename": doc! {"Type": "Category"}},
        )
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
    "Price": Int32(
        1,
    ),
    "_id": ObjectId(
        "66e3ebed70920585c379257a",
    ),
    "Category": String(
        "Box",
    ),
})
Document({
    "Price": Int32(
        10,
    ),
    "_id": ObjectId(
        "66e3ebed70920585c379257b",
    ),
    "Category": String(
        "Box",
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
        "66e3ebed70920585c379257c",
    ),
})
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
