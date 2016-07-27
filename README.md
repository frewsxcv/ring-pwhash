# ring-pwhash

A collection of password hashing functions, using [*ring*][ring] cryptographic primitives

## Why?

The [*ring*][ring] library for Rust provides many high-performance cryptographic primitives,
but does not implement any password hashing functions except PBKDF2.

This library implements password hashing algorithms based on [*ring*][ring]'s cryptographic
primitives, serving as a "companion library" for applications that want to leverage
[*ring*][ring] as their one-and-only cryptography library, and also providing high-performance
password hash implementations thanks to the speed of [*ring*][ring]'s core primitives.

## Supported Algorithms

* [**scrypt:**][scrypt] Colin Percival's Salsa20/8+PBKDF2-based password hashing function

No other algorithms are supported at this time, although it'd be great to add additional algorithms!
Argon2 and bcrypt are both good candidates. Pull Requests Accepted!

## Benchmark

**NOTE:** *If you really care about performance, please run your own purpose-specific benchmark!*

The performance of [scrypt] on `ring-pwhash` is approximately **1.8X** faster than the equivalent
algorithm in `rust-crypto`.

Below is the output of `time cargo test scrypt::test::test_scrypt` for both `ring-pwhash` and the
upstream `rust-crypto` library (measured by 2.3GHz Intel Core i7 running Mac OS X 10.11.5):

### ring-pwhash

```
$ time cargo test scrypt::test::test_scrypt
[...]
cargo test scrypt::test::test_scrypt  9.11s user 0.09s system 107% cpu 8.592 total
```

### rust-crypto

```
$ time cargo test scrypt::test::test_scrypt
[...]
cargo test scrypt::test::test_scrypt  16.92s user 0.14s system 107% cpu 15.833 total
```

## License

ring-pwhash is a fork of rust-crypto, and is dual licensed under the MIT and
Apache 2.0 licenses, the same licenses as rust-crypto.

[ring]: https://github.com/briansmith/ring
[scrypt]: https://en.wikipedia.org/wiki/Scrypt
