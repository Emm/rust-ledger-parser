# ledger-parser

[![Crates.io Version](https://img.shields.io/crates/v/ledger-parser.svg)](https://crates.io/crates/ledger-parser)
[![Docs.rs Version](https://docs.rs/ledger-parser/badge.svg)](https://docs.rs/ledger-parser)
[![License Unlicense](https://img.shields.io/crates/l/ledger-parser.svg)](http://unlicense.org/UNLICENSE)

Rust library for parsing [Ledger-cli](https://www.ledger-cli.org/) input files.

## File format

Only a subset of the ledger-cli's file format is implemented.

Supported elements:

* Line comments (starting with: ``; # % | *``)

* Inline comments (starting with ``;``)

* Transaction headers with format:

  ```
  DATE[=EDATE] [*|!] [(CODE)] DESC
  ```

* Transaction postings with format (minimum two spaces or one tab between ``ACCOUNT`` and ``AMOUNT``):

  ```
    ACCOUNT  AMOUNT [; NOTE]
  ```

  There may be a single posting without an amount in a transaction.

* Commodity prices with format:

  ```
  P DATE SYMBOL PRICE
  ```

## Example

```rust
extern crate ledger_parser;

let result = ledger_parser::parse(r#"; Example 1
2018-10-01=2018-10-14 ! (123) Description
  ; Transaction comment
  TEST:Account 123  $1.20
  ; Posting comment
  TEST:Account 345  -$1.20"#);
```
