Rust guarantees memory safety at compile time, if we run code without initializing variables the code wont even work and it will give compile time error.
As long as the compiler knows that a variable has a value, it will run the code orelse it will result in runtime error.
