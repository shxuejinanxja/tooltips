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

## Reference and borrowing

> a reference is like a pointer in that it's an address we can follow to access the data that stored at that address;that data is owned by some other variable. Unlike a pointer, a reference is guaranteed to point to a valid value of a particular type for the life of that reference.

### mutable Reference

one restriction: if you have a mutable reference to a value, you can have no other reference(mutable or immutable) to that value.

### dangling reference

> if you have a reference to some data, the compiler will ensure that the data will not go out of scope before the reference to the data does.

## macros

### println!

by default the curly brackets tell println! to use formatting known as Display to output intended for direct end user consumption.

### debug!

dbg! will return the ownship of the expression's value.

## slice

> a slice is kind of reference, so it does not have ownship. it let you reference a contiguous sequence of elements in a collection rather than the whole.

### string slice

```rust
fn main() {
    let s = String::from("hello world");

let hello = &s[0..5];
	let world = &s[6..11];

}

```

## struct

### struct update

the sync `..` specifies that the remaining field not explicitly set should have the same value as the fields in the given instance.

```rust
let user2=User{
email:String::from("another email"),
..user1
}

```

be aware that if the user one contain field like name:String then the data in the name field of user1 will be move to user2. it will make user1.name not usable.
but other field in the user1 is still accessable if they implement Copy trait.

### tuple struct

it have the added meaning the struct name provides but don't have names accociated with their fields.

```rust
struct Color(i32,i32,i32)
struct Point(f32,f32,f32)
let black=Color(0,0,0);
let origin=Point(0.0,0.0,0.0);

```

### unit-like structs without any fields

just like unit tuple which is `()`. the unit tuple represent an empty value
unit like struct is useful when you need to implement a trait on some type but don't have any data that you want to store in the type itself.

```rust
struct AlwaysEqual
let subject=AlwaysEqual;

```

### accociated functions

all functions defined within an impl block are called accociated functions because they are associated with the type named after impl.

## enum

it's more than a type .
the key of enum is variants.
each variant in one enum type should have distinct boundary.
but the variant could be different type.

> enum give you a way of saying a value is one of a possible set of values.

enum can be used in function signiture as other types.

- variants of enum can be different type or even empty
- we can also define methods on enum

### Enum Option

> programming language design is often thought of in terms of which features you include, but the features you exclude are important too.
> Null: is a value that means there is no value there.
> Rust **does not** have the Null feature
> in languagewith null, variables can always be in one of two states: null or not-null.

> The Option<T> enum is so useful that it’s even included in the prelude; you don’t need to bring it into scope explicitly. Its variants are also included in the prelude: you can use Some and None directly without the Option:: prefix. The Option<T> enum is still just a regular enum, and Some(T) and None are still variants of type Option<T>.

Enum Option is very important. Be familiar with it's method can bring you benefits.

### match

_match_ is a extremely powerful control flow that allows you to compare a value against a series of **patterns** and then execute code based on which pattern matches.
it's like a coin machine.

#### patterns that bind to value

match arms can bind to the parts of the values that match the pattern. So we can extract value out of enum variants.

### if let

`if let` look not like if +let. it more like a
if let <pattern> =< enum>.

> The syntax if let takes a pattern and an expression separated by an equal sign. It works the same way as a match, where the expression is given to the match and the pattern is its first arm.
> use if let will lost the exhaustive check since it only compare one pattern.

the `else` in `if let ` pair is the `_` case.

## module system

package ,crate, moduel and path

### crate and package

> A crate is the smallest amount of code that the Rust compiler considers at a time.

- binary crate
- library crate

> A package is a bundle of one or more crates that provides a set of functionality.
> a package contains a Cargo.toml that describe how to build those crates
> if a pabke contains src/main.rs and src/lib.rs, it has two crates: a binary crate and a library crate
> A package can have multiple binary crates by placing files in the src/bin directory: each file will be a separate binary crate.

### modules cheat sheet

- start from crate root
- declaring modules
  - declare module in crate root file `mod garden`, then it will looking for
    - inline, within curly brackest that replace the semicolon following `mod garden`
    - in the file src/garden.rs , it's a new style
    - in the file src/garden/mod.rs , it's a older style
      you can't use both style for the same module. but using a mix of both styles for different modules in the same project is allowed.
- declaring submodules
  > In any file other than the crate root, you can declare submodules. For example, you might declare mod vegetables; in src/garden.rs. The compiler will look for the submodule’s code within the directory named for the parent module in these places:
  - inline, within curly brackest that replace the semicolon following `mod vegetables`
  - in the file src/garden/vegetables.rs
  - in the file src/garden/vegetables/mod.rs
- paths to code in modules
  > Once a module is part of your crate, you can refer to code in that module from anywhere else in that same crate, as long as the privacy rules allow, using the path to the code. For example, an Asparagus type in the garden vegetables module would be found at crate::garden::vegetables::Asparagus
- private vs public
  > Code within a module is private from its parent modules by default. To make a module public, declare it with pub mod instead of mod. To make items within a public module public as well, use pub before their declarations.
  > Items in a parent module can’t use the private items inside child modules, but items in child modules can use the items in their ancestor modules. This is because child modules wrap and hide their implementation details, but the child modules can see the context in which they’re defined.
  > In the absolute path, we start with crate, the root of our crate’s module tree. The front_of_house module is defined in the crate root. While front_of_house isn’t public, because the eat_at_restaurant function is defined in the same module as front_of_house (that is, eat_at_restaurant and front_of_house are siblings), we can refer to front_of_house from eat_at_restaurant.
  > Enums aren’t very useful unless their variants are public; it would be annoying to have to annotate all enum variants with pub in every case, so the default for enum variants is to be public. Structs are often useful without their fields being public, so struct fields follow the general rule of everything being private by default unless annotated with pub.
- the `use` keyword

  - it's idiomatic to bring a function into scope with use it's parent so it's clear that the function is not defined in the place of other place.

  ```rust
  use crate::front_of_house::hosting;
  pub fn eat_at_restaurant(){
  // it's clear here that add_to_waitlist is not defined in the root crate.
     hosting::add_to_waitlist();
  }

  ```

  - on the other hand, it's idiomatic to specific full path when bringing in struct, enums and other items.

  ```rust
  use std::collection::HashMap;
  fn main(){
    let mut map==HashMap::new();

  }

  ```

  - to avoid name collison when bring in two types of the same name into the same scope, we can specific as and a new local name. or alias, for the type.

  ```rust
  use std::fmt::Result;
  use std::io::Result as IoResult;

  ```

- Re-exporting
  > When we bring a name into scope with the use keyword, the name available in the new scope is private. To enable the code that calls our code to refer to that name as if it had been defined in that code’s scope, we can combine pub and use. This technique is called re-exporting because we’re bringing an item into scope but also making that item available for others to bring into their scope.
- using nested paths to clean up large use lists

```rust
use std::cmp::Ordering;
use std::io;
//equal
use std::{cmp::Ordering,io};

//other case
use std::io;
use std::io::Write;
//equal
use std::io::{self,Write};
```

- glob operator `*`
  > If we want to bring all public items defined in a path into scope, we can specify that path followed by the _ glob operator: `use std::collections::_;`

## data type

### how to check the variable type

```rust
use std::any::type_name
fn type_of<T>(_:T)->&'static str{
   type_name::<T>()
}

```

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
