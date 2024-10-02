## General Golang notes
- Valuable links: 
  - [Go By Example](https://gobyexample.com/)
  - [Tour of Go](https://go.dev/tour/list) 
  - [Effective Go](https://go.dev/doc/effective_go)
  - String formatting reference: [click here](https://gobyexample.com/string-formatting)

- Single chars must be enclosed in *single quotes(')*, double quotes will only work for strings
- `:=` is called the short assignment operator. It both declares and assigns a variable, and implicitly decides on the datatype as well
  - An example: `var i int =  5` can be shortened as `i := 5`, unless the declaration and assignment needs to be separate as shown  
  in the switch case of the `nextToken()` in `lexer.go`
- Consts do not use datatypes or the short hand operator `:=`

- Test methods but always start with a capital letter T and follow the format `func TestXxx(t *testing.T) {...}`.  
This must be done in a file called `something_test.go` where the method under test is `something.go`. Both must be in the same package.
- Imports from other files must always start from the actual directory of the `go.mod`. For example, `import "Interpreter/monkey-v1/token"` is the correct way, not `import "monkey=v1/token"` unless the *monkey-v1* directory has a `go.mod`. 


- Type convertion works like this: `datatype(value)`. Example: `float64(2)` converts int 2 into float64
- We also have type checking/assertion like this: `ident.(type)`. Example: `value.(string)` checks if value contains a string expression
- This is how to get the datatype of an identifier/variable
```
dataType := variableName.(type)
```
- Interesting error message: `impossible type assertion: program.Statements[0].(*ast.Statement)
	*ast.Statement does not implement ast.Statement (type *ast.Statement is pointer to interface, not interface)`. What does this mean?

- Enums are not a thing in Golang but we can use custom types and const as a way to enforce type safety as done in `token.go` and `object.go`
- The datatype `interface{}` can be used to send a value of any type. This can be used either in structs or even as params to methods
- Arrays in go have two values attached with them: `length` and `capacity`
  - For example `make([]int, 0, 10)` returns an array (also called a `slice` in Golang), of size 0 but it's underlying *capacity* is 10, i.e, it can hold 10 values, but it is currently empty.
    - Thus, the length of a slice is *always* less than or equal to its capacity. This helps with memory conservation.