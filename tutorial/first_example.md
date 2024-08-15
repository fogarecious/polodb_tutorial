# First Example

Here is an example code of [PoloDB](https://github.com/PoloDB/PoloDB):

```rust
use polodb_core::{bson::doc, Database};

fn main() {
    let db = Database::open_memory().unwrap();
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

It opens a database in memory, inserts a document into the database and queries all inserted documents.

Output:

```text
Document({
    "Name": String(
        "John",
    ),
    "Age": Int32(
        20,
    ),
    "_id": ObjectId(
        "66bc9e1e13dbc06f151d08b1",
    ),
})
```

We will explain every parts of the example in detail later.

:arrow_right:  Next: [Databases, Collections And Documents](./databases_collections_and_documents.md)

:blue_book: Back: [Table of contents](./../README.md)
