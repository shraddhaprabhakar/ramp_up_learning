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

**Part 5: factorial**
// Define a function named `factorial` that, given a non-negative integer `n`,
// returns `n!`, the factorial of `n`.
//
// The factorial of `n` is defined as the product of all positive integers up to `n`.
// For example, `5!` (read "five factorial") is `5 * 4 * 3 * 2 * 1`, which is `120`.
// `0!` is defined to be `1`.
//
// We expect `factorial(0)` to return `1`, `factorial(1)` to return `1`,
// `factorial(2)` to return `2`, and so on.
//
// Use only what you learned! No loops yet, so you'll have to use recursion!

#[cfg(test)]
mod tests {
    use crate::factorial;

    #[test]
    fn first() {
        assert_eq!(factorial(0), 1);
    }

    #[test]
    fn second() {
        assert_eq!(factorial(1), 1);
    }

    #[test]
    fn third() {
        assert_eq!(factorial(2), 2);
    }

    #[test]
    fn fifth() {
        assert_eq!(factorial(5), 120);
    }
}

**Answer**
**Explanation:** Formula for factorial is n*(factorial)(n-1) which calls n recursively in a stack till n reaches 0 and returns 1.
/// Calculate the factorial of a non-negative integer `n`.
fn factorial(n: u32) -> u32 {
    // Base case: 0! is 1
    if n == 0 {
        return 1;
    }
    // Recursive case: n! = n * (n-1)!
    n * factorial(n - 1)
}

#[cfg(test)]
mod tests {
    use crate::factorial;

    #[test]
    fn first() {
        assert_eq!(factorial(0), 1);
    }

    #[test]
    fn second() {
        assert_eq!(factorial(1), 1);
    }

    #[test]
    fn third() {
        assert_eq!(factorial(2), 2);
    }

    #[test]
    fn fifth() {
        assert_eq!(factorial(5), 120);
    }
}

**Part 6: while loop**
// Rewrite the factorial function using a `while` loop.
pub fn factorial(n: u32) -> u32 {
    // The `todo!()` macro is a placeholder that the compiler
    // interprets as "I'll get back to this later", thus
    // suppressing type errors.
    // It panics at runtime.
    todo!()
}

#[cfg(test)]
mod tests {
    use crate::factorial;

    #[test]
    fn first() {
        assert_eq!(factorial(0), 1);
    }

    #[test]
    fn second() {
        assert_eq!(factorial(1), 1);
    }

    #[test]
    fn third() {
        assert_eq!(factorial(2), 2);
    }

    #[test]
    fn fifth() {
        assert_eq!(factorial(5), 120);
    }
}

**Answer**
**Explanation:** We need to use mutable variables as the result has to be updated and the approach is calculating factorial backwards like result = result * n and then decreasing n value till it becomes 1.
pub fn factorial(mut n: u32) -> u32 {
    let mut result = 1;

    // Loop while n is greater than 1
    while n > 1 {
        result *= n;  // Multiply result by the current value of n
        n -= 1;       // Decrement n
    }

    result
}

#[cfg(test)]
mod tests {
    use crate::factorial;

    #[test]
    fn first() {
        assert_eq!(factorial(0), 1);
    }

    #[test]
    fn second() {
        assert_eq!(factorial(1), 1);
    }

    #[test]
    fn third() {
        assert_eq!(factorial(2), 2);
    }

    #[test]
    fn fifth() {
        assert_eq!(factorial(5), 120);
    }
}


**Part 7: For loop**

// Rewrite the factorial function using a `for` loop.
pub fn factorial(n: u32) -> u32 {
    todo!()
}

#[cfg(test)]
mod tests {
    use crate::factorial;

    #[test]
    fn first() {
        assert_eq!(factorial(0), 1);
    }

    #[test]
    fn second() {
        assert_eq!(factorial(1), 1);
    }

    #[test]
    fn third() {
        assert_eq!(factorial(2), 2);
    }

    #[test]
    fn fifth() {
        assert_eq!(factorial(5), 120);
    }
}

**Answer**
**Explanation:** We are using a range based for loop to go from 1 to n (inclusive because of ..=) and calculating factorial by using result = result *i
pub fn factorial(n: u32) -> u32 {
    let mut result = 1;

    // Iterate from 1 to n (inclusive)
    for i in 1..=n {
        result *= i;  // Multiply result by i in each iteration
    }

    result
}

#[cfg(test)]
mod tests {
    use crate::factorial;

    #[test]
    fn first() {
        assert_eq!(factorial(0), 1);
    }

    #[test]
    fn second() {
        assert_eq!(factorial(1), 1);
    }

    #[test]
    fn third() {
        assert_eq!(factorial(2), 2);
    }

    #[test]
    fn fifth() {
        assert_eq!(factorial(5), 120);
    }
}


**Part 8: Overflow**
// Customize the `dev` profile to wrap around on overflow.
// Check Cargo's documentation to find out the right syntax:
// https://doc.rust-lang.org/cargo/reference/profiles.html
//
// For reasons that we'll explain later, the customization needs to be done in the `Cargo.toml`
// at the root of the repository, not in the `Cargo.toml` of the exercise.

pub fn factorial(n: u32) -> u32 {
    let mut result = 1;
    for i in 1..=n {
        result *= i;
    }
    result
}

#[cfg(test)]
mod tests {
    use crate::factorial;

