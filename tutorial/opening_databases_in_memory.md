# Opening Databases In Memory

To open a database in memory, we can use [open_memory()](https://docs.rs/polodb_core/4.4.2/polodb_core/struct.Database.html#method.open_memory) of [Database](https://docs.rs/polodb_core/latest/polodb_core/struct.Database.html).

```rust
let db = Database::open_memory().unwrap();
```

After opening the database, we can use the variable, `db`, to manipulate the database.

:arrow_right:  Next: [Opening Databases In File Systems](./opening_databases_in_file_systems.md)

:blue_book: Back: [Table of contents](./../README.md)
