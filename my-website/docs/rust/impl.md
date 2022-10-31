The impl keyword is primarily used to define implementations on types. Inherent implementations are standalone, while trait implementations are used to implement traits for types, or other traits.

Functions and consts can both be defined in an implementation. A function defined in an impl block can be standalone, meaning it would be called like Foo::bar(). If the function takes self, &self, or &mut self as its first argument, it can also be called using method-call syntax, a familiar feature to any object oriented programmer, like foo.bar().

```
struct Example {
    number: i32,
}

impl Example {
    fn boo() {
        println!("boo! Example::boo() was called!");
    }

    fn answer(&mut self) {
        self.number += 42;
    }

    fn get_number(&self) -> i32 {
        self.number
    }
}

trait Thingy {
    fn do_thingy(&self);
}

impl Thingy for Example {
    fn do_thingy(&self) {
        println!("doing a thing! also, number is {}!", self.number);
    }
}
```

The other use of the impl keyword is in impl Trait syntax, which can be seen as a shorthand for “a concrete type that implements this trait”. Its primary use is working with closures, which have type definitions generated at compile time that can’t be simply typed out.

```
fn thing_returning_closure() -> impl Fn(i32) -> bool {
    println!("here's a closure for you!");
    |x: i32| x % 3 == 0
}
```