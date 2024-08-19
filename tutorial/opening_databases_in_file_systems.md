# Opening Databases In File Systems

We can also open a database that is stored in the file system.
To do this, we use [open_file](https://docs.rs/polodb_core/latest/polodb_core/struct.Database.html#method.open_file) of [Database](https://docs.rs/polodb_core/latest/polodb_core/struct.Database.html)

```rust
let db = Database::open_file("some_file.db").unwrap();
```

where `some_file.db` is the filename of the opened database.
In debug mode, this file will be created in the project root folder.

Let's try to replace [open_memory](https://docs.rs/polodb_core/4.4.2/polodb_core/struct.Database.html#method.open_memory) with [open_file](https://docs.rs/polodb_core/latest/polodb_core/struct.Database.html#method.open_file) in the [First Example](./first_example.md).

```rust
use polodb_core::{bson::doc, Database};

fn main() {
    let db = Database::open_file("contacts.db").unwrap();
    let contacts = db.collection("contacts");

    let john = doc! {
        "Name": "John",
        "Age": 20,
    };

    contacts.insert_one(john).unwrap();

    let people = contacts.find(None).unwrap();
    for person in people {
        println!("{:#?}", person.unwrap());
    }
}
```

After running the program, we get the output:

```text
Document({
    "Name": String(
        "John",
    ),
    "Age": Int32(
        20,
    ),
    "_id": ObjectId(
        "66c32ee1144f3bb99d9aa078",
    ),
})
```

We can also see that the file `contacts.db` is created.
By re-running the program, we should see from the output that there are two documents.

```text
Document({
    "Name": String(
        "John",
    ),
    "Age": Int32(
        20,
    ),
    "_id": ObjectId(
        "66c32ee1144f3bb99d9aa078",
    ),
})
Document({
    "Name": String(
        "John",
    ),
    "Age": Int32(
        20,
    ),
    "_id": ObjectId(
        "66c32f081ab12fee7e1b7419",
    ),
})
```

This is because the program reads a document from the file that is created when we run the program at the first time, and then we insert another document at the second run.

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
