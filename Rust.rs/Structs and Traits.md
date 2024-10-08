In other languages we have classes, in Rust we have Structs.
**STRUCTS**
syntax:
struct RedFox {
    enemy : bool,
    life : u8,
}

instantiating a rust struct:
let fox = RedFox {
}

impl RedFox {
    fn new() -> Self {
      Self {                          //this is an associative function same as class methods 
        enemy : true,                   //Self is basically RedFox struct name only
        life : 70,
}
let fox = RedFox :: new();

Instead of struct inheritance( class inheritance ) we have traits in Rust

**TRAITS**
ex
struct RedFox {
    enemy : bool,
    life : u32,
}
trait Noisy {
    fn get_noise(&self) -> &str;
}
impl Noisy for RedFox {
    fn get_noise(&self) -> &str {"Meow"}
}
