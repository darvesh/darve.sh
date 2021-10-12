---
# author: "Me"
title: "Rust: Writing tests"
date: "2021-10-11"
description: "Writing tests in Rust"
tags: ["Rust", "Test"]
categories: ["Programming"]
series: ["Rust"]
aliases: ["rust-tests"]
ShowToc: true
TocOpen: true
---

The `#[cfg(test)]` annotation tells Rust to run the function only when `cargo test` is run and not when `cargo build` is run

### Functions

```rust
assert!(1 == 2, "wasn't true"); //it will print wasn't true when test fails
assert_eq!(6, 6);
assert_ne!(6, 5);

```

### Run test

```sh
cargo test
```

### Run tests in parallel or consecutively

```sh
cargo test -- --test-threads=<numbers>
```

### Change output capture behavior, show logs

```sh
cargo test -- --nocapture
```

### Run single or multiple tests

```sh
cargo test <function-name|pattern>
```

```rust
pub fn add_one(num: i64) -> i64 {
    num + 1
}

pub fn add_two(num: i64) -> i64 {
    num + 2
}

#[cfg(test)]
mod tests {
	use super::*;
	#[test]
	fn add_one_test() {
		assert_eq!!(4, add_one(3));
	}

	#[test]
	fn add_two_test() {
		assert_eq!(6, add_two(4));
	}
}

```

Example

```bash
//will run only one test
cargo test add_one_test
//will run all tests starting with add_
cargo test add_
```

### Test function that should panic

use `#[should_panic]` attribute

```rust
pub fn i_panic() {
    panic!("omg!");
}

#[cfg(test)]
mod test {
    use super::*;
    #[test]
    #[should_panic]
    fn should_panic() {
        i_panic();
    }
}

//The above test will pass
```

### Ignore a test

Use `#[ignore]` attribute

### Integration tests

Make a directory called `tests` at the root level of the project. Assume you have this code in the `lib.rs` file in the project `adder`

```rust
/*
|-adder/src
  |--lib.rs
*/
pub add_two(num: i64) -> i64{
	num + 2
}
```

_tests/integration_test.rs_

```rust
extern crate adder;

#[test]
fn add_two_test(){
	assert_eq!(6, adder::add_two(4));
}

```

We don't need to use `#[cfg(test)]` here.
When running `cargo test`, it will run both unit and integration tests. You can also run only tests from a particular integration test file. In the above example, if you want to run tests from integration_test.ts file

```rust
cargo test --test integration_test.rs
```
