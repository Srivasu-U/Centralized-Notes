## Pointers, structs and interfaces

- **Pointers** are really useful when utilizing variable of large sizes. Often a good practice to always just pass references for structs,  for example, instead of an entire struct, a reference to the struct can be passed instead
- Note: [Useful article](https://medium.com/@mathieu.durand/how-to-use-golang-interface-vs-java-1fc8b281c101) to the differences in Interfaces between Java and Golang
    - Another [article](https://gobyexample.com/interfaces) showing a clear example of the usage of interfaces at a basic level
- Interfaces are the one thing in Golang from OOP. It does not have classes. Interfaces can be declared using 
```
type X interface {
    methodX() return_type
}
```
- Inheritance or implementation of interfaces can also work like this 
```
type Y interface {
    X       // Here, Y implements methodX() from X as well. Y **must** provide its own implementation of methodX()
    methodY() return_type
}
```
- Interfaces can somehow be struct elements?, ie, structs implement interfaces. I am not sure how
- Interfaces can be parameters to functions