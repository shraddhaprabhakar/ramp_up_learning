**Rust**
It is a systems programming language, safety which is guaranteed at compile time, blazing concurrency which is a lot easier when things are safe, and very fast.
Core firefox written in rust and hence it became a faster web browser.

**CARGO**
Package manager, test runner and documentation generator.
**commands**:
cargo new hello //creates a new project called hello, a hello directory is created with a config file cargo.toml and a source sub directory with a main.rs file. toml is toms obvious minimal language
**cargo.toml** - it is the config file of the project, it has name, version, author,edition and dependencies if any
rust has semantic versioning, version is separated by 3 dots 0.1.0 - MAJOR.MINOR.PATCH
**MAJOR**: When you make incompatible changes (breaking changes). For example, if the new version of a library introduces changes that are not backward-compatible, you increase the MAJOR version. 
**MINOR**: When you add functionality in a backward-compatible manner. This includes adding new features that don't break existing functionality. 
**PATCH**: When you make backward-compatible bug fixes. This is for changes that fix bugs without altering the existing API or functionality in a way that would require changes by the consumers of the package.
1.0.0: Initial stable release.
1.1.0: New features added, but backward-compatible.
2.0.0: Major changes that break compatibility with version 1.x.x.
**cargo run** - used to compile and run the code
**cargo build**- makes exe file: cargo.lock, cargo.toml, src, target
then cd target, cd debug, .\nameofproject.exe , .exe can run on any platform even if rust isnt installed
In Rust, when using cargo (Rust’s package manager and build system), debug symbols are included in the compiled binary when you build the project in debug mode. These symbols help in debugging by including metadata about your code (e.g., variable names, line numbers, and file locations), which makes it easier to step through the program using a debugger, inspect variables, and analyze crashes. If you want to remove the debug you can use **cargo run- --release**. Instead of debug subdirectory now it will be stored in release subdirectory.
