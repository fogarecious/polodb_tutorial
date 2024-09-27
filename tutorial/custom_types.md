# Custom Types

Instead of using [doc!](https://docs.rs/bson/latest/bson/macro.doc.html) to add documents, we can use our own custom types.

First, we need to add [serde](https://docs.rs/serde/latest/serde/).

```sh
cargo add serde
```

The dependencies of `Cargo.toml` file should look like this:

```toml
[dependencies]
polodb_core = "4.4.2"
serde = "1.0.210"
```

Then, we declare our `struct`s that derive [Serialize](https://docs.rs/serde/latest/serde/trait.Serialize.html) and [Deserialize](https://docs.rs/serde/latest/serde/trait.Deserialize.html).

```rust
#[derive(Debug, Serialize, Deserialize)]
struct Student {
    name: String,
    age: u8,
}
```

Finally, we can add instances of the `struct` to our `collection`.

The complete code is presented below:

```rust
use polodb_core::{bson::doc, Database};
use serde::{Deserialize, Serialize};

#[derive(Debug, Serialize, Deserialize)]
struct Student {
    name: String,
    age: u8,
}

fn main() {
    let db = Database::open_memory().unwrap();
    let collection = db.collection("name_of_the_collection");

    let docs = vec![
        Student {
            name: "Alice".to_string(),
            age: 21,
        },
        Student {
            name: "Bob".to_string(),
            age: 20,
        },
        Student {
            name: "Cat".to_string(),
            age: 3,
        },
    ];
    collection.insert_many(docs).unwrap();

    let docs_found = collection.find(doc! {"name": "Bob"}).unwrap();
    for doc in docs_found {
        println!("{:#?}", doc.unwrap());
    }
}
```

Output:

```text
Student {
    name: "Bob",
    age: 20,
}
```

Note that the current entry name is in lowercase.

:arrow_right:  Next: [Transactions](./transactions.md)

:blue_book: Back: [Table of contents](./../README.md)
