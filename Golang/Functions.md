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


### Error Handling
- In terms of error handling, the fundamental thinking strategy for Golang is to always look at a function returning an `err` value if it fails, or `nil` if it succesfully passes.  
  - This is further enabled by the ability of methods in Go to return multiple values so having `int, err` return values is good
    - `int, nil` in case of successful execution or `nil, errVal` in case of failure
    - This is important because we need an error check, ie, `if err != nil { //handle err}` in most cases for most methods
    - This is how errors get propagated which I find to be more intuitive than `try..catch..finally` blocks
    - Still need to figure out best practices around error handling and how much you can propagate errors
- Golang convention: Error messages must not be capitalized, i.e, `invalid operation` over `Invalid operation`
  - This throws a warning on the linter/compiler, though not an error. At least on `staticcheck`


### Anonymous functions
- In Go, *anonymous functions* or `inline functions` or `function literals` also exist. Syntax as such
```
func(parameter_list)(return_type){
[...]
}(inputParams)
```
- You are allowed to assign an anonymous function to a variable. When you assign a function to a variable, then the type of the variable is of function type and you can call that variable like a function call.
```
func main() {   
    // Assigning an anonymous  
   // function to a variable 
   value := func(){ 
      fmt.Println("Welcome! to GeeksforGeeks") 
  } 
  value() 
} 
```
- Passing arguments works as such
```
func main() { 
      
    // Passing arguments in anonymous function 
  func(ele string){ 
      fmt.Println(ele) 
  }("GeeksforGeeks") 
    
} 
```