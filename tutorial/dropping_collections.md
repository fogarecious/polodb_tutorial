# Dropping Collections

To drop a collection, we can use [drop](https://docs.rs/polodb_core/latest/polodb_core/trait.CollectionT.html#tymethod.drop) of [Collection](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html).

In the following example, we first create a collection and then drop it.

```rust
use polodb_core::{bson::Document, Collection, Database};

fn main() {
    let db = Database::open_memory().unwrap();

    db.create_collection("name_of_the_collection").unwrap();
    println!("{:?}", db.list_collection_names());

    let collection: Collection<Document> = db.collection("name_of_the_collection");
    collection.drop().unwrap();
    println!("{:?}", db.list_collection_names());
}
```

Output:

```text
Ok(["name_of_the_collection"])
Ok([])
```

:arrow_right:  Next: [Inserting A Document](./inserting_a_document.md)

:blue_book: Back: [Table of contents](./../README.md)
