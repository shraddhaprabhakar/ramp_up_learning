**OWNERSHIP**
The ownership module of rust makes it so safe guaranteed.
It has 3 rules: 
a) Each value has its own member: there is no value in memory , no data that doesnt have variable of its own.
b) There is only one owner of a value. No variables can share ownership but they can borrow.
c) Value gets dropped if the owner goes out of scope.

Ex:
let s1 = String::from("abc"); //creating string s1
let s2 = s1; // assigning s1 to s2(at this point the value of s1 is moved to s2 as there can be only one owner)
println!( "{}", s1); //this will give error as s1 has been moved to s2 and it does not exist on stack temporarily till it gets the ownership back , borrow of moved value s1 is the compiler error.
