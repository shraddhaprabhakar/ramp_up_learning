**COLLECTIONS**
Vec<T> is a generic collection in collections used in place of lists and arrays, that holds a bunch of one type.
let mut v : Vec<i32> = Vec::new();
v.push(2);
v.push(4);
v.push(6):
let x = v.pop();  //pops 6
println!("{}", v[1]); //x is 4
Vector acts like a stack so push appends things to the end and pop removes the item at the end of the vector and returns it.

we can also create vectors using macros
A macro in Rust is a piece of code that generates other Rust code during compilation. This process is called metaprogramming. Macros are similar to functions, but they operate on syntax trees instead of values. 
let mut v = vec![2,4,6];
Hashmap is a generic collection when you specify a type for the key. HashMap<K,V> - key value pair also called dictionary, insert remove and lookup the key in constant time that is why we use hashmap.
let mut h :HashMap<u8, bool> = HashMap::new();
h.insert(5,true);
h.insert(6,false);
let have_five = h.remove(&5).unwrap();

**ENUMS**
enum Color {
    Red, 
    Green,
    Blue,
}
let color = Color::Red()
