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
  * [Setting Entries](./tutorial/setting_entries.md)
  * [Upper Limits / Lower Limits](./tutorial/upper_limits_lower_limits.md)
  * [Increasing Entries](./tutorial/increasing_entries.md)
  * [Multiplying Entries](./tutorial/multiplying_entries.md)
  * [Renaming Entries](./tutorial/renaming_entries.md)
  * [Removing Entries](./tutorial/removing_entries.md)
  * [Updating At Most One Document](./tutorial/updating_at_most_one_document.md)
* Deleting Documents
  * [Deleting All Selected Documents](./tutorial/deleting_all_selected_documents.md)
  * [Deleting At Most One Document](./tutorial/deleting_at_most_one_document.md)

## Indexes

* [Creating Indexes](./tutorial/creating_indexes.md)
* [Unique Entries](./tutorial/unique_entries.md)
* [Dropping Indexes](./tutorial/dropping_indexes.md)

## Miscellaneous

* [Custom Types](./tutorial/custom_types.md)
* [Transactions](./tutorial/transactions.md)

## See Also

* [PoloDB](https://github.com/PoloDB/PoloDB) - the embedded document database.
* [Documentations](https://www.polodb.org/docs) - an official introductory documentation about PoloDB.

## Contributions

Pull requests for typos, incorrect information, or other ideas are welcome!

## License

All code in the tutorial is provided under the MIT License.
