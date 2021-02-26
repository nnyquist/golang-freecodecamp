# freeCodeCamp.org Golang Training Course

[Video Course](https://www.youtube.com/watch?v=YS4e4q9oBaU)

> Learn the Go programming language (Golang) in this step-by-step tutorial course for beginners. Go is an open source programming language designed at Google that makes it easy to build simple, reliable, and efficient software.

## Useful Resources

- [Go Website](https://www.golang.org)
- [Golang Bridge](https://golangbridge.org)

## Summary Information

### Arrays

- Collection of items with same type
- Fixed size
- Declaration styles
  - `a := [3]int{1, 2, 3}`
  - `a := [...]int{1, 2, 3}`
  - `var a [3]int`
- Access via zero-based index
  - `a := [3]int{1, 3, 5} // a[1] == 3`
- `len` function returns the size of the array
- Copies refer to different underlying data

### Slices

- Backed by array
- Creation styles
  - Slice existing array or slice
  - Literal style
  - Via `make` function
    - `a := make([]int, 10) // create slice with capacity and length == 10`
    - `a := make([]int, 10, 100) // slice with length == 10 and capacity == 100`
- `len` function returns length of slice
- `cap` functions returns length of underlying array
- `append` functions to add elements to slice
  - May cause expensive copy operation if underlying array is too small

### Maps

- Collection of value types that are accessed via keys
- Created via literals or via `make` function
- Members accessed via `[key]` syntax
  - `myMap["key"] = "value"`
- Check for presence with `value, ok` form of result
- Multiple assignments refer to the same underlying data

### Structs

- Collections of disparate data types that describe a single concept
- Keyed by named fields
- Normally created as types, but anonymous structs are allowed (although rare)
- Structs are value types
- No inheritance, but can use composition via embedding
- Tags can be added to struct fields to describe field

### If Statements

- Initializer
- Comparison operators
- Logical operators
- Short circuiting
- `If-else` statements
- `If-else if` statements
- Equality and floats

### Switch Statements

- Switching on a tag
- Cases with multiple tests
- Initializers
- Switches with no tags, more verbose syntax
- Fallthrough
  - Go has implicit breaks and explicit fallthrough
  - Any additional case logic is ignored, the next statements will execute regardless
- Type switches
  - `i.(type)`
- Breaking out early

### Looping

- For statements
- simple loops
  - `for initializer; test; incrementer {}`
  - `for test {}`
  - `for {}`
- exiting early
  - `break`
  - `continue` - breaks out of current iteration and goes back to the incrementer
  - labels
- looping over collections
  - arrays, slices, maps, strings, channels
  - `for k, v := range collection {}`

### Defer

- Used to delay the execution of a statement until function ends
- Useful to group "open" and "close" functions together
  - Be careful of loops
- Run in LIFO (last-in, first-out) order
- Arguments evaluated at time defer is executed, not at time of called function execution

### Panic

- Occur when program cannot continue at all
  - Don't use when file can't be opened, unless it is critical
  - Use for unrecoverable events - cannot obtain TCP port for web server
- Function will stop executing
  - Deferred functions will still fire
- If nothing handles panic, program will exit

### Recover

- Used to recover from panics
- Only useful in deferred functions
- Current function will not attempt to continue, but higher functions in call stack will

### Pointers

- Creating pointers
  - Pointer types use an asterisk `*` as a prefix to type pointed to
    - `*int` - a pointer to an integer
  - Use the addressof operator `&` to get address of variable
- Dereferencing pointers
  - Dereference a pointer by preceding with an asterisk `*`
  - Complex types (e.g., structs) are automatically dereferenced
- Create pointers to objects
  - Can use the addressof operator `&` if value type already exists
    - `ms := myStruct{foo: 42}`
    - `p  := &ms`
  - Use addressof operator befor initializer
    - `&myStruct{foo: 42}`
  - Use a `new` keyword
    - Can't initialize fields at the same time
- Types with internal pointers
  - All assignment operations in Go are copy operations
  - Slices and maps contain internal pointers, so copies point to same underlying data

### Functions

- Basic Syntax
  - `func foo() {...}`
- Parameters
  - Comma delimited list of variables and types
    - `func foo(bar string, baz int)`
  - Parameters of the same type list type once
    - `func foo(bar, baz int)`
  - When pointers are passed in, the function can change the value in the caller
    - This is always true for data of slices and maps
  - Use variadic parameters to send list of same types in
    - Must be last parameter
    - Received as a slice
    - `func foo(bar string, baz ...int)`
- Return values
  - Single return values just list type
    - `func foo() int`
  - Multiple return value list types surrounded by parentheses
    - `func foo() (int, error)`
    - The `(result type, error)` paradigm is a very common idiom
  - Can use named return values
    - Initializes returned variable
    - Return using `return` keyword on its own
  - Can return addresses of local variables
    - Automatically promoted from local memory (stack) to shared memory (heap)
- Anonymous functions
  - Functions don't have names if they are:
    - Immediately invoked
    - Assigned to a variable or passed as an argument to a function
- Functions as types
  - Can assign functions to variables or use as arguments and return values in functions
  - Type signature is like function signature, with no parameter names
    - `var f func(string, string, int) (int, error)`
- Methods
  - Function that executes in context of a type
  - Format:
    - `func (g greeter) greet() {...}`
    - `g` is a value receiver
  - Receiver can be value or pointer
    - Value receiver gets copy of type
    - Pointer receiver gets pointer to type