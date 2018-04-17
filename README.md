# C+Alt
C+Alt (CplusAlt) is an alternative C++ standard library. It's designed to be used as an outright replacement for the C++ Standard Template Library, and **is not** directly compatible.

## What's wrong with C++'s Standard Template Library (STL)
STL is old. It was originally designed back in the late 80's and early 90's, back before the internet was prevelent and before internationalization was an everyday problem. A **huge** amount of important software is written in C++, so while C++ and STL can evolve, it can-not break compatibility. To much important code relies on it.

Even with all the improvements to the C++ language made by the ISO C++ comittee, when compared to competing languages, in practice C++ with the STL _is not_ a good language for new software.

C+Alt is a reboot. Starting with the C standard library, it throws away the names, legacy, and heavy templating of the original. That said, templating is still used in C+Alt, but the goal is to provide simpler classes with better every-day defaults.

## What does C+Alt code look like?
Work in progress


### Simple Mode
```c++
#include <alt.hpp>
using namespace alt;

int main( int argc, char* argv[] ) {
  Array<> myArray = { 10, 20, 30 };
  String text = "myArray has " + size(myArray) + u8" elements 😊. " + length("dog");
  printn(text);

  return 0;
}
```

### Verbose Mode

```c++
#include <alt/lib.hpp>
#include <alt/array.hpp>
#include <alt/string.hpp>

int main( int argc, char* argv[] ) {
  alt::Array<int> myArray = { 10, 20, 30 };
  alt::String text = "myArray has " + alt::size(myArray) + u8" elements 😊. " + alt::length("dog");
  alt::printn(text);
  
  returnif(!myArray.size(), 1);

  return 0;
}
```

### Details
* `alt::print` prints a string
* `alt::printn` prints a string, and appends a newline to the end of the string
* `alt::size(val)` typically invokes the `val.size()` method 
* `alt::length(val)` typically invokes the `val.length()` method, or a UTF-8 friendly strlen.


## C++ Language/Compiler Wishlist
* Some way to set the default string format to UTF-8, without the `u8` string prefix.
* `returnif` as a language feature instead of macro (because `void` returns are weird)
  * `returnif(success);` returns value of `success` if condition `success` is true.
  * `returnif(success, 1)` returns value of `1` if condition `success` is true.
  * `returnif(success);` when return is void to return nothing (instead of having to use `returnifvoid(success);`.
  * `returnif success;` syntax variation.
  * `returnif (success);` syntax variation (i.e. macros require no space between `name` and `(`).
  * `return if (success);` or `return if (success) 1;` syntax variation(s).
    * this is probably a really difficult sell.
* `breakif` and `continueif` as language features, with the syntax variations above.
* Word operators, or implicit functions
  * i.e. `vec4 v = p1 cross p2;` for cross product (instead of `vec4 v = cross(p1, p2);`

## C+Alt Wishlist
* SIMD, vector, and matrix math as a first class members of Math library (GLSL syntax)
* Signal operations (smoothstep) as first class members of Math library
* `Flex` type as default for all containers (i.e. `alt::Array<>` == `alt::Array<Flex>`)
* JSON, XML parsing (core lib or addon?)
* Networking (core lib or addon?)
