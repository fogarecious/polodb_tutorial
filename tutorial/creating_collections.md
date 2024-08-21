# Creating Collections

A database may have many collections.
To create a collection, we use [create_collection](https://docs.rs/polodb_core/latest/polodb_core/struct.Database.html#method.create_collection)

```rust
let db = Database::open_memory().unwrap();
db.create_collection("name_of_the_collection").unwrap();
```

where `name_of_the_collection` is the name (of the created collection) that is used for accessing the collection later.

The other way to create a collection is by using [collection](https://docs.rs/polodb_core/latest/polodb_core/struct.Database.html#method.collection).

```rust
let db = Database::open_memory().unwrap();
let collection = db.collection("name_of_the_collection");
```

Yet, this method does not actually create a collection.
It only creates a collection after a document is inserted.

Sometimes, we need to specify explicitly a type of [Collection](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html).
In this case, we can use [Collection](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html)<[Document](https://docs.rs/bson/latest/bson/struct.Document.html)>, which is also the default type of [Collection](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html).

```rust
use polodb_core::{bson::Document, Collection, Database};

fn main() {
    let db = Database::open_memory().unwrap();
    let _collection: Collection<Document> = db.collection("name_of_the_collection");
}
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
