fn main() {
    let x = 5;
    {
        let y = 99;
        println!("{}, {}", x, y); //here it will print x and y because of same scope
    }
    println!("{}, {}", x, y); //error as after the above line y is destroyed from scope so we get error message at compile time.
}
