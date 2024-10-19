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
- Been noticing a lot of methods that return only an `error` as a return value. If that method evaluates correctly, then the return value is `nil`, aka, in the check after the function call, a normal `if err != nil {//Handle the error}` can be used
  - If an actual error is to be thrown then the `fmt.Errorf()` method can be used which creates a formatted string to be thrown as an error
  ```
  err := funcToBeCalled()
  if err != nil {
    // Handle the error, aka, failure case, end exec here
  }
  
  func funcToBeCalled() error {
    return fmt.Errorf() // in case of error
    return nil // No error, successful exec
  }
  ```

### Slices
- Slices in Golang have `length` and `capacity`
  - Syntax: `arr := [<len>]<type>{<value-list>}`. Ex: ` s := [5]int{}` -> Creates a slice of arrays with capacity 5 but length 0
    - Can also use `make()`. Ex: `s := make([]int, 0, 5)` -> Same as above
  - Length is the number of elements actually in an array
  - Capacity is the underlying capacity, ie, how much it *can* hold
  - Retrieved using `len(arr)` and `cap(arr)`
  - Slices of slices are possible like `[][]int`. Essentially a 2D matrix
  - `append()` is used as follows: `s = append(s, newElem)` -> Returns a new slice with the newElem appended

### Maps
- Key-value pairs as usual
- Syntax: `mapA := map[int]string` -> Creates a map with int keys and string values
  - Can also be `mapA := make(map[int]string)`

### Terminal commands  
- List of useful terminal commands for Golang
  - `go mod init <name>` to create mod file. `name` is generally started with `github.com` as a convention but not enforced
  - `go run main.go` while being in the directory that the `main.go` is present in.
  - `go test ./<dir-name>` to run the test file within the specified folder
    - `go test -run <test-name> ./<dir-name>` to run a specific test
  - `go build -o <dir-name> . && ./<dir-name>` to build the executable file

### JSON and webapp stuff
- This is called `JSON Marshalling`
```
type RegisterUserPayload struct {
	FirstName string `json:"firstName"`
	LastName  string `json:"lastName"`
	Email     string `json:"email"`
	Password  string `json:"password"`
}
```
- Basically converting a struct and it's values into equivalent json values. The reverse is called `unmarshalling`