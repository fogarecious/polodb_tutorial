# Transactions

Transactions let us update multiple documents in a batch.
By using transactions, we can make sure that either the documents are all updated or none of them are updated.

```rust
let mut session = db.start_session().unwrap();
session.start_transaction(None).unwrap();
// ...
session.commit_transaction().unwrap();
```

We start a session first and then start a transaction.
All operations in `//...` will be executed at [commit_transaction()](https://docs.rs/polodb_core/4.4.2/polodb_core/struct.ClientSession.html#method.commit_transaction).

Let us see an example.

```rust
use polodb_core::Database;

fn main() {
    let db = Database::open_memory().unwrap();
    
    let mut session = db.start_session().unwrap();
    session.start_transaction(None).unwrap();
    
    db.create_collection_with_session("name_of_the_collection", &mut session)
        .unwrap();
    
    let names = db.list_collection_names().unwrap();
    println!("{:?}", names);
    
    let names = db.list_collection_names_with_session(&mut session).unwrap();
    println!("{:?}", names);
    
    session.commit_transaction().unwrap();

    let names = db.list_collection_names().unwrap();
    println!("{:?}", names);
}
```

Output:

```text
[]
["name_of_the_collection"]
["name_of_the_collection"]
```

We create a collection in the session.
This does not change the database until we execute [commit_transaction()](https://docs.rs/polodb_core/4.4.2/polodb_core/struct.ClientSession.html#method.commit_transaction).

In addition to [create_collection_with_session](https://docs.rs/polodb_core/4.4.2/polodb_core/struct.Database.html#method.create_collection_with_session) and [list_collection_names_with_session](https://docs.rs/polodb_core/4.4.2/polodb_core/struct.Database.html#method.list_collection_names_with_session), we can also use other methods that end with `_with_session`, such as [insert_many_with_session](https://docs.rs/polodb_core/4.4.2/polodb_core/struct.Collection.html#method.insert_many_with_session) and [update_many_with_session](https://docs.rs/polodb_core/4.4.2/polodb_core/struct.Collection.html#method.update_many_with_session).

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
