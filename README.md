Automoduse
==========

[<img alt="github" src="https://img.shields.io/badge/github-yvvki/automoduse-8da0cb?style=for-the-badge&labelColor=555555&logo=github" height="20">](https://github.com/yvvki/automoduse)
[<img alt="crates.io" src="https://img.shields.io/crates/v/automoduse.svg?style=for-the-badge&color=fc8d62&logo=rust" height="20">](https://crates.io/crates/automoduse)
[<img alt="docs.rs" src="https://img.shields.io/badge/docs.rs-automoduse-66c2a5?style=for-the-badge&labelColor=555555&logo=docs.rs" height="20">](https://docs.rs/automoduse)
[<img alt="build status" src="https://img.shields.io/github/actions/workflow/status/yvvki/automoduse/ci.yml?branch=master&style=for-the-badge" height="20">](https://github.com/yvvki/automoduse/actions?query=branch%3Amaster)

Pull in every source file in a directory as a module.

```toml
[dependencies]
automoduse = "1.0"
```

## Syntax

```rust
automoduse::dir!("path/to/directory");
```

This macro expands to one or more `mod` items, one for each source file in the
specified directory.

The path is given relative to the directory containing Cargo.toml.

It is an error if the given directory contains no source files.

The macro takes an optional visibility to apply on the generated modules:
`automoduse::dir!(pub "path/to/directory")`.

## Example

Suppose that we would like to keep a directory of regression tests for
individual numbered issues:

- tests/
  - regression/
    - issue1.rs
    - issue2.rs
    - ...
    - issue128.rs

We would like to be able to toss files in this directory and have them
automatically tested, without listing them in some explicit list of modules.
Automoduse solves this by adding *tests/regression.rs* containing:

```rust
mod regression {
    automoduse::dir!("tests/regression");
}
```

The macro invocation expands to:

```rust
mod issue1;
mod issue2;
/* ... */
mod issue128;
```

<br>

#### License

<sup>
Licensed under either of <a href="LICENSE-APACHE">Apache License, Version
2.0</a> or <a href="LICENSE-MIT">MIT license</a> at your option.
</sup>

<br>

<sub>
Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in this crate by you, as defined in the Apache-2.0 license, shall
be dual licensed as above, without any additional terms or conditions.
</sub>
