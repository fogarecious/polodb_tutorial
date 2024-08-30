# And

When we search in documents with filters, we can combine two or more entries.
This will retrieve the documents satisfying all these entries.

```rust
collection.find(doc! {"Age": 20, "Height": 190}).unwrap();
```

In the following example, we have two documents that share the same entry `"Age": 20`.
By combining the entry to another entry `"Height": 190`, we can filter the documents further.

```rust
use polodb_core::{bson::doc, Database};

fn main() {
    let db = Database::open_memory().unwrap();
    let collection = db.collection("name_of_the_collection");
    
    let docs = [
        doc! {
            "Name": "Alice",
            "Age": 20,
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

    let docs_found = collection.find(doc! {"Age": 20, "Height": 190}).unwrap();
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
        20,
    ),
    "Height": Int32(
        190,
    ),
    "_id": ObjectId(
        "66b61855180511f2717e90bf",
    ),
})
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
