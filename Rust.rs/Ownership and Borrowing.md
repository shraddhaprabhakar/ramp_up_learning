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
When we create s1, in stack ptr len and capacity gets created wih value 3 and in heap data abc is there and ptr points to a, when we assign s1 to s2, a new stack ptr len and capacity get created with name s2 and value on heap as abc with ptr pointing a but the s1 gets invalidated although it still exists on stack as the value has just been moved as we can have only 1 owner, this gives safety. The compiler just understands s1 as uninitialised and wont let you use it.
If s1 was mutable then it would work.
What if we dont want to move value and just copy it? we can do it as follows:
 let s1 = String::from("abc");
 let s2 = s1.clone();
 println!("{}",s1); // clone method not only creates 2 separate variables s1 ans s2 but also copies both the stack and heap values separately and adjusts s2's pointer to point to it.
We use the term copy to copy only the stack data but when heap data is also involved along with stack, we use clone. Clone is like deep copy.
When the value is dropped, the destructor is called and popped, the heap portion is immediately freed and the stack portion is immediately popped, so no leaks and no dangling pointers.


**BORROWING**
Ex:
let s1 = String::from("abc")
do_stuff(&s1);
println!("{}, s1);

fn do_stuff(s: &String) {
//do stuff
}
//here when we call do_stuff we are passing a reference to s1, and s1 retains ownership of the value. do_stuff borrows the reference to the value, at the end of the function the reference goes out of scope and gets dropped off so our borrowing ends at that point. Now when we call s1 in print statement it prints as value never moved.
When we create a reference to s1, rust creates a pointer under the hood to s1, the rust lang automatically creates and deletes the pointer and makes sure they are always valid using a concept called lifetimes.
Lifetimes can be summed up like a rule that references must always valid, this means u can never point to null.
By default, reference is immutable.

At any time we can have either 1 mutable reference or many number of immutable reference. This rule applies across all threads. 
It is not safe to have multiple mutable references to the same variable at the same time without any locking. But if all the references are immutable then there is no problem.
