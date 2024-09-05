# Excluding Specified Entries

Previously, we always find the documents satisfying the given entry conditions.
Sometimes, we need the complement of the given entry conditions.
In this case, we can use `$not`.

```rust
collection.find(doc! {"Age": {"$not": {"$eq": 21}}}).unwrap();
```

The example above finds the documents with all `Age`s except `21`.

In addition to `$eq`, we can also use `$gt`, `$lt`, `$gte`, `$lte` and `$in` when we use `$not`.

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

    let docs_found = collection
        .find(doc! {"Age": {"$not": {"$eq": 21}}})
        .unwrap();
    for doc in docs_found {
        println!("{:#?}", doc.unwrap());
    }
}
```

Output:

```text
Document({
    "Name": String(
        "Bob",
    ),
    "Age": Int32(
        20,
    ),
    "Height": Int32(
        180,
    ),
    "_id": ObjectId(
        "66d71616753702e9e36ae43c",
    ),
})
Document({
    "Name": String(
        "Cat",
    ),
    "Age": Int32(
        3,
    ),
    "_id": ObjectId(
        "66d71616753702e9e36ae43d",
    ),
})
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
