# Unique Entries

When creating indexes by [create_index](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.create_index), we can pass an [IndexOptions](https://docs.rs/polodb_core/latest/polodb_core/struct.IndexOptions.html) to `options`.

```rust
collection.create_index(IndexModel {keys: doc! {"Name": 1}, options: Some(IndexOptions {unique: Some(true), ..Default::default()})}).unwrap();
```

In [IndexOptions](https://docs.rs/polodb_core/latest/polodb_core/struct.IndexOptions.html), we can set `unique` to `Some(true)` to require the uniqueness of the entry.

Here is the complete code:

```rust
use polodb_core::{bson::doc, Database, IndexModel, IndexOptions};

fn main() {
    let db = Database::open_memory().unwrap();
    let collection = db.collection("name_of_the_collection");

    collection
        .create_index(IndexModel {
            keys: doc! {
                "Name": 1,
            },
            options: Some(IndexOptions {
                unique: Some(true),
                ..Default::default()
            }),
        })
        .unwrap();
    
    let result = collection.insert_one(doc! {"Name": "Bob"});
    println!("{:?}", result);

    let result = collection.insert_one(doc! {"Name": "Bob"});
    println!("{:?}", result);
}
```

Output:

```text
Ok(InsertOneResult { inserted_id: ObjectId("66f15ee26a6ba31a4ddd7bef") })
Err(DuplicateKey(DuplicateKeyError { name: "Name_1", key: "\"Bob\"", ns: "name_of_the_collection" }))
```

In the example, when we add a repeated entry, it throws an error.

:arrow_right:  Next: [Dropping Indexes](./dropping_indexes.md)

:blue_book: Back: [Table of contents](./../README.md)
