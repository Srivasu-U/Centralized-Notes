## Functions

- - Function declarations and calls are surprisingly intuitive. For example
```
  func A(input string) int {
    // This function takes an input string and returns an integer value, ie, var output int = A("hello"). 
    // This is called a function
  } 

  func (input string) A() int {
    // This function takes no input but is instead called using a dot operator after a string and returns an int,  
    // ie, var output int = "hello".A()
    // Conventionally, this style is called a method
  }
```
- Functions can also have multiple return values. Probably one of the best things about golang
```
func A(x, y int) (string, string) {...}
```
- Variable number of params can be set to functions with this format 
```
func name(args ...<datatype>) {...}
```
- - In Golang, only methods or values starting with a capital letter can be exported. For example, in the `lexer.go` file
`New()` and `NewToken()` are exportable methods while `isDigit()` and others are not.