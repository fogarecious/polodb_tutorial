# Dropping Indexes

We can use [drop_index](https://docs.rs/polodb_core/latest/polodb_core/trait.CollectionT.html#tymethod.drop_index) to remove an index.

```rust
collection.drop_index("Name_1").unwrap();
```

By default, an index name is the entry name with `_1` appended.
We can change the index name by `options` when we create an index.

The complete code is shown below:

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
    
    collection.drop_index("Name_1").unwrap();

    let result = collection.insert_one(doc! {"Name": "Bob"});
    println!("{:?}", result);

    let result = collection.insert_one(doc! {"Name": "Bob"});
    println!("{:?}", result);
}
```

Output:

```text
Ok(InsertOneResult { inserted_id: ObjectId("66f160eeaf31a48fb03e3710") })
Ok(InsertOneResult { inserted_id: ObjectId("66f160eeaf31a48fb03e3711") })
```

Without the uniqueness constraint, we can add duplicated data.

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
