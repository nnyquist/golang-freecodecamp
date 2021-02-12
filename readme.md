# freeCodeCamp.org Golang Training Course

[Video Course](https://www.youtube.com/watch?v=YS4e4q9oBaU)
>Learn the Go programming language (Golang) in this step-by-step tutorial course for beginners. Go is an open source programming language designed at Google that makes it easy to build simple, reliable, and efficient software.

## Useful Resources
* [Go Website](https://www.golang.org)
* [Golang Bridge](https://golangbridge.org)

## Summary Information

### Arrays
* Collection of items with same type
* Fixed size
* Declaration styles
    * `a := [3]int{1, 2, 3}`
    * `a := [...]int{1, 2, 3}`
    * `var a [3]int`
* Access via zero-based index
    * `a := [3]int{1, 3, 5} // a[1] == 3`
* `len` function returns the size of the array
* Copies refer to different underlying data

### Slices
* Backed by array
* Creation styles
    * Slice existing array or slice
    * Literal style
    * Via `make` function
        * `a := make([]int, 10) // create slice with capacity and length == 10`
        * `a := make([]int, 10, 100) // slice with length == 10 and capacity == 100`
* `len` function returns length of slice
* `cap` functions returns length of underlying array
* `append` functions to add elements to slice
    * May cause expensive copy operation if underlying array is too small
