**Question:**
// TODO: fix the function signature below to make the tests pass.
//  Make sure to read the compiler error message—the Rust compiler is your pair programming
//  partner in this course and it'll often guide you in the right direction!
//
// The input parameters should have the same type of the return type.
fn compute(a, b) -> u32 {
    // Don't touch the function body.
    a + b * 2
}

#[cfg(test)]
mod tests {
    use crate::compute;

    #[test]
    fn case() {
        assert_eq!(compute(1, 2), 5);
    }
}


**Answer**
**explanation**: The input parameters have the same type as the return type, which is u32.
fn compute(a: u32, b: u32) -> u32 {
    // Don't touch the function body.
    a + b * 2
}

#[cfg(test)]
mod tests {
    use crate::compute;

    #[test]
    fn case() {
        assert_eq!(compute(1, 2), 5);
    }
}
