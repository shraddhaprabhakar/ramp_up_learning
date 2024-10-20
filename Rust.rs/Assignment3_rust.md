### **Questions**
**Part 1: Struct**
// Define a struct named `Order` with the following fields:
// - `price`, an unsigned integer
// - `quantity`, an unsigned integer
//
// It should also have a method named `is_available` that returns a `true` if the quantity is
// greater than 0, otherwise `false`.

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_order_is_available() {
        let order = Order {
            price: 100,
            quantity: 10,
        };
        assert!(order.is_available());
    }

    #[test]
    fn test_order_is_not_available() {
        let order = Order {
            price: 100,
            quantity: 0,
        };
        assert!(!order.is_available());
    }
}

**Answer**
**Explanation:** 
// Define a struct named `Order`
struct Order {
    price: u32,     // unsigned integer for price
    quantity: u32,  // unsigned integer for quantity
}

impl Order {
    // Method to check if the order is available
    fn is_available(&self) -> bool {
        self.quantity > 0  // Returns true if quantity is greater than 0
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_order_is_available() {
        let order = Order {
            price: 100,
            quantity: 10,
        };
        assert!(order.is_available());
    }

    #[test]
    fn test_order_is_not_available() {
        let order = Order {
            price: 100,
            quantity: 0,
        };
        assert!(!order.is_available());
    }
}

**Part 2: validation**
struct Ticket {
    title: String,
    description: String,
    status: String,
}

impl Ticket {
    // TODO: implement the `new` function.
    //  The following requirements should be met:
    //   - Only `To-Do`, `In Progress`, and `Done` statuses are allowed.
    //   - The `title` and `description` fields should not be empty.
    //   - the `title` should be at most 50 bytes long.
    //   - the `description` should be at most 500 bytes long.
    //  The method should panic if any of the requirements are not met.
    //  You can find the needed panic messages in the tests.
    //
    // You'll have to use what you learned in the previous exercises,
    // as well as some `String` methods. Use the documentation of Rust's standard library
    // to find the most appropriate options -> https://doc.rust-lang.org/std/string/struct.String.html
    fn new(title: String, description: String, status: String) -> Self {
        todo!();
        Self {
            title,
            description,
            status,
        }
    }
}

#[cfg(test)]
mod tests {
    use super::*;
    use common::{overly_long_description, overly_long_title, valid_description, valid_title};

    #[test]
    #[should_panic(expected = "Title cannot be empty")]
    fn title_cannot_be_empty() {
        Ticket::new("".into(), valid_description(), "To-Do".into());
    }

    #[test]
    #[should_panic(expected = "Description cannot be empty")]
    fn description_cannot_be_empty() {
        Ticket::new(valid_title(), "".into(), "To-Do".into());
    }

    #[test]
    #[should_panic(expected = "Title cannot be longer than 50 bytes")]
    fn title_cannot_be_longer_than_fifty_chars() {
        Ticket::new(overly_long_title(), valid_description(), "To-Do".into());
    }

    #[test]
    #[should_panic(expected = "Description cannot be longer than 500 bytes")]
    fn description_cannot_be_longer_than_500_chars() {
        Ticket::new(valid_title(), overly_long_description(), "To-Do".into());
    }

    #[test]
    #[should_panic(expected = "Only `To-Do`, `In Progress`, and `Done` statuses are allowed")]
    fn status_must_be_valid() {
        Ticket::new(valid_title(), valid_description(), "Funny".into());
    }

    #[test]
    fn done_is_allowed() {
        Ticket::new(valid_title(), valid_description(), "Done".into());
    }