    #[test]
    fn twentieth() {
        // 20! is 2432902008176640000, which is too large to fit in a u32
        // With the default dev profile, this will panic when you run `cargo test`
        // We want it to wrap around instead
        assert_eq!(factorial(20), 2_192_834_560);
        //                           ☝️
        // A large number literal using underscores to improve readability!
    }

    #[test]
    fn first() {
        assert_eq!(factorial(0), 1);
    }

    #[test]
    fn second() {
        assert_eq!(factorial(1), 1);
    }

    #[test]
    fn third() {
        assert_eq!(factorial(2), 2);
    }

    #[test]
    fn fifth() {
        assert_eq!(factorial(5), 120);
    }
}

**Answer**
**Explanation:** In the cargo.toml which is a manifest for every rust package, written in toml format which has metadata needed to compile the package, we change the overflow-checks = false from true. This configuration disables the overflow checks in the development profile, allowing arithmetic overflow to result in wrapping (modular arithmetic: numbers wrap around while reaching a certain limit). So because of this if we find 20!, rust wont panic ad instead wrap around the interger type.

[profile.dev]
overflow-checks = false


**Part 9: Saturating**
pub fn factorial(n: u32) -> u32 {
    let mut result = 1;
    for i in 1..=n {
        // Use saturating multiplication to stop at the maximum value of u32
        // rather than overflowing and wrapping around
        result *= i;
    }
    result
}

#[cfg(test)]
mod tests {
    use crate::factorial;

    #[test]
    fn twentieth() {
        assert_eq!(factorial(20), u32::MAX);
    }

    #[test]
    fn first() {
        assert_eq!(factorial(0), 1);
    }

    #[test]
    fn second() {
        assert_eq!(factorial(1), 1);
    }

    #[test]
    fn third() {
        assert_eq!(factorial(2), 2);
    }

    #[test]
    fn fifth() {
        assert_eq!(factorial(5), 120);
    }
}

**Answer**
**Explanation:** We use saturating_mul to prevent overflow. In Rust, saturating_mul is a method provided by numeric types that performs multiplication in a saturating manner. This means that if the result of the multiplication exceeds the maximum or minimum value that the type can represent, it will "saturate" at that value instead of wrapping around or causing overflow.

pub fn factorial(n: u32) -> u32 {
    let mut result = 1;
    for i in 1..=n {
        // Use saturating multiplication to prevent overflow
        result = result.saturating_mul(i);
    }
    result
}

#[cfg(test)]
mod tests {
    use crate::factorial;

    #[test]
    fn twentieth() {
        // Factorial(20) would overflow, but with saturating multiplication, it stops at u32::MAX
        assert_eq!(factorial(20), u32::MAX);
    }

    #[test]
    fn first() {
        assert_eq!(factorial(0), 1);
    }

    #[test]
    fn second() {
        assert_eq!(factorial(1), 1);
    }

    #[test]
    fn third() {
        assert_eq!(factorial(2), 2);
    }

    #[test]
    fn fifth() {
        assert_eq!(factorial(5), 120);
    }
}

**part 10: Casting**
// TODO: based on what you learned in this section, replace `todo!()` with
//  the correct value after the conversion.

#[cfg(test)]
mod tests {

    #[test]
    fn u16_to_u32() {
        let v: u32 = todo!();
        assert_eq!(47u16 as u32, v);
    }

    #[test]
    fn u8_to_i8() {
        // The compiler is smart enough to know that the value 255 cannot fit
        // inside an i8, so it'll emit a hard error. We intentionally disable
        // this guardrail to make this (bad) conversion possible.
        // The compiler is only able to pick on this because the value is a
        // literal. If we were to use a variable, the compiler wouldn't be able to
        // catch this at compile time.
        #[allow(overflowing_literals)]
        let x = { 255 as i8 };

        // You could solve this by using exactly the same expression as above,
        // but that would defeat the purpose of the exercise. Instead, use a genuine
        // `i8` value that is equivalent to `255` when converted from `u8`.
        let y: i8 = todo!();

        assert_eq!(x, y);
    }

    #[test]
    fn bool_to_u8() {
        let v: u8 = todo!();
        assert_eq!(true as u8, v);
    }
}

**Answer**
**Explanation:** 47u16 as u32 will convert u16 as u32
#[cfg(test)]
mod tests {
    
    #[test]
    fn u16_to_u32() {
        let v: u32 = 47u16 as u32;  // 47 can be safely converted to u32
        assert_eq!(47u16 as u32, v);
    }

    #[test]
    fn u8_to_i8() {
        // The compiler is smart enough to know that the value 255 cannot fit
        // inside an i8, so it'll emit a hard error. We intentionally disable
        // this guardrail to make this (bad) conversion possible.
        // The compiler is only able to pick on this because the value is a
        // literal. If we were to use a variable, the compiler wouldn't be able
        // to catch this at compile time.
        #[allow(overflowing_literals)]
        let x = { 255 as i8 };  // This will cause overflow and wrap around

        // 255 in u8 is equivalent to -1 in i8 because of wrapping.
        let y: i8 = -1;  // The equivalent i8 value for u8 255

        assert_eq!(x, y);
    }

    #[test]
    fn bool_to_u8() {
        let v: u8 = true as u8;  // true is equivalent to 1 in u8
        assert_eq!(true as u8, v);
    }
}







