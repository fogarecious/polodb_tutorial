# Multiple Conditions Together

Multiple entry conditions can be combined together.

```rust
collection.find(doc! {"Age": {"$gt": 10}, "Height": {"$not": {"$eq": 190}}}).unwrap();
```

The example above finds the documents with `Age` being more than `10` as well as `Height` being not equal to `190`.

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
        .find(doc! {"Age": {"$gt": 10}, "Height": {"$not": {"$eq": 190}}})
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
        "66d7152ac2b07e12a63d66ca",
    ),
})
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
