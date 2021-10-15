# Go

- [Go](#go)
  - [Compiled or Interpreted?](#compiled-or-interpreted)
  - [Is Go Object Oriented?](#is-go-object-oriented)
  - [What Go Doesn't Support](#what-go-doesnt-support)

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
  - Custom structs (data structures) can have member fields

## What Go Doesn't Support

- Type inheritance (no classes)
- Method or operator overloading
- Structured exception handling
  - No try catch keywords
  - Error objects are returned by functions that generate those errors which conditional logic can be used to examine
- Implicit numeric conversions