# Go

- [Go](#go)
  - [Compiled or Interpreted?](#compiled-or-interpreted)
  - [Is Go Object Oriented?](#is-go-object-oriented)
  - [What Go Doesn't Support](#what-go-doesnt-support)
  - [Essential Syntax Rules](#essential-syntax-rules)
    - [Semicolons Usually Not Needed](#semicolons-usually-not-needed)
    - [Code Blocks with Braces](#code-blocks-with-braces)
    - [Built-In Functions](#built-in-functions)
  - [Storing Data in Variables](#storing-data-in-variables)
    - [Boolean and String Types](#boolean-and-string-types)
    - [Integer Types](#integer-types)
    - [Other Numeric Types](#other-numeric-types)
    - [Complex Types](#complex-types)
    - [Math Requires Identical Types](#math-requires-identical-types)
  - [make vs new](#make-vs-new)
  - [Arrays](#arrays)
  - [Slices](#slices)
  - [Slices vs Arrays](#slices-vs-arrays)
  - [Maps](#maps)
  - [Structs](#structs)
  - [Switch Statement](#switch-statement)
  - [Looping](#looping)
    - [LoopingOver Collections](#loopingover-collections)
  - [Methods in Types](#methods-in-types)
  - [Pointers](#pointers)
    - [Creating pointers to variables](#creating-pointers-to-variables)
  - [Iota](#iota)
  - [Functions](#functions)
    - [Variadic Functions](#variadic-functions)
    - [Making Functions Public](#making-functions-public)
    - [Naming Return Values](#naming-return-values)
    - [Receivers](#receivers)
      - [Value Based Receivers](#value-based-receivers)
      - [Pointer Based Receivers](#pointer-based-receivers)
    - [Anonymous Functions](#anonymous-functions)
    - [Returning Functions from Functions](#returning-functions-from-functions)
    - [Functions as Parameters](#functions-as-parameters)
    - [Stateful Functions](#stateful-functions)
  - [Error Handling](#error-handling)
    - [Defer Functions](#defer-functions)
    - [Panics](#panics)
      - [Recovering from Panics](#recovering-from-panics)
  - [Threads vs Goroutines](#threads-vs-goroutines)
    - [Thread](#thread)
    - [Goroutine](#goroutine)
  - [Wait Groups](#wait-groups)
  - [Mutex (Mutual Exclusion Lock)](#mutex-mutual-exclusion-lock)
    - [RWMutex](#rwmutex)
  - [Channels](#channels)
    - [Unbuffered Channels](#unbuffered-channels)
    - [Buffered Channels](#buffered-channels)
    - [Channel Types](#channel-types)
    - [Closing Channels](#closing-channels)
      - [Checking for closed channels](#checking-for-closed-channels)
      - [Using Channels in Loops](#using-channels-in-loops)
    - [Select Statements](#select-statements)

## Compiled or Interpreted?

- Go is a compiled, statically typed language
- The Go tool can run a file without precompiling
- Compiled executables are OS specific
- Compiled apps contain a statically linked runtime
- No external VM needed

## Is Go Object Oriented?

- Everything is a type in Go
- Go has some object-oriented features
  - You can define custom interfaces
  - Custom types can implement one or more interfaces
  - Custom types can have function methods
  - Custom structs (data structures) can have member fields and member methods

## What Go Doesn't Support

- Type inheritance (no classes)
- Method or operator overloading
- Structured exception handling
  - No try catch keywords
  - Error objects are returned by functions that generate those errors which conditional logic can be used to examine
- Implicit numeric conversions

## Essential Syntax Rules

- Go is case sensitive
- Variable and package names are lowercase and mixed case
- Names of public fields have initial uppercase characters
- Initial uppercase character means the symbol is exported (equivalent to public in Java or C#)
- Initial lower case character means the symbol is not exported (private in Java or C#)

### Semicolons Usually Not Needed

- Line feed ends a statement; no semicolon required
- Semicolons are part of the formal language spec
- The lexer adds them as needed

### Code Blocks with Braces

- Code blocks are wrapped in braces

### Built-In Functions

- Members of builtin package
  - len(string) - returns the length of a string
  - panic(error) - stops execution; displays error message

## Storing Data in Variables

- Go is a statically typed language
- All variables have assigned types
- You can set types explicitly or implicitly

### Boolean and String Types

- Boolean values
  - bool
- String type
  - string

### Integer Types

- Fixed integer types
  - uint8
  - uint16
  - uint32
  - uint64
  - int8
  - int16
  - int32
  - int64
- Aliases can be used instead of full type names
  - byte
  - uint
  - int
  - uintptr

### Other Numeric Types

- Floating values
  - float32
  - float64
- Complex numbers
  - complex64
  - complex128

### Complex Types

- Data collections
  - Arrays
  - Slices
  - Maps
  - Structs
- Language organization
  - Functions
  - Interfaces
  - Channels
- Data management
  - Pointers

### Math Requires Identical Types

- Numeric types don't implicitly convert
- Convert types before using
  - Wrap value in target type as function call
- For other operations, use math package

## make vs new

- make initializes slice, map, and channel (make initializes memory)
- new only allocates memory

## Arrays

- Cannot be sorted
- Elements be added or removed at runtime

## Slices

- Abstraction layer on top of arrays

## Slices vs Arrays

- Slices enable resizing and sorting

```go
  var colors = [5]string // array
  var colors = []string // slice
```

```go
  func main() {
    arr := [3]int{1, 2, 3}
    slice := arr[:] // create a slice from start to end of arr
    arr[1] = 42
    slice[2] = 27
    fmt.Println(arr, slice) // [1 42 27] [1 42 27] -> slice points to arr
  }
```

## Maps

```go
  func main() {
    m := map[string]int{"foo": 42} // create a map with strings as keys and ints as values
    delete(m, "foo") // delete key-value pair with key of "foo"
  }
```

## Structs

- Structs can have fields with different data types

```go
  type user struct {
    ID int
    FirstName string
    LastName string
  }
  var u user
  fmt.Println(u) // {0 } -> struct initialized with 0 and empty strings
  u.ID = 1
  u.FirstName = "Arthur"
  u.LastName = "Dent"
  fmt.Println(u) // {1 Arthur Dent}

  u2 := user{ID: 1, FirstName: "Arthur", LastName: "Dent"}
```

## Switch Statement

- In Go, as soon as one of the condition evaluates to ```true```, Go will go to the end of the switch statement. Therefore, Go has no ```break``` keyword
- If we want to evaluate multiple cases in a switch statement, we can use the ```fallthrough``` keyword, which will make Go evaluate the next case

## Looping

- In Go, there is no ```while``` statements

### LoopingOver Collections

```go
  func main() {
    slice := []int{1, 2, 3, 4}
    for i, v := range slice {
      println(i, v)
    }

    ports := map[string]int{"http": 80, "https": 443}
    for k, v := range ports {
      println(k, v)
    }
  }
```

## Methods in Types

```go
func main() {
  poodle := Dog{"Poodle", 10, "Woof"}
  fmt.Println(poodle)
  fmt.Printf("%+v\n", poodle)
  fmt.Printf("Breed: %v\nWeights: %v\n", poodle.Breed, poodle.Weight)

  poodle.Speak()
}

type Dog struct {
  Breed string
  Weight int
  Sound string
}

// (d Dog) is a receiver, which is the same as the "this" keyword
func (d Dog) Speak() {
  fmt.Println(d.Sound)
}

// if you want to use the same copy of Dog, use a pointer
func (d *Dog) Speak() {
  fmt.Println(d.Sound)
}
```

## Pointers

```go
  // creating an uninitialized pointer (pointer to nothing)
  var firstName *string

  // creating an initialized pointer
  var firstName *string = new(string)

  // dereferencing a pointer (set value at address of firstName to ...)
  *firstName = "Arthur"

  // dereferencing a pointer (get value at address of firstName)
  fmt.Println(*firstName)
```

### Creating pointers to variables

```go
  // creating a pointer to a variable
  firstName := "Arthur"
  fmt.Println(firstName)

  // address of ... operator
  ptr := &firstName
```

## Iota

```go
  const (
    first = iota
    second = iota
  )

  func main() {
    fmt.Println(first, second) // 0 1
  }
```

```go
  const (
    first = iota + 6
    second
  )

  func main() {
    fmt.Println(first, second) // 6 7
  }
```

Every time iota is used, its value is incremented by one. Iota is scoped to its const block

## Functions

- Go can return multiple values

```go
  func main() {
    answer, err := divide(6, 0)
    if err != nil {
      fmt.Printf("Error: %s\n", err.Error())
    } else {
      fmt.Printf("%f\n", answer)
    }
  }

  func divide(p1, p2 float64) (float64, error) {
    if p2 == 0 {
      return math.NaN(), errors.New("Cannot divide by zero")
    }
    return p1 / p2, nil
  }
```

### Variadic Functions

```go
  func main() {
    numbers := []float64{12.2, 14, 16, 22.4}
    total := sum(numbers...)
  }

  func sum(values ...float64) float64 {
    total := 0.0
    for _, value := range values {
      total += value
    }
    return total
  }
```

### Making Functions Public

- To make functions public, capitalize the name of the function

### Naming Return Values

```go
  func divide(p1, p2 float64) (answer float64, err error) {
    if p2 == 0 {
      err = errors.New("Cannot divide by zero")
    }
    answer = p1 / p2
    return
  }
```

### Receivers

#### Value Based Receivers

- Value based receivers make a copy of the object it refers to when it's called

```go
  func (sv SemanticVersion) IncrementMajor() {
    sv.major += 1
  }
```

#### Pointer Based Receivers

- Pointer based receivers modifies the current object it refers to when it's called

```go
  func (sv *SemanticVersion) IncrementMajor() {
    sv.major += 1
  }
```

### Anonymous Functions

```go
  func main() {
    func() {
      println("anonymous function")
    }()
  }
```

### Returning Functions from Functions

```go
  func main() {
    addExpr := mathExpression()
    println(addExpr(2, 3))
  }

  func mathExpression() func(float64, float64) float64 {
    return func(f1 float64, f2 float64) float64 {
      return f1 + f2
    }
  }
```

### Functions as Parameters

```go
  const (
    AddExpr = MathExpr("add")
    SubtractExpr = MathExpr("subtract")
    MultiplyExpr = MathExpr("multiply")
  )

  func main() {
    fmt.Printf("%f", double(3, 2, mathExpression(AddExpr)))
  }

  func Add(f1, f2 float64) float64 {
    return f1 + f2
  }

  func mathExpression(expr MathExpr) func(float64, float64) float64 {
    switch expr {
      case AddExpr:
        return Add
      case SubtractExpr:
        return Subtract
      case MultiplyExpr:
        return Multiply
      default:
        return func(f1, f2 float64) float64 {
          return 0
        }
    }
  }

  func double(f1, f2 float64, mathExpr func(float64, float64) float64) float64 {
    return 2 * mathExpr(f1, f2)
  }
```

### Stateful Functions

```go
  func main() {
    p2 := powerOfTwo()
    value := p2()
    println(value) // 4
    value = p2()
    println(value) // 9
  }

  func powerOfTwo() func() int64 {
    x := 1.0
    return func() int64 {
      x += 1
      return int64(math.Pow(x, 2))
    }
  }
```

## Error Handling

```go
  func ReadSomething() error {
    var r io.Reader = BadReader{errors.New("bad reader")}
    value, err := r.Read([]byte("test"))
    if err != nil {
      fmt.Printf("error %s", err)
      return err
    }
    println(value)
    return nil
  }

  type BadReader struct {
    err error
  }

  func(br BadReader) Read(p []byte) (n int, err error) {
    return -1, br.err
  }
```

### Defer Functions

- defer function executes when the parent function returns
- it's possible to have more than one defer function
- defer functions are placed onto and removed from a stack (LIFO)

```go
  func ReadFullFile() error {
    var r io.ReadCloser = &SimpleReader{}
    defer func() { _ = r.Close() }()
    defer func() {
      println("second defer")
    }
    for {
      value, err := r.Read([]byte("some text"))
      if err == io.EOF {
        println("finished")
        break
      } else if err != nil {
        return err
      }
      println(value)
    }
  }

  type SimpleReader struct {
    count int
  }

  func (sr *SimpleReader) Read(p []byte) (n int, err error) {
    if sr.count > 3 {
      return 0, io.EOF
    }
    br.count += 1
    return br.count, nil
  }

  func (sr *SimpleReader) Close() error {
    return nil
  }
```

### Panics

- Panics are used when something unexpected happens when an application does not know how to recover from them

```go
  func (sr *SimpleReader) Read(p []byte) (n int, err error) {
    if sr.count == 2 {
      panic("Something bad happened")
    }
    if sr.count > 3 {
      return 0, io.EOF
    }
    br.count += 1
    return br.count, nil
  }
```

```go
  func mathExpression(expr MathExpr) func(float64, float64) float64 {
    switch expr {
      case AddExpr:
        return Add
      case SubtractExpr:
        return Subtract
      case MultiplyExpr:
        return Multiply
      default:
        panic("invalid math expression")
    }
  }
```

#### Recovering from Panics

- recover() stops the panicking sequence, grab the error from the panic and lets the developer handle the error

```go
  func ReadFullFile() (err error) {
    var r io.ReadCloser = &SimpleReader{}
    defer func() {
      _ = r.Close()
      if p := recover(); p != nil {
        err = errors.New("a panic occurred")
      }
    }()
  }
```

## Threads vs Goroutines

### Thread

- Have own execution stack
- Fixed stack space (~1MB)
- Managed by OS

### Goroutine

- Have own execution stack
- Variable stack space (starts @ 2KB)
- Managed by Go runtime

## Wait Groups

- A WaitGroup waits for a collection of goroutines to finish

```go
  func main() {
    wg := &sync.WaitGroup{}
    for i := 0; i < 10; i++ {
      id := rnd.Intn(10) + 1
      wg.Add(2) // increment tasks to wait on by the number of goroutines running
      go func(id int, wg *sync.WaitGroup) {
        if b, ok := queryCache(id); ok {
          fmt.Println("from cache")
        }
        wg.Done() // tell the wait group the goroutine is done
      }(id, wg)
      go func(id int, wg *sync.WaitGroup) {
        if b, ok := queryDatabase(id); ok {
          fmt.Println("from database")
        }
        wg.Done()
      }(id, wg)
    }
    wg.Wait() // wait until all goroutines are finished
  }
```

## Mutex (Mutual Exclusion Lock)

- Mutexes allow only one process to access shared memory at any given time

```sh
  go run --race . # looks for race condition when running a Go application
```

```go
  func main() {
    wg := &sync.WaitGroup{}
    m := &sync.Mutex{}
    for i := 0; i < 10; i++ {
      id := rnd.Intn(10) + 1
      wg.Add(2) // increment tasks to wait on by the number of goroutines running
      go func(id int, wg *sync.WaitGroup, m *sync.Mutex) {
        if b, ok := queryCache(id, m); ok {
          fmt.Println("from cache")
        }
        wg.Done() // tell the wait group the goroutine is done
      }(id, wg, m)
      go func(id int, wg *sync.WaitGroup, m *sync.Mutex) {
        if b, ok := queryDatabase(id, m); ok {
          fmt.Println("from database")
        }
        wg.Done()
      }(id, wg, m)
    }
    wg.Wait() // wait until all goroutines are finished
  }

  func queryCache(id int, m *sync.Mutex) (Book, bool) {
    m.Lock() // the goroutine that calls Lock() locks the mutex and prevents other code from accessing the mutex
    b, ok := cache[id]
    m.Unlock() // unlocks the mutex
    return b, ok
  }

  func queryDatabase(id int, m *sync.Mutex) (Book, bool) {
    time.Sleep(100 * time.Millisecond)
    for _, b := range books {
      if b.ID == id {
        m.Lock()
        cache[id] = b
        m.Unlock()
        return b, true
      }
    }
  }
```

### RWMutex

- RWMutex allows multiple readers and one writer to access shared memory
- If an application has many more readers and few writers, RWMutex can be used
- If an application has approximately the same number of readers and writers, use Mutex instead

```go
  func main() {
    wg := &sync.WaitGroup{}
    m := &sync.RWMutex{}
    for i := 0; i < 10; i++ {
      id := rnd.Intn(10) + 1
      wg.Add(2) // increment tasks to wait on by the number of goroutines running
      go func(id int, wg *sync.WaitGroup, m *sync.RWMutex) {
        if b, ok := queryCache(id, m); ok {
          fmt.Println("from cache")
        }
        wg.Done() // tell the wait group the goroutine is done
      }(id, wg, m)
      go func(id int, wg *sync.WaitGroup, m *sync.RWMutex) {
        if b, ok := queryDatabase(id, m); ok {
          fmt.Println("from database")
        }
        wg.Done()
      }(id, wg, m)
    }
    wg.Wait() // wait until all goroutines are finished
  }

  func queryCache(id int, m *sync.RWMutex) (Book, bool) {
    m.RLock() // allows multiple readers to acquire the read lock
    b, ok := cache[id]
    m.RUnlock() // unlocks the mutex
    return b, ok
  }

  func queryDatabase(id int, m *sync.RWMutex) (Book, bool) {
    time.Sleep(100 * time.Millisecond)
    for _, b := range books {
      if b.ID == id {
        m.Lock() // when writes happens, the mutex will let readers finish and then the writer come in
        cache[id] = b
        m.Unlock() // when the writer finishes, the mutex will unlock and let readers read
        return b, true
      }
    }
  }
```

## Channels

- In a channel, message senders and receivers know about the channel, but not about each other
- Channels must be used only in goroutines because they block operations in the threads they are on. Otherwise, they will cause deadlocks

```go
  // create a channel which sends and receives integers
  ch := make(chan int)

  // create a buffered channel which can store 5 messages
  ch := make(chan int, 5)
```

### Unbuffered Channels

```go
  func main() {
    wg := &sync.WaitGroup{}
    ch := make(chan int)
    wg.Add(2)
    go func(ch chan int, wg *sync.WaitGroup) {
      fmt.Println(<-ch) // receiving message from channel
      wg.Done()
    }(ch, wg)
    go func(ch chan int, wg *sync.WaitGroup) {
      ch <- 42 // sending message to channel
      wg.Done()
    }(ch, wg)
    wg.Wait()
  }
```

- In the above example, if the first goroutine happens first, it will then go to sleep until the second goroutine is done because there is no message in the channel
- When the second goroutine sends a message into the channel, the first goroutine wakes up to receive the message

### Buffered Channels

```go
  func main() {
    wg := &sync.WaitGroup{}
    ch := make(chan int, 1)
    wg.Add(2)
    go func(ch chan int, wg *sync.WaitGroup) {
      fmt.Println(<-ch) // receiving message from channel
      wg.Done()
    }(ch, wg)
    go func(ch chan int, wg *sync.WaitGroup) {
      ch <- 42 // sending message to channel
      ch <- 27
      wg.Done()
    }(ch, wg)
    wg.Wait()
  }
```

- In this example, the second goroutine will second message that will sit in a buffered channel. Without a buffered channel, the second message will cause a deadlock

### Channel Types

- Bidirectional
- Send-only
- Receive-only

```go
  ch := make(chan int) // bidirectional channel

  func myFunc(ch chan int) {} // passing bidirectional channel to a function

  func myFunc(ch chan<- int) {} // passing send-only channel

  func myFunc(ch <-chan int) {} // passing read-only channel
```

### Closing Channels

- Channels are closed through the close function
- Channels cannot be checked to determine whether they are close
- Sending messages into a closed channel will cause a panic
- Receiving messages from a closed channel is possible
  - If the channel is buffered, receive messages in buffer
  - if the channel is unbuffered or empty, receive 0
- Only a channel that sends messages can be closed. Channels that receive messages cannot be closed

#### Checking for closed channels

```go
  func main() {
    wg := &sync.WaitGroup{}
    ch := make(chan int, 1)
    wg.Add(2)
    go func(ch chan int, wg *sync.WaitGroup) {
      msg, ok := <-ch
      fmt.Println(msg, ok) // if ok is false, channel is closed
      wg.Done()
    }(ch, wg)
    go func(ch chan int, wg *sync.WaitGroup) {
      ch <- 42 // sending message to channel
      ch <- 27
      wg.Done()
    }(ch, wg)
    wg.Wait()
  }
```

#### Using Channels in Loops

```go
  func main() {
    wg := &sync.WaitGroup{}
    ch := make(chan int, 1)
    wg.Add(2)
    go func(ch chan int, wg *sync.WaitGroup) {
      for msg := range ch { // iterating using range requires the sender to close the channel to avoid a deadlock because range keeps listening for new messages
        fmr.Println(msg)
      }
      wg.Done()
    }(ch, wg)
    go func(ch chan int, wg *sync.WaitGroup) {
      for i := 0; i < 10; i++ {
        ch <- i
      }
      close(ch)
      wg.Done()
    }(ch, wg)
    wg.Wait()
  }
```

### Select Statements

- Select statements send or receive messages directly
- Select statements have no order of execution
- Select statements block until a case is processed unless a default case is added

```go
  ch1 := make(chan int)
  ch2 := make(chan string)
  select {
    case i := <-ch1:
    ...
    case ch2 <- "hello":
    ...
    default:
    ... // default case which doesn't block
  }
```

```go
  func main() {
    wg := &sync.WaitGroup{}
    m := &sync.RWMutex{}
    cacheCh := make(chan Book)
    dbCh := make(chan Book)
    for i := 0; i < 10; i++ {
      id := rnd.Intn(10) + 1
      wg.Add(2) // increment tasks to wait on by the number of goroutines running
      go func(id int, wg *sync.WaitGroup, m *sync.RWMutex, ch chan<- Book) {
        if b, ok := queryCache(id, m); ok {
          ch <- b
        }
        wg.Done() // tell the wait group the goroutine is done
      }(id, wg, m, cacheCh)
      go func(id int, wg *sync.WaitGroup, m *sync.RWMutex, ch chan<- Book) {
        if b, ok := queryDatabase(id, m); ok {
          m.Lock()
          cache[id] = b
          m.Unlock()
          ch <- b
        }
        wg.Done()
      }(id, wg, m, dbCh)
      go func(cacheCh, dbCh <-chan Book) {
        select {
          case b := <-cacheCh:
            fmt.Println("from cache")
            <-dbCh // if cache channel has a massage, drain database channel and ignore what's in database channel (database channel always runs regardless of whether something's in the cache or not and without draining, cache channel will block database channel if cache channel has a message)
          case b := <-dbCh:
            fmt.Println("from database")
        }
      }(cacheCh, dbCh)
    }
    wg.Wait() // wait until all goroutines are finished
  }
```
