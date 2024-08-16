# Databases, Collections And Documents

[PoloDB](https://github.com/PoloDB/PoloDB) has a hierarchical structure.

```mermaid
block-beta
  columns 7
  space:3 db[("&nbsp;Database&nbsp;")] space:3
  space:7
  space:1 c1("&nbsp;Collection&nbsp;") space:2 c2("&nbsp;Collection&nbsp;") space:1 c3("&nbsp;Collection&nbsp;")
  space:7
  d1(["Document"]) space:1 d2(["Document"]) d3(["Document"]) d4(["Document"]) d5(["Document"]) d6(["Document"])
  db --> c1
  db --> c2
  db --> c3
  c1 --> d1
  c1 --> d2
  c2 --> d3
  c2 --> d4
  c2 --> d5
  c3 --> d6
```

The topmost level is a *Database*.
A Database may contain multiple *Collections*.
A Collection may contain multiple *Documents*.
A Document is of type [JSON](https://www.json.org/).
It is possible to have Documents of custom types.

:arrow_right:  Next: [Opening Databases In Memory](./opening_databases_in_memory.md)

:blue_book: Back: [Table of contents](./../README.md)
