**PCMP**
**Packages**
A package has a set of crates. There are 2 types of crates library crate and binary crate.  
**Binary crates** are programs you can compile to an executable that you can run, such as a command-line program or a server. Each must have a function called main that defines what happens when the executable runs.
**Library crates** don’t have a main function, and they don’t compile to an executable. Instead, they define functionality intended to be shared with multiple projects. For example, the rand crate we used provides functionality that generates random numbers. Most of the time when Rustaceans say “crate”, they mean library crate, and they use “crate” interchangeably with the general programming concept of a “library”.
Inside crates there are many **Modules** written with keyword **mod**
We use the **use** keyword for using **paths**

**Modules**
Rust provides a powerful module system that can be used to hierarchically split code in logical units (modules), and manage visibility (public/private) between them.
A module is a collection of items: functions, structs, traits, impl blocks, and even other modules.

In main function we use the use keyword to get into the lub crate, the function which is public and then the module and the the function. Example if we have a crate called intutils and we have 2 mod functions(collection of items) for addition and subtraction and then 2 functions for adding and subtracting and we use it like this in main:
use intutils::addition::add;
We also add path in cargo.toml as intutils = { path = "intutils" }

The **super** and **self** keywords can be used in the path to remove ambiguity when accessing items and to prevent unnecessary hardcoding of paths.

A **crate** is the fundamental/smallest unit of code compilation and packaging. It can be thought of as a package or library in other programming languages. 

**Cargo.toml** is used for binary crates, when we create a crate we have to mention the path in the cargo.toml package
Cargo.toml is package manager for rust and has metadata of everything.
