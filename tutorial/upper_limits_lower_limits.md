# Upper Limits / Lower Limits

When entry values are numbers, we can set an upper limit of all these entry values.
This ensures that no such values are larger than the upper limit.
More precisely, we will decrease a value to the limit if the value is more than the limit.

```rust
collection.update_many(doc! {"Price": {"$gt": 0}}, doc! {"$min": {"Price": 5}}).unwrap();
```

The example above finds all documents with `Price` more than `0` and sets their `Price`s to `5` if the `Price` is more than `5`.
We use `$min` to specify that the new entry value should be the minimum of its old value and the given value.
We can also use `$max` to specify a lower limit.

The complete code is presented below:

```rust
use polodb_core::{bson::doc, Database};

fn main() {
    let db = Database::open_memory().unwrap();
    let collection = db.collection("name_of_the_collection");
    
    let docs = [
        doc! {
            "Type": "Box",
            "Color": "Blue",
            "Price": 1,
        },
        doc! {
            "Type": "Box",
            "Color": "Blue",
            "Price": 10,
        },
        doc! {
            "Type": "Box",
            "Color": "Yellow",
            "Price": 20,
        },
    ];
    collection.insert_many(docs).unwrap();

    let result = collection
        .update_many(doc! {"Price": {"$gt": 0}}, doc! {"$min": {"Price": 5}})
        .unwrap();
    println!("{:?}", result);

    let docs_found = collection.find(None).unwrap();
    for doc in docs_found {
        println!("{:#?}", doc.unwrap());
    }
}
```

Output:

```text
UpdateResult { modified_count: 3 }
Document({
    "Type": String(
        "Box",
    ),
    "Color": String(
        "Blue",
    ),
    "Price": Int32(
        1,
    ),
    "_id": ObjectId(
        "66d998ce97a343c0ca8a31ff",
    ),
})
Document({
    "Type": String(
        "Box",
    ),
    "Color": String(
        "Blue",
    ),
    "Price": Int32(
        5,
    ),
    "_id": ObjectId(
        "66d998ce97a343c0ca8a3200",
    ),
})
Document({
    "Type": String(
        "Box",
    ),
    "Color": String(
        "Yellow",
    ),
    "Price": Int32(
        5,
    ),
    "_id": ObjectId(
        "66d998ce97a343c0ca8a3201",
    ),
})
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
