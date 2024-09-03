# Greater Than / Less Than

If values of an entry are numbers, we can compare the sizes of the values when we retrieve documents.
We can filter the documents that have the entry value larger (or smaller) than a given entry value.

```rust
collection.find(doc! {"Height": {"$gt": 185}}).unwrap();
```

The example above finds the documents with `Height` larger than `185`.

In addition to `$gt`, we can use `$lt` for *less than*, `$gte` for *greater than or equal to*, and `$lte` for *less than or equal to*.

The complete code is presented below:

```rust
use polodb_core::{bson::doc, Database};

fn main() {
    let db = Database::open_memory().unwrap();
    let collection = db.collection("name_of_the_collection");

    let docs = [
        doc! {
            "Name": "Alice",
            "Age": 21,
            "Height": 190,
        },
        doc! {
            "Name": "Bob",
            "Age": 20,
            "Height": 180,
        },
        doc! {
            "Name": "Cat",
            "Age": 3,
        },
    ];
    collection.insert_many(docs).unwrap();

    let docs_found = collection.find(doc! {"Height": {"$gt": 185}}).unwrap();
    for doc in docs_found {
        println!("{:#?}", doc.unwrap());
    }
}
```

Output:

```text
Document({
    "Name": String(
        "Alice",
    ),
    "Age": Int32(
        21,
    ),
    "Height": Int32(
        190,
    ),
    "_id": ObjectId(
        "66ba285f89a2c920077fb007",
    ),
})
```

Note that, since `Cat` has no `Height` entry, it will not be output.

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
