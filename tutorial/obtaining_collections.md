# Obtaining Collections

To obtain a collection, we use [collection](https://docs.rs/polodb_core/latest/polodb_core/struct.Database.html#method.collection) of [Database](https://docs.rs/polodb_core/latest/polodb_core/struct.Database.html).

```rust
let db = Database::open_memory().unwrap();
let collection = db.collection("name_of_the_collection");
```

If we do not know the name of a collection, we can use [list_collection_names](https://docs.rs/polodb_core/latest/polodb_core/struct.Database.html#method.list_collection_names) of [Database](https://docs.rs/polodb_core/latest/polodb_core/struct.Database.html) to see all the collection names.

```rust
let db = Database::open_memory().unwrap();
db.create_collection("collection 1").unwrap();
db.create_collection("collection 2").unwrap();
println!("{:?}", db.list_collection_names());
```

Output:

```text
Ok(["collection 1", "collection 2"])
```

:arrow_right:  Next: [Dropping Collections](./dropping_collections.md)

:blue_book: Back: [Table of contents](./../README.md)