    #[test]
    fn in_progress_is_allowed() {
        Ticket::new(valid_title(), valid_description(), "In Progress".into());
    }
}

**Answer**
**Explanation:** 
struct Ticket {
    title: String,
    description: String,
    status: String,
}

impl Ticket {
    fn new(title: String, description: String, status: String) -> Self {
        // Check if title is empty
        if title.is_empty() {
            panic!("Title cannot be empty");
        }
        // Check if description is empty
        if description.is_empty() {
            panic!("Description cannot be empty");
        }
        // Check if title is longer than 50 bytes
        if title.len() > 50 {
            panic!("Title cannot be longer than 50 bytes");
        }
        // Check if description is longer than 500 bytes
        if description.len() > 500 {
            panic!("Description cannot be longer than 500 bytes");
        }
        // Check if status is valid
        let valid_statuses = ["To-Do", "In Progress", "Done"];
        if !valid_statuses.contains(&status.as_str()) {
            panic!("Only `To-Do`, `In Progress`, and `Done` statuses are allowed");
        }

        // If all checks pass, create a new Ticket
        Self {
            title,
            description,
            status,
        }
    }
}

#[cfg(test)]
mod tests {
    use super::*;
    use common::{overly_long_description, overly_long_title, valid_description, valid_title};

    #[test]
    #[should_panic(expected = "Title cannot be empty")]
    fn title_cannot_be_empty() {
        Ticket::new("".into(), valid_description(), "To-Do".into());
    }

    #[test]
    #[should_panic(expected = "Description cannot be empty")]
    fn description_cannot_be_empty() {
        Ticket::new(valid_title(), "".into(), "To-Do".into());
    }

    #[test]
    #[should_panic(expected = "Title cannot be longer than 50 bytes")]
    fn title_cannot_be_longer_than_fifty_chars() {
        Ticket::new(overly_long_title(), valid_description(), "To-Do".into());
    }

    #[test]
    #[should_panic(expected = "Description cannot be longer than 500 bytes")]
    fn description_cannot_be_longer_than_500_chars() {
        Ticket::new(valid_title(), overly_long_description(), "To-Do".into());
    }

    #[test]
    #[should_panic(expected = "Only `To-Do`, `In Progress`, and `Done` statuses are allowed")]
    fn status_must_be_valid() {
        Ticket::new(valid_title(), valid_description(), "Funny".into());
    }

    #[test]
    fn done_is_allowed() {
        Ticket::new(valid_title(), valid_description(), "Done".into());
    }

    #[test]
    fn in_progress_is_allowed() {
        Ticket::new(valid_title(), valid_description(), "In Progress".into());
    }
}

**Part 3: Modules**
mod helpers {
    // TODO: Make this code compile, either by adding a `use` statement or by using
    //  the appropriate path to refer to the `Ticket` struct.

    fn create_todo_ticket(title: String, description: String) -> Ticket {
        Ticket::new(title, description, "To-Do".into())
    }
}

struct Ticket {
    title: String,
    description: String,
    status: String,
}

impl Ticket {
    fn new(title: String, description: String, status: String) -> Ticket {
        if title.is_empty() {
            panic!("Title cannot be empty");
        }
        if title.len() > 50 {
            panic!("Title cannot be longer than 50 bytes");
        }
        if description.is_empty() {
            panic!("Description cannot be empty");
        }
        if description.len() > 500 {
            panic!("Description cannot be longer than 500 bytes");
        }
        if status != "To-Do" && status != "In Progress" && status != "Done" {
            panic!("Only `To-Do`, `In Progress`, and `Done` statuses are allowed");
        }

        Ticket {
            title,
            description,
            status,
        }
    }
}

**Answer**
**Explanation:**
mod helpers {
    use super::Ticket;  // Import the Ticket struct from the outer scope

    fn create_todo_ticket(title: String, description: String) -> Ticket {
        Ticket::new(title, description, "To-Do".into())
    }
}

struct Ticket {
    title: String,
    description: String,
    status: String,
}

impl Ticket {
    fn new(title: String, description: String, status: String) -> Ticket {
        if title.is_empty() {
            panic!("Title cannot be empty");
        }
        if title.len() > 50 {
            panic!("Title cannot be longer than 50 bytes");
        }
        if description.is_empty() {
            panic!("Description cannot be empty");
        }
        if description.len() > 500 {
            panic!("Description cannot be longer than 500 bytes");
        }
        if status != "To-Do" && status != "In Progress" && status != "Done" {
            panic!("Only `To-Do`, `In Progress`, and `Done` statuses are allowed");
        }

        Ticket {
            title,
            description,
            status,
        }
    }
}

**Part 4: Visibility**
mod ticket {
    struct Ticket {
        title: String,
        description: String,
        status: String,
    }

