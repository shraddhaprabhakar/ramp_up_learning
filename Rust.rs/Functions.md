Writing functions using fn keyword and snake case in Rust
fn do_stuff(qty : f32, oz : f32) -> f64 {
    println!("{},{}", qty, oz);
    return qty*oz;
}
fn main() {
    let x = do_stuff(2.0,12.5);
}
