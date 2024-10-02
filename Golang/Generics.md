## Generics

- Reference link: https://go.dev/doc/tutorial/generics
- Go functions can be written to work on multiple types using type parameters. The type parameters of a function appear between brackets, before the function's arguments.
```
func Index[T comparable](s []T, x T) int
```
- This declaration means that s is a slice of any type T and x is a value of type T that fulfills the built-in constraint *comparable*. 
- *comparable* basically means that anything that can work with **==** or **!=** 
- Another example:
```
// SumIntsOrFloats sums the values of map m. It supports both int64 and float64
// as types for map values.
func SumIntsOrFloats[K comparable, V int64 | float64](m map[K]V) V {
    var s V
    for _, v := range m {
        s += v
    }
    return s
}
```
- The above functions basically takes a single map as input param. The map must have a key that is of a *comparable* datatype, since all map keys must be comparable. 
- The values can be either int64 or float64
- The method also returns a value of type int64 or float64
- The **|** is called the union operator
- The function call can either mention the specific datatypes or let Go infer the datatypes
```
fmt.Printf("Generic Sums: %v and %v\n",
    SumIntsOrFloats[string, int64](ints),  // Specifying types
    SumIntsOrFloats[string, float64](floats))

fmt.Printf("Generic Sums, type parameters inferred: %v and %v\n",
    SumIntsOrFloats(ints),  // Letting Go infer types
    SumIntsOrFloats(floats))
```
- The `SumIntsOrFloats` method can also be modified by moving the union into it's own interface, or a *type constraint*
```
type Number interface {
    int64 | float64
}

func SumNumbers[K comparable, V Number](m map[K]V) V {
    var s V
    for _, v := range m {
        s += v
    }
    return s
}
```