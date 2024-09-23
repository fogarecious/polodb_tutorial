# Creating Indexes

We can create indexes for better searching performance.
Without an index, [PoloDB](https://github.com/PoloDB/PoloDB) has to read all documents to search for a particular document.
Indexes let [PoloDB](https://github.com/PoloDB/PoloDB) read less documents while it is looking for some documents.

We use [create_index](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.create_index) to create an index.

```rust
collection.create_index(IndexModel {keys: doc! {"Age": 1}, options: None,}).unwrap();
```

Method [create_index](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.create_index) needs an [IndexModel](https://docs.rs/polodb_core/latest/polodb_core/struct.IndexModel.html), which needs `keys` and `options`.
`keys` are the entry names that we would like to build an index on.
We specify `doc! {"Age": 1}` here, where `1` indicates that the entry is sorted in ascending order.
`options` will be introduced later.

The complete code is shown below:

```rust
use polodb_core::{bson::doc, Database, IndexModel};

fn main() {
    let db = Database::open_memory().unwrap();
    let collection = db.collection("name_of_the_collection");
    
    collection
        .create_index(IndexModel {
            keys: doc! {
                "Age": 1,
            },
            options: None,
        })
        .unwrap();
    
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
    
    let docs_found = collection
        .find(doc! {
            "Age": doc! {"$eq": 20}
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
        "Bob",
    ),
    "Age": Int32(
        20,
    ),
    "_id": ObjectId(
        "66f1591edb03e4fd392164e6",
    ),
})
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
