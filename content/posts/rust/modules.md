---
# author: "Me"
title: "Rust: Modules"
date: "2021-10-11"
description: "Modules in Rust"
tags: ["Rust", "Module"]
categories: ["Programming"]
series: ["Rust"]
aliases: ["rust-modules"]
ShowToc: true
TocOpen: true
---

### Rules

1. If a module named `human` has no submodules, you should put the declaration for the `human` in a file named human.rs
2. If a module named `human` does have a submodule, you should put the declarations for `human` in a file named `human/mod.rs`

Example

```rust
/*
src/lib.rs
*/
pub mod Human;

/*
src/human/mod.rs
*/
pub mod social;
pub mod action;

/*
src/human/social.rs
*/
pub fn have_fun(){
	println!("Have fun");
}

/*
src/human/action.rs
*/
pub fn walk(){
	println!("walking");
}


/*
src/main.rs
*/
use my_project_name::human;

fn main(){
	human::social::have_fun();
	human::action::walk();
}

```
