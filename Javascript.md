## 100 concepts

- You can run javascript on browser or a seperate runtime such as node
- V8 engine is used the browser to JIT the code
- Any thing thats not primitive type will inherit from the object class
- Lexical environment is different scopes in the code:
    -  Global - available everywhere
    -  Function - if its part of the function then its local to that function.  Using var can hoist block scoped variables
    -  Block - this is available within a conditional but not outside of it
- Functions are just objects that can be called by themselves are assigned to a value
- Higher order functions example:
```javascript
function higherOrder(fun){
    fun()
    return function() {
    }
}
```
- Closure:
```javascript
function giveMeClosure(){
    // stored in heap memory
    // which means this will persist between function calls
    let a = 10; 
    return function(){
        a++
        return a
    }
}
```
- When this is called without binding its attached to global or window object 
- When you bind an object to a function, then it will be attached to that object
- Primitives are passed by value which means the it we be a copy of the original value.
- Objects are pass by reference, which means its just a pointer to the original object.
- Javascript uses prototypical inheritence.
```javascript
// Recommended way to get prototype
Object.getPrototypeOf(human)
```
- Supports class based syntax but still uses the prototype under the hood
- You can create instance methods which will only effect the instance of the class
- You can also create static methods which are called on the class, not instance

main thread is where all the code is executed
thread pool is where all the async/callback code is waiting to be executed

functions like set time out gets put into the event loop to be executed after the
sync code has been finished in the current stack

if you use async await functions you need to wrap the code in a try catch for error handling

