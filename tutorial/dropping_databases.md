# Dropping Databases

It is easy to drop a database.

* For a database that is opened by [open_file](https://docs.rs/polodb_core/latest/polodb_core/struct.Database.html#method.open_file), just delete the file.
* For a database that is opened by [open_memory](https://docs.rs/polodb_core/4.4.2/polodb_core/struct.Database.html#method.open_memory), the database will be dropped automatically when the program exits.

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
