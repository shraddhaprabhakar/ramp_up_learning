**Questions**
**Part 1: Integers** 
fn compute(a: u32, b: u32) -> u32 {
    // TODO: change the line below to fix the compiler error and make the tests pass.
    a + b * 4u8
}

#[cfg(test)]
mod tests {
    use crate::compute;

    #[test]
    fn case() {
        assert_eq!(compute(1, 2), 9);
    }
}

**Answer**
**Explanation:** We have to change u8 to u32 as implicit conversion is not allowed in rust
fn compute(a: u32, b: u32) -> u32 {
    // Converting 4u8 to u32 to match the type of 'b'
    a + b * 4u32
}

#[cfg(test)]
mod tests {
    use crate::compute;

    #[test]
    fn case() {
        assert_eq!(compute(1, 2), 9);
    }
}

**Part 2: Variables**
// 👇 The lines below, starting with `///`, are called **documentation comments**.
//    They attach documentation to the item that follows them. In this case, the `speed` function.
//    If you run `cargo doc --open` from this exercise's directory, Rust will generate
//    HTML documentation from these comments and open it in your browser.

/// Given the start and end points of a journey, and the time it took to complete it,
/// calculate the average speed.
pub fn speed(start: u32, end: u32, time_elapsed: u32) -> u32 {
    // TODO: define a variable named `distance` with the right value to get tests to pass
    //  Do you need to annotate the type of `distance`? Why or why not?

    // Don't change the line below
    distance / time_elapsed
}

#[cfg(test)]
mod tests {
    use crate::speed;

    #[test]
    fn case1() {
        assert_eq!(speed(0, 10, 10), 1);
    }

    #[test]
    fn case2() {
        assert_eq!(speed(10, 30, 10), 2);
    }

    #[test]
    fn case3() {
        assert_eq!(speed(10, 31, 10), 2);
    }
}

**Answer**
**Explanation:** Distance is simply the difference between the end and start points.
/// Given the start and end points of a journey, and the time it took to complete it,
/// calculate the average speed.
pub fn speed(start: u32, end: u32, time_elapsed: u32) -> u32 {
    // Calculate the distance
    let distance = end - start;

    // Don't change the line below
    distance / time_elapsed
}

#[cfg(test)]
mod tests {
    use crate::speed;

    #[test]
    fn case1() {
        assert_eq!(speed(0, 10, 10), 1);
    }

    #[test]
    fn case2() {
        assert_eq!(speed(10, 30, 10), 2);
    }

    #[test]
    fn case3() {
        assert_eq!(speed(10, 31, 10), 2);
    }
}

**Part 3: if else**
/// Return `true` if `n` is even, `false` otherwise.
fn is_even(n: u32) -> bool {
    todo!()
}

#[cfg(test)]
mod tests {
    use crate::is_even;

    #[test]
    fn one() {
        assert!(!is_even(1));
    }

    #[test]
    fn two() {
        assert!(is_even(2));
    }

    #[test]
    fn high() {
        assert!(!is_even(231));
    }
}

**Answer**
**Explanation:** n % 2 == 0 checks whether n is divisible by 2. If true, the number is even, and the function returns true. Otherwise, it returns false.

fn is_even(n: u32) -> bool {
    n % 2 == 0
}

#[cfg(test)]
mod tests {
    use crate::is_even;

    #[test]
    fn one() {
        assert!(!is_even(1));
    }

    #[test]
    fn two() {
        assert!(is_even(2));
    }

    #[test]
    fn high() {
        assert!(!is_even(231));
    }
}

**Part 4: panics**
/// Given the start and end points of a journey, and the time it took to complete the journey,
/// calculate the average speed of the journey.
fn speed(start: u32, end: u32, time_elapsed: u32) -> u32 {
    // TODO: Panic with a custom message if `time_elapsed` is 0

    (end - start) / time_elapsed
}

#[cfg(test)]
mod tests {
    use crate::speed;

    #[test]
    fn case1() {
        assert_eq!(speed(0, 10, 10), 1);
    }

    #[test]
    // 👇 With the `#[should_panic]` annotation we can assert that we expect the code
    //    under test to panic. We can also check the panic message by using `expected`.
    //    This is all part of Rust's built-in test framework!
    #[should_panic(expected = "The journey took no time at all, that's impossible!")]
    fn by_zero() {
        speed(0, 10, 0);
    }
}

**Answer**
**Explanation:** We can use the panic! macro to write the panic message. The panic! macro in Rust is used to immediately terminate a program when something goes wrong. It triggers a panic at runtime, which is Rust’s way of handling critical errors. When the panic! macro is invoked, the program prints an error message, unwinds the stack (releases resources and cleans up), and then terminates.

fn speed(start: u32, end: u32, time_elapsed: u32) -> u32 {
    // Panic with a custom message if `time_elapsed` is 0
    if time_elapsed == 0 {
        panic!("The journey took no time at all, that's impossible!");
    }

    (end - start) / time_elapsed
}

#[cfg(test)]
mod tests {
    use crate::speed;

    #[test]
    fn case1() {
        assert_eq!(speed(0, 10, 10), 1);
    }

    #[test]
    #[should_panic(expected = "The journey took no time at all, that's impossible!")]
    fn by_zero() {
        speed(0, 10, 0);
    }
}



