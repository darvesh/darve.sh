---
# author: "Me"
title: "Rust: String Literals and Slices"
date: "2021-10-11"
description: "String literals and slices in Rust"
tags: ["Rust", "String Literal", "Slice"]
categories: ["Programming"]
series: ["Rust"]
aliases: ["rust-string-literals-slices"]
ShowToc: true
TocOpen: true
---

```rust
let greeting = "Good morning";
```

`greeting` is a string literal and they are immutable. The reason why it's immutable is explained below.

In Rust, you can store part of the String and they are called String slices. For example,

```rust
let str = String::from("Hello there");

let hello = &str[0..4];
let there = &str[6..10];
```

`hello` and `there` are String slices. They store references to the portion of the String.

Now let's talk about why string literals are immutable. The string literals are literally slices of a string. Imagine that the value `Good morning` is stored on the heap(in a memory location called `temp`) then the `greeting` variable is basically `temp[0..temp.len()]` (can write as `temp[..]`)

As I mentioned in the ownership chapter, if you have an immutable reference to a variable, you cannot take a mutable reference for the same.

Here is an example.

```rust
fn main(){
	let str = String::from("Hello there");
	let hello = &str[0..4];
	let there = &str[6..10];

	/*this will result in an error because `hello`
	a `there` already have an immutable reference to `str`*/
	str.clear();
}

```
