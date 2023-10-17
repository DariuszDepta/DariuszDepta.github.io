# Rust formatter configuration

Rust formatting configuration is stored in file `rustfmt.toml`.

[Configuring Rustfmt (v1.6.0)](https://rust-lang.github.io/rustfmt/?version=v1.6.0&search=)

## Unstable but handy

```toml
imports_granularity = "Module"
tab_spaces = 2
max_width = 180
```
unstable option: [imports_granularity](https://github.com/rust-lang/rustfmt/issues/4991)

Can be used like this:

```shell
$ cargo +nightly fmt
```
