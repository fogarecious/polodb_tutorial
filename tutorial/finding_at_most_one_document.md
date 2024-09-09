# Finding At Most One Document

Previously, we use [find](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.find) to find all the documents that satisfy the given entry conditions.
We can restrict ourselves to find only at most one document by [find_one](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.find_one).

```rust
collection.find_one(doc! {"Age": {"$gt": 10}}).unwrap();
```

The example above finds the first document that has `Age` more than `10`.

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
        },
        doc! {
            "Name": "Bob",
            "Age": 20,
        },
        doc! {
            "Name": "Cat",
            "Age": 3,
        },
    ];
    collection.insert_many(docs).unwrap();
    
    let doc_found = collection.find_one(doc! {"Age": {"$gt": 10}}).unwrap();
    println!("{:#?}", doc_found.unwrap());
}
```

Now that there is at most one returned document, we do not need to use a for loop to go through all the documents.
Instead, we can manipulate the returned document directly.

Output:

```text
Document({
    "Name": String(
        "Alice",
    ),
    "Age": Int32(
        21,
    ),
    "_id": ObjectId(
        "66d843923f8193105d066f6a",
    ),
})
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
