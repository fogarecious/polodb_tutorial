# Inserting A Document

We can use [insert_one](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.insert_one) to insert a document to a [Collection](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html).

```rust
collection.insert_one(/* a document */).unwrap();
```

For creating a document, a convenient way is to use [doc!](https://docs.rs/bson/latest/bson/macro.doc.html).
The macro [doc!](https://docs.rs/bson/latest/bson/macro.doc.html) transforms a [JSON](https://www.json.org/json-en.html) text to a rust type.

```rust
collection.insert_one(doc! {
    "Name": "John",
    "Age": 21,
}).unwrap();
```

In the [JSON](https://www.json.org/json-en.html) text above, we have two entries: `Name` and `Age`, which have value `John` and `21` respectively.

Here is the complete example:

```rust
use polodb_core::{bson::doc, Database};

fn main() {
    let db = Database::open_memory().unwrap();
    let collection = db.collection("name_of_the_collection");

    let result = collection
        .insert_one(doc! {
            "Name": "John",
            "Age": 21,
        })
        .unwrap();
    
    println!("{:?}", result);
}
```

Output:

```text
InsertOneResult { inserted_id: ObjectId("66b3bc1e5c6165633b65f593") }
```

:arrow_right:  Next: [Inserting Multiple Documents](./inserting_multiple_documents.md)

:blue_book: Back: [Table of contents](./../README.md)
