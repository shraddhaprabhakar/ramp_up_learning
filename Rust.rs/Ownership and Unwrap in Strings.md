**Ownership:**
ownership means that each value has a single owner. When the owner goes out of scope, the value is dropped. If you transfer ownership, the original owner can no longer use the value.
Eg: fn main() {
    let s1 = String::from(""hello""); // s1 owns the string
    let s2 = s1; // ownership moves to s2
    // println!(""{}"", s1); // This would cause an error because s1 no longer owns the string
    println!(""{}"", s2); // This works fine
}

**Unwrap:**
The unwrap method is used to get the value inside an Option<> or Result<>.Basically if the value is None or Err, it will cause a panic or will throw a compilation error. This is similar to dereferencing a nullpointer in C/C++ which gives a undefined behavior.

Eg: fn main() {
    let some_string = Some(String::from(""hello""));
    println!(""{}"", some_string.unwrap()); // This prints ""hello""

    let none_string: Option<String> = None;
    // println!(""{}"", none_string.unwrap()); // This would cause a panic
}"