    impl Ticket {
        fn new(title: String, description: String, status: String) -> Ticket {
            if title.is_empty() {
                panic!("Title cannot be empty");
            }
            if title.len() > 50 {
                panic!("Title cannot be longer than 50 bytes");
            }
            if description.is_empty() {
                panic!("Description cannot be empty");
            }
            if description.len() > 500 {
                panic!("Description cannot be longer than 500 bytes");
            }
            if status != "To-Do" && status != "In Progress" && status != "Done" {
                panic!("Only `To-Do`, `In Progress`, and `Done` statuses are allowed");
            }

            Ticket {
                title,
                description,
                status,
            }
        }
    }
}

// TODO: **Exceptionally**, you'll be modifying both the `ticket` module and the `tests` module
//  in this exercise.
#[cfg(test)]
mod tests {
    // TODO: Add the necessary `pub` modifiers in the parent module to remove the compiler
    //  errors about the use statement below.
    use super::ticket::Ticket;

    // Be careful though! We don't want this function to compile after you have changed
    // visibility to make the use statement compile!
    // Once you have verified that it indeed doesn't compile, comment it out.
    fn should_not_be_possible() {
        let ticket = Ticket::new("A title".into(), "A description".into(), "To-Do".into());

        // You should be seeing this error when trying to run this exercise:
        //
        // error[E0616]: field `description` of struct `Ticket` is private
        //    |
        //    |              assert_eq!(ticket.description, "A description");
        //    |                         ^^^^^^^^^^^^^^^^^^
        //
        // TODO: Once you have verified that the below does not compile,
        //   comment the line out to move on to the next exercise!
        assert_eq!(ticket.description, "A description");
    }

    fn encapsulation_cannot_be_violated() {
        // This should be impossible as well, with a similar error as the one encountered above.
        // (It will throw a compilation error only after you have commented the faulty line
        // in the previous test - next compilation stage!)
        //
        // This proves that `Ticket::new` is now the only way to get a `Ticket` instance.
        // It's impossible to create a ticket with an illegal title or description!
        //
        // TODO: Once you have verified that the below does not compile,
        //   comment the lines out to move on to the next exercise!
        let ticket = Ticket {
            title: "A title".into(),
            description: "A description".into(),
            status: "To-Do".into(),
        };
    }
}

**Answer**
**Explanation:**
We need to make the Ticket struct and the new method public so they can be accessed from outside the ticket module. At the same time, we should keep the struct fields (title, description, and status) private to enforce encapsulation. Items inside a module (mod) are private by default. This means that if you define a struct, function, or any other item inside a module, it is only accessible within that module or any child modules unless explicitly made public using the pub keyword.
mod ticket {
    // Make the Ticket struct public so it can be used outside this module
    pub struct Ticket {
        // Keep these fields private to prevent direct access from outside the module
        title: String,
        description: String,
        status: String,
    }

    impl Ticket {
        // Make the new function public so it can be accessed outside this module
        pub fn new(title: String, description: String, status: String) -> Ticket {
            if title.is_empty() {
                panic!("Title cannot be empty");
            }
            if title.len() > 50 {
                panic!("Title cannot be longer than 50 bytes");
            }
            if description.is_empty() {
                panic!("Description cannot be empty");
            }
            if description.len() > 500 {
                panic!("Description cannot be longer than 500 bytes");
            }
            if status != "To-Do" && status != "In Progress" && status != "Done" {
                panic!("Only `To-Do`, `In Progress`, and `Done` statuses are allowed");
            }

            Ticket {
                title,
                description,
                status,
            }
        }
    }
}

// Tests module
#[cfg(test)]
mod tests {
    use super::ticket::Ticket;

    // Commenting this function out after confirming the private field violation
    // fn should_not_be_possible() {
    //     let ticket = Ticket::new("A title".into(), "A description".into(), "To-Do".into());
    //     // This will produce a compiler error as `description` is private
    //     assert_eq!(ticket.description, "A description");
    // }

    // Commenting this function out after confirming the private field violation
    // fn encapsulation_cannot_be_violated() {
    //     // This should also produce a compiler error because the fields are private
    //     let ticket = Ticket {
    //         title: "A title".into(),
    //         description: "A description".into(),
    //         status: "To-Do".into(),
    //     };
    // }
}

