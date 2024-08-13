# Setting Up

First of all, we create a [Cargo](https://doc.rust-lang.org/cargo/index.html) project,

```sh
cargo new my_project
```

where `my_project` is the name of the project.

In the project directory, we add [PoloDB](https://github.com/PoloDB/PoloDB) to the project.

```sh
cargo add polodb_core
```

The dependencies in `Cargo.toml` file should look like this:

```toml
[dependencies]
polodb_core = "4.4.2"
```

<!-- :arrow_right:  Next:  -->

:blue_book: Back: [Table of contents](./../README.md)
