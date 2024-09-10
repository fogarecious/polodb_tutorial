# Simple PoloDB Tutorial

[PoloDB](https://github.com/PoloDB/PoloDB) is a lightweight [MongoDB](https://www.mongodb.com/).
This tutorial serves as a quick start for [PoloDB](https://github.com/PoloDB/PoloDB).
We try to keep each part of the tutorial as simple as possible.

(The tutorial is for PoloDB version 4.4.2.)

## Quick Start

* [Setting Up](./tutorial/setting_up.md)
* [First Example](./tutorial/first_example.md)
* [Databases, Collections And Documents](./tutorial/databases_collections_and_documents.md)

## Databases

* Opening Databases
  * [Opening Databases In Memory](./tutorial/opening_databases_in_memory.md)
  * [Opening Databases In File Systems](./tutorial/opening_databases_in_file_systems.md)
* [Dropping Databases](./tutorial/dropping_databases.md)

## Collections

* [Creating Collections](./tutorial/creating_collections.md)
* [Obtaining Collections](./tutorial/obtaining_collections.md)
* [Dropping Collections](./tutorial/dropping_collections.md)

## Documents

* Inserting Documents
  * [Inserting A Document](./tutorial/inserting_a_document.md)
  * [Inserting Multiple Documents](./tutorial/inserting_multiple_documents.md)
* Finding Documents
  * [Finding All Documents](./tutorial/finding_all_documents.md)
  * Finding With Filters
    * [By An Entry](./tutorial/by_an_entry.md)
    * [And](./tutorial/and.md)
    * [Or](./tutorial/or.md)
    <!-- * Not Equal -->
    <!-- $ne does not work -->
    * [Greater Than / Less Than](./tutorial/greater_than_less_than.md)
    * [Any One In An Array](./tutorial/any_one_in_an_array.md)
    <!-- $nin does not work -->
    <!-- * Regular Expressions -->
    <!-- $regex does not work -->
    <!-- find(doc! {"Name": {"$regex": Regex { pattern: "a".into(), options: "i".into() }}}) -->
    * [Excluding Specified Entries](./tutorial/excluding_specified_entries.md)
    * [Multiple Conditions Together](./tutorial/multiple_conditions_together.md)
  * [Finding At Most One Document](./tutorial/finding_at_most_one_document.md)
* Updating Documents
  * Setting Entries
  * Upper Limits / Lower Limits
  * Increasing Entries
  * Multiplying Entries
  * Renaming Entries
  * Removing Entries
* Deleting Documents
  * Deleting By Entries
  * Deleting By Other Conditions

## Indexes

* Creating Indexes
* Unique Entries
* Dropping Indexes

## Miscellaneous

* Custom Types
* Transactions

## See Also

* [PoloDB](https://github.com/PoloDB/PoloDB) - the embedded document database.
* [Documentations](https://www.polodb.org/docs) - an official introductory documentation about PoloDB.

## Contributions

Pull requests for typos, incorrect information, or other ideas are welcome!

## License

All code in the tutorial is provided under the MIT License.
