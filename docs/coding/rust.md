# Notes for Rust coding

## Official Reference

- [Rust book](https://doc.rust-lang.org/book/index.html)
- [Rust reference](https://doc.rust-lang.org/reference/introduction.html)
- [Rust std](https://doc.rust-lang.org/std/index.html)
- [Rust by example](https://doc.rust-lang.org/rust-by-example/index.html)

## traits

### Clone , Copy and Move

- [move copy and clone in Rust](https://hashrust.com/blog/moves-copies-and-clones-in-rust/)
- [Copy](https://doc.rust-lang.org/std/marker/trait.Copy.html)
- [Clone](https://doc.rust-lang.org/std/clone/trait.Clone.html)

## [Derive](https://doc.rust-lang.org/reference/attributes/derive.html)

- [derive macros](https://doc.rust-lang.org/reference/procedural-macros.html#derive-macros)
- compiler is capable of providing basic implementations for some traits via `#[derive]` attribute
- list of derivable traits
  - comparison traits: Eq, ParitialEq, Ord, PartialOrd
  - Clone
  - Copy
  - hash
  - Default
  - Debug

## attribute

## \* and &

- [\* operator](https://micouy.github.io/rust-dereferencing/#:~:text=It%E2%80%99s%20simply%20impossible%20to%20dereference%20a%20reference%20in,operator%20is%20totally%20unrelated%20to%20the%20ref%20operator.)
- [dereference operator](https://www.becomebetterprogrammer.com/rust-dereference-unary-operator/)
- [reference and borrowing](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html)

## Ownership

### stack and heap

- stack, FILO or LIFO last in first out, conjected in memory from bottom to top

- heap less orginized. alloctor find an empty spot and return back a pointer.

## data type

### tuple, array and vector

- tuple
  - finte
  - heterogeneous : each element can have a different type and lifetime
  - sequence and accessed by position
  - access by period(.) `tup.1`
  - syntax `let x :(i32, 64, u8)=(100,5.4,1)`
- array
  - same type
  - fixed length
  - allocated in stack
  - syntax `let a:[i32;5]=[1,2,3,4,5];`
  - init array with same value `let a=[3;5]`
- vector
