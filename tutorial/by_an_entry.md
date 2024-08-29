# By An Entry

A document may have many entries such as `Name`, `Age`, `Height`, etc.
Sometimes, several documents would have the common entry.
We can search for these documents if we know the entry name and value.

```rust
collection.find(doc! {"Name": "Bob"}).unwrap();
```

To search for the documents, we use [find](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.find) with [doc!](https://docs.rs/bson/latest/bson/macro.doc.html) as its parameter.
In the example above, we specify an entry with name `Name` and value `Bob` in [doc!](https://docs.rs/bson/latest/bson/macro.doc.html).
This will return all the documents that have such an entry.
And then we can access the other entries of these documents.

The complete code is presented below:

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

    let docs_found = collection.find(doc! {"Name": "Bob"}).unwrap();
    for doc in docs_found {
        println!("{:#?}", doc.unwrap());
    }
}
```

Output:

```text
Document({
    "Name": String(
        "Bob",
    ),
    "Height": Int32(
        180,
    ),
    "_id": ObjectId(
        "66b613e6d08028e445046942",
    ),
})
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
