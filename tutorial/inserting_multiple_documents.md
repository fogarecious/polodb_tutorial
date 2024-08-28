# Inserting Multiple Documents

The method [insert_one](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.insert_one) can only insert one document at a time.
To insert multiple documents, we can call [insert_one](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.insert_one) repeatedly over all documents.
Or we can use [insert_many](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.insert_many) for better performance.

```rust
collection.insert_many(/* multiple documents */).unwrap();
```

The method [insert_many](https://docs.rs/polodb_core/latest/polodb_core/struct.Collection.html#method.insert_many) accepts an array of documents.
We can put the documents inside `[]` and `vec!`.

```rust
collection.insert_many([/* doc 1 */, /* doc 2 */, /* etc */]).unwrap();
```

In the following example, we insert two documents to a collection at a time.

```rust
use polodb_core::{bson::doc, Database};

fn main() {
    let db = Database::open_memory().unwrap();
    let collection = db.collection("name_of_the_collection");
    
    let docs = [
        doc! {
            "Name": "Alice",
            "Age": 20,
        },
        doc! {
            "Name": "Bob",
            "Height": 180,
        },
    ];
    let result = collection.insert_many(docs).unwrap();

    println!("{:?}", result);
}
```

Output:

```text
InsertManyResult { inserted_ids: {0: ObjectId("66b4cbac508a17ca0d9e5b57"), 1: ObjectId("66b4cbac508a17ca0d9e5b58")} }
```

Note that documents can contain different entries (such as `Age` and `Height`) even if they are inserted together.

:arrow_right:  Next: [Finding All Documents](./finding_all_documents.md)

:blue_book: Back: [Table of contents](./../README.md)
