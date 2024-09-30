fn main() {
    let x = 5;
    {
        let y = 99;
        println!("{}, {}", x, y); //here it will print x and y because of same scope
    }
    println!("{}, {}", x, y); //error as after the above line y is destroyed from scope so we get error message at compile time.
}
but
fn main() {
    let x = 5;
    {
        let x = 99;
        println!("{}", x}; //prints x = 99, shadowed variable x which goes out of scope after this block
    }
    println!("{}",x); //prints x = 5
}

fn main()
    let mut x = 5; //x is mutable
    let x = x;     //x is now immutable
