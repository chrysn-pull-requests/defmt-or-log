# defmt-or-log

In embedded projects you often want to log something either via `core::fmt::Debug` or `defmt::Format`, depending on the configuration. The crate `defmt-or-log` provides the usual logger macros and either forwards them to the `log` or `defmt` crate, depending on the enabled features.

Furthermore, the `defmt-or-log` crate provides:
* the `FormatOrDebug` trait, that uses `core::fmt::Debug` or `defmt::Format` as super-trait and provides matching blanket implementations. This is useful for specifying trait bounds.
* the `Debug2Format` struct, which behaves similar to `defmt::Debug2Format`, but does nothing extra if using `log`.
* the `Display2Format` struct, which behaves similar to `defmt::Display2Format`, but does nothing extra if using `log`.
* the `Hex` and `Cbor` structs, which allow formatting `&[u8]`-slices with a format specifier that works for `log` and `defmt`:  
  `info!("Found bytes {}", Hex(&data))` instead of `{:02x}` (defmt) resp `{:02x?}` (log). 

See [examples/derive.rs](./examples/derive.rs).

You may either enable the `log` or the `defmt` feature but not both.  
The feature `at_least_one` (enabled per default) generates a compiler error if neither `log` nor `defmt` are enabled.   

This repository, also provides the `defmt-or-log-macros` crate, that contains Proc Macros to conditonally derive `core::fmt::Debug` or `defmt::Format`, depending on the enabled features.


## Supported macros (`defmt-or-log` crate):
* trace
* debug
* info
* warn
* error

* assert
* assert_eq
* assert_ne
* debug_assert
* debug_assert_eq
* debug_assert_ne

* todo
* unreachable
* panic
* unwrap
* intern
* expect
* unimplemented

## License

Licensed under either of:

- Apache License, Version 2.0 ([LICENSE-APACHE](../LICENSE-APACHE.txt) or http://www.apache.org/licenses/LICENSE-2.0)
- MIT license ([LICENSE-MIT](../LICENSE-MIT.txt) or http://opensource.org/licenses/MIT)

at your option.

### Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in
the work by you, as defined in the Apache-2.0 license, shall be dual licensed as above, without
any additional terms or conditions.