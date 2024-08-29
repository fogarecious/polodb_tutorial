# Finding All Documents

We can use [find](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.find) of [Collection](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html) to retrieve all documents in a collection.
The method [find](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.find) receives a parameter for filters.
Currently, we can use [None](https://doc.rust-lang.org/std/option/enum.Option.html#variant.None) for *no filters*.
We then use a for loop to go through all the documents found.

```rust
let docs_found = collection.find(None).unwrap();
for doc in docs_found {
    println!("{:#?}", doc.unwrap());
}
```

The complete code is provided below:

```rust
use polodb_core::{bson::doc, Database};

fn main() {
    let db = Database::open_memory().unwrap();
    let collection = db.collection("name_of_the_collection");

    let docs = [
        doc! {
            "Name": "Alice",
            "Age": 20,
        },
        doc! {
            "Name": "Bob",
            "Height": 180,
        },
    ];
    collection.insert_many(docs).unwrap();
    
    let docs_found = collection.find(None).unwrap();
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
    "_id": ObjectId(
        "66b610fb9d9613d5f5533aa5",
    ),
})
Document({
    "Name": String(
        "Bob",
    ),
    "Height": Int32(
        180,
    ),
    "_id": ObjectId(
        "66b610fb9d9613d5f5533aa6",
    ),
})
```

For each document, there is an entry `_id`, which is the unique id of the document and is created automatically.

:arrow_right:  Next: [By An Entry](./by_an_entry.md)

:blue_book: Back: [Table of contents](./../README.md)
