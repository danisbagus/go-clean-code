# go-clean-code
This document is about how to write go clean code by transform bad code into good code.

# Introduce

## Clean Code
- Code that is easy to understand and easy to change.
- Have a good format and structure.
- The goal is that the code written can be more easily read and understood by other programmers.
- Help collaboration between programmers in working on a project.

## Main Rules:
- Readable
- Independent
- Reusable
- Testable
- Low Complexity
- No Duplication

## Goal
- Avoid the dirty (smells/sphagetti) code to reduce or eliminate introdution of bugs to applications.

## Tips:
- Keep it simple 
- Understand Your Code
- Comments Are Your New Best Friends
- Don’t Repeat Yourself (DRY)
- Indent Your Code
- Naming Convention
- Explore
- Use Your Brain
- Test Runs

# How to Write Clean Code

## Meaningful Names

### Use Intention-Revealing Names

Bad:
```go
var d []int

func getThem(theList []int) []int {
	list := []int{}

	for _, x := range list {
		if x%2 == 0 {
			list = append(list, x)
		}
	}

	return list
}
```

Good:
```go
var numbers []int

func getEventNumber(numbers []int) []int {
	eventNumbers := []int{}

	for _, number := range numbers {
		if number%2 == 0 {
			eventNumbers = append(eventNumbers, number)
		}
	}

	return eventNumbers
}
```

### Avoid Disinformation
#### Avoid words whose entrenched meaning vary from our intended meaning.

Bad:
```go
var accountList []Account
```

Good:
```go
var accounts []Account
```

#### Beware of using names which vary in small ways.

```go
var XYZControllerForEfficientHandlingOfStrings string
var XYZControllerForEfficientStorageOfStrings string
```

### Make Meaningful Distinctions

Bad:
```go
// Change one name in an arbitrary way with misspelling name. because the name class was used for something else.
type klass struct{}

// Noise words. Info and Data are indistinct noise words like a, an, and the
var productData Product
var productInfo Product

// The arguments are noninformative, a1 and a2 doesn't provide clues to the author intention
func copyMap(a1 map[string]string, a2 map[string]string) {
	for key, value := range a1 {
		a2[key] = value
	}
}
```

Good:
```go
func copyMap(source map[string]string, destination map[string]string) {
	for key, value := range source {
		destination[key] = value
	}
}
```

### Use Pronounceable Names
Bad:
```go
type DtaRcrd struct {
	createdmdhms time.Time
	pszqint      string
}
```

Good:
```go
type Product struct {
	createdTimestamp   time.Time
	categoryId         string
}
```

### Use Searchable Names
- If a variable or constant might be seen or used in multiple places in a body of code, it is imperative to give it a search-friendly name.

Bad:
```go
	for j := 0; j < 34; j++ {
		s += (t[j] * 4) / 5
	}
```

Good:
```go
    var realDaysPerIdealDay int = 4
	const WORK_DAYS_PER_WEEK int = 5
	var sum int = 0

	for int = 0; j < NUMBER_OF_TASKS; j++ {
		var realTaskDays int = taskEstimate[j] * realDaysPerIdealDay
		var realTaskWeeks int = (realdays / WORK_DAYS_PER_WEEK)
		sum += realTaskWeeks
	}
```

### Class Names
- Classes and objects should have noun or noun phrase names like `Customer`, `WikiPage`, `Account`, and `AddressParser`.
- Avoid words like `Manager`,`Processor`, `Data`, or `Info` in the name of a class. A class name should not be a verb.

### Method Names
- Methods should have verb or verb phrase names like `postPayment`, `deletePage` or `save`.

### Don't Be Cute
Cute name:
```go
func holyHandGranade(){}

func whack(){}

func eatMyShorts(){}
```

Clean name:
```go
func deleteItems(){}

func kill(){}

func abort(){}
```

### Pick one word per concept
- Pick one word for one abstract concept and stick with it. 
- It’s confusing to have `fetch`, `retrieve`, and `get` as equivalent methods of different classes.

### Don’t Pun
- Avoid using the same word for two purposes
- Example: in a class use `add` for create a new value by adding or concatenating two existing values and in another class use `add` for put a simple parameter in a collection, it's a better options use a name like `insert` or `append` instead.

### Use Solution Domain Names
- Remember that the people who read your code will be programmers. 
- So go ahead and use computer science (CS) terms, algorithm names, pattern names, math terms, and so forth.
- The name `AccountVisitor` means a great deal to a programmer who is familiar with the VISITOR patern.

### Use Problem Domain Names
- When there is no “programmer-eese” for what you’re doing, use the name from the problem domain. 
- At least the programmer who maintains your code can ask a domain expert what it means.

### Add Meaningful context
- Varibles `firstName`, `lastName`, `street`, `city`, `state`, `zizcode` is form of address. 
- Yu could add context using prefixes: `addrState`, `addrFirstName`, `addrLastname` at least readers will understand that the variable is part of a large structure. 
- A better solution is to create a class named `Address`.

### Don’t Add Gratuitous Context
- In an imaginary application called `Gas Station Deluxe`, it is a bad idea to prefix every class with `GSD`.
- class named `GSDAccountAddress`, ten of 17 characters are redundant or irrelevant.
- Shorter names are generally better than longer ones, so long as they are clear.
- `accountAddress` and `customerAddress` are fine names for instances but could be poor names for classes. `Address` is fine name for a class.