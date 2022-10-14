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

## operators

### \* and &

- [\* operator](https://micouy.github.io/rust-dereferencing/#:~:text=It%E2%80%99s%20simply%20impossible%20to%20dereference%20a%20reference%20in,operator%20is%20totally%20unrelated%20to%20the%20ref%20operator.)
- [dereference operator](https://www.becomebetterprogrammer.com/rust-dereference-unary-operator/)
- [reference and borrowing](https://doc.rust-lang.org/book/ch04-02-references-and-borrowing.html)

## Ownership

### stack and heap

- stack, FILO or LIFO last in first out, conjected in memory from bottom to top

- heap less orginized. alloctor find an empty spot and return back a pointer.

### Ownership Rules

- each value has an owner
- there can only be one owner at a time
- when the owner goes out of scope, the vaule will be dropped

### variable scope

- a scope is the range within a program for which an item is valid.

### memory and allocation

- the memory must be requested from the memory allocator at runtime
  - ` String::from`
- we need a way of returning this memory to the allocator when we're done with it.
  - path taken by rust:
    > the memory is automatically returned once the variable that owns it goes out of scope.
    > when a variable goes out of scope, Rust calls a special function `drop`

### ways varibles and data interact

- move

  - a String is made of three parts:
    - a pointer to the memory that hold the contents of the string
    - a length
    - a capacity

  ```rust
      let s1 = String::from("hello");
      let s2 = s1;
  ```

  to avoid `drop` twice when both s1 and s2 out of scope, Rust consider s1 as no longer valid after `let s2=s1`
  'let s2=s1' does not create a **shallow copy** of s1's three part. It's kind of **move**

- clone

```rust
let s1 = String::from("hello");
let s2 = s1.clone();
println!("s1 = {}, s2 = {}", s1, s2);
```

- stack-only data: copy
  Rust has a special annotation called `Copy` trait that we can place on types that are stored on the stack.  
  Rust won't let us annotate a type with `Copy` if the type, or any of its parts, has implemented the `Drop` traits

### Ownership and functions

> the mechanics of passing a value to a function are similar to those when assigning a value to a variable

### return values and scope

> returning values can also transfer ownship.

## data type

### String, str, String literal and string slice

- [String](https://doc.rust-lang.org/std/string/struct.String.html)

  - A UTF-8-encoded
  - growable string
  - interation with str
    - create from a literal string `let hello = String::from("hello");`
    - append a &str with push_str `hello.push_str("word");`
      - note if append a `char` it's `hello.push('w');`
  - create from a vector of UTF-8 bytes

  ```rust
  // some bytes, in a vector
  let sparkle_heart = vec![240, 159, 146, 150];

  // We know these bytes are valid, so we'll use `unwrap()`.
  let sparkle_heart = String::from_utf8(sparkle_heart).unwrap();

  assert_eq!("💖", sparkle_heart);

  ```

  - deref

    - String implements Deref<Target=str> and so inherits all of str's method. it means that you can pass a String which takes &str by using a ampersand(&)

    ```rust
    fn takes_str(s: &str) { }

    let s = String::from("Hello");

    takes_str(&s);

    ```

- [str](https://doc.rust-lang.org/std/primitive.str.html)
  - it's primitive type
  - aka string slice
  - string literals is type `&'static str`

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
  - access `let first=a[0];`
- vector
  - changeable length

## item

an item is a component of a crate. A crate is a unit of compilation and linking, as well as versioning, distribution, and runtime loading.

## loop

### loop label

example

```rust
fn main() {
    let mut count = 0;
        'counting_up: loop {
	        println!("count = {}")
		loop {
		if count==0 {
		break 'counting_up
		}
		}
	}
}
```

### loop through collection by 'for'

- example

```rust
let a=[1,2,3]
for element in a{
  println!("{}",element);
}
// loop through Range
for num in (1..4).rev(){
  println!("{}",num);
}

```
