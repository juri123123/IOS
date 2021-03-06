# ν΄λ‘μ (Closures)
***

π ν΄λ‘μ λ₯Ό μ μ΄ν΄ν΄μΌ μ€μννΈμ ν¨μν νλ‘κ·Έλλ° ν¨λ¬λ€μ μ€νμΌμ λͺννκ² μ΄ν΄ν  μ μμ
π ν΄λ‘μ , μ λ€λ¦­, νλ‘ν μ½, λͺ¨λλ λ±μ΄ κ²°ν©ν΄μ μ€μννΈλ κ°λ ₯ν μΈμ΄κ° λ¨.
π C, Object-Cμ λΈλ‘ λλ λ€λ₯Έ μΈμ΄μ λλ€μ μ μ¬ν¨.
π `ν΄λ‘μ (closures)` : μΌμ  κΈ°λ₯μ νλ μ½λλ₯Ό νλμ λΈλ‘μΌλ‘ λͺ¨μ κ²
π ν¨μλ ν΄λ‘μ μ ν νν, μ΄λ¦μ΄ μλ ν΄λ‘μ 

## β ν΄λ‘μ  νν(Closure Expressions)

### 1οΈβ£ μ λ ¬ λ©μλ (The Sorted Method)
```swift
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
```

```swift
//sortedμ backwardν¨μλ₯Ό μ λ¬μΈμλ‘ λ³΄λ΄κΈ°
func backward(_ s1: String, _ s2: String) -> Bool {
	return s1 > s2
}
var reversedNames = names.sorted(by: backward)
//reversedNames is equal to ["Ewa", "Daniella", "Chris", "Barry", "Alex"]
```
- `sorted(by: )` : `true`λ₯Ό λ°ννλ©΄ μ²« λ²μ§Έ μ λ¬μΈμκ° λ λ²μ§Έ μ λ¬μΈμλ³΄λ€ μμ μ΄

β `ν¨μ`λ₯Ό `λ©μλμ μ λ¬μΈμ`λ‘ λ³΄λ΄λ μΌμ `ν¨μν νλ‘κ·Έλλ° ν¨λ¬λ€μ`μμλ μμ£Ό λΉμ°ν μΌ
### 2οΈβ£ ν΄λ‘μ  νν λ¬Έλ² (Closure Expression Syntax)
```swift
{( parameters ) -> return type in 
		statements
}
```
- `general form` : μΈμλ‘ λ£μ `parameters`, μΈμ κ°μΌλ‘ μ²λ¦¬ν  λ΄μ©μ κΈ°μ νλ `statements` κ·Έλ¦¬κ³  `return type`

```swift
//backwardλμ  ν΄λ‘μ λ₯Ό μ λ¬νκΈ°
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in 
		return s1 > s2
})
```
- μμ μμ λ₯Ό ν΄λ‘μ  ννμΌλ‘ λμ²΄ν κ²
- μ½λκ° κ°κ²°ν΄μ§κ³  μ§κ΄μ 

```swift
//λ°λκ° μ§§μΌλ ν μ€λ‘ νν κ°λ₯
reversedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in return s1 > s2 } )
```
- ν΄λ‘μ μ λ°λλ `in` λ€μ μμ
- `inline closure` : ν¨μλ‘ λ°λ‘ μ μλ ννκ° μλ ν΄λ‘μ 


### 3οΈβ£ λ¬Έλ§₯μμ νμ μΆλ‘  (Inferring Type From Context)
```swift
reversedNames = names.sorted(by: { s1, s2 in return s1 > s2 } )
```
- `sorted(by:)`μ λ©μλμμ μ΄λ―Έ `(String, String) -> Bool` νμμ μΈμκ° λ€μ΄μμΌ νλμ§ μκΈ° λλ¬Έμ ν΄λ‘μ μμ μ΄ νμλ€μ μλ΅ λ  μ μμ

### 4οΈβ£ λ¨μΌ νν ν΄λ‘μ μμμ μμμ  λ°ν (Implicit Returns from Single-Express Closures)
```swift
//λ°ν ν€μλ μλ΅, λͺ¨νΈμ± μμ
reversedNames = names.sorted(by: { s1, s2 in s1 > s2 } )
```
- s1, s2λ₯Ό μΈμλ‘ λ°μ λ κ°μ λΉκ΅ν κ²°κ³Όλ₯Ό λ°ν

### 4οΈβ£ μΈμ μ΄λ¦ μΆμ½ (Shorthand Arguments Names)
```swift
reversedNames = names.sorted(by: { $0 > $1 } )
```
- `$`μ `μ«μ`μ μ‘°ν©μΌλ‘ νν
- `in` ν€μλ μ¬μ©ν  νμ μμ

### 5οΈβ£ μ°μ°μ λ©μλ (Operator Methods)
```swift
reversedNames = names.sorted(by: >)
```
- κ³μλλ μΆμ½
- `Swift`μ `String` νμ μ°μ°μμλ `String`λΌλ¦¬ λΉκ΅ν  μ μλ `λΉκ΅ μ°μ°μ(>)` λ₯Ό κ΅¬ν
- `>` μμ²΄κ° ν¨μ μ΄λ¦

## β νμ ν΄λ‘μ (Trailing Closures)
π λ§μ½ ν¨μμ λ§μ§λ§ μΈμλ‘ ν΄λ‘μ λ₯Ό λ£κ³  κ·Έ ν΄λ‘μ κ° κΈΈλ€λ©΄ `νμ ν΄λ‘μ `λ₯Ό μ¬μ©ν  μ μμ

```swift
func someFunctionThatTakesAClosure(closure: () -> Void) {
    // function body goes here
}
```
```swift
//μΈμ κ° μλ ₯ λΆλΆκ³Ό λ°ν ν λΆλΆμ μλ΅
someFunctionThatTakesAClosure(closure: {
    // closure's body goes here
})
```

```swift
//μ μ­ν¨μ νν
someFunctionThatTakesAClosure() {
    // trailing closure's body goes here
}
```
- ν¨μλ₯Ό `λκ΄νΈ ( { } )`λ‘ λ¬Άμ΄ κ·Έ μμ μ²λ¦¬ν  λ΄μ©μ μ μΌλ©΄ λ¨

π μ΄λ° μΌλ°μ μΈ μ μ­ν¨μ ννκ° μ¬μ€ ν΄λ‘μ λ₯Ό μ¬μ©νκ³  μλ κ²

```swift
reversedNames = names.sorted() { $0 > $1 }
```
- μμ μ λ ¬ μμ λ₯Ό νμ ν΄λ‘μ λ₯Ό μ¬μ©ν΄ νν

```swift
reversedNames = names.sorted { $0 > $1 }
```
- ν¨μμ λ§μ§λ§ μΈμκ° ν΄λ‘μ μ΄κ³  `νμ ν΄λ‘μ `λ₯Ό μ¬μ©νλ©΄ `κ΄νΈ()` μλ΅ κ°λ₯
```swift
//νμ ν΄λ‘μ λ₯Ό μ΄μ©ν΄ μ«μ(Int)λ₯Ό λ¬Έμ(String)λ‘ λ§€ν(Mapping)
let digitNames = [
    0: "Zero", 1: "One", 2: "Two",   3: "Three", 4: "Four",
    5: "Five", 6: "Six", 7: "Seven", 8: "Eight", 9: "Nine"
]
let numbers = [16, 58, 510]

let strings = numbers.map { (number) -> String in
    var number = number
    var output = ""
    repeat {
        output = digitNames[number % 10]! + output
        number /= 10
    } while number > 0
    return output
}
// let stringsλ νμ μΆλ‘ μ μν΄ λ¬Έμ λ°°μ΄([String])νμμ κ°μ§.
// κ²°κ³Όλ μ«μκ° λ¬Έμλ‘ λ°λ ["OneSix", "FiveEight", "FiveOneZero"]κ° λ¨.
```
- λ°°μ΄μ `map(_:)` λ©μλλ₯Ό μ΄μ©ν΄ νΉμ  κ°μ λ€λ₯Έ νΉμ  κ°μΌλ‘ λ§€ννλ ν  μ μλ ν΄λ‘μ λ₯Ό κ΅¬ν
- κ° μλ¦¬μλ₯Ό κ΅¬ν΄μ κ·Έ μλ¦¬μλ₯Ό λ¬Έμλ‘ λ³ννκ³ , 10μΌλ‘ λλ μ μλ¦¬μλ₯Ό λ°κΎΈλ©° λ¬Έμλ‘ λ³ννλ κ²μ λ°λ³΅
-  `number`κ°μ μμμΈλ°, μ΄ μμ κ°μ ν΄λ‘μ  μμμ λ³μ `var`λ‘ μ¬μ μ νκΈ° λλ¬Έμ `number`κ°μ λ³νμ΄ κ°λ₯. κΈ°λ³Έμ μΌλ‘ ν¨μμ ν΄λ‘μ μ λκ²¨μ§λ μΈμ κ°μ μμ

π¨ `digitNames[number % 10]!`μ λ€μ `λλν(!)`κ° λΆμ΄μλ κ²μ `μ¬μ (dictionary)`μ `subscript`λ `μ΅μλ`μ΄κΈ° λλ¬Έ. μ¬μ μμ νΉμ  `keyμ λν κ°`μ μμ μλ μκ³  μμ μλ μκΈ° λλ¬Έμ λΌλ¦¬μ μΌλ‘ λΉμ°.
## β κ° μΊ‘μ³(Capturing Values)
π `ν΄λ‘μ `λ νΉμ  λ¬Έλ§₯μ μμλ λ³μμ κ°μ `μΊ‘μ³`ν  μ μμ.(μ£Όλ³ λ¬Έλ°±μ ν΅ν΄ μμλ λ³μλ₯Ό νλ) λ€μλ§ν΄ `μλ³Έ κ°μ΄ μ¬λΌμ Έλ` ν΄λ‘μ Έμ `body`μμμ `κ·Έ κ°μ νμ©` κ°λ₯.
π `μ€μ²© ν¨μ(nested function)` : `Swift`μμ κ°μ `μΊ‘μ³` νλ κ°μ₯ λ¨μν νν
```swift
func makeIncrementer(forIncrement amount: Int) -> () -> Int {
    var runningTotal = 0
    func incrementer() -> Int {
        runningTotal += amount
        return runningTotal
    }
    return incrementer
}
```
- `(forIncrement amount: Int)` : μΈμ κ°
- `() -> Int` : λ°ν κ°(ν¨μ κ°μ²΄λ₯Ό λ°ν)
- λ°ν κ° => μΈμκ° μκ³  Intνμ ν΄λ‘μ λ₯Ό λ°ννλ€λ μλ―Έ

```swift
//μμμ func incrementer λ§ λ³΄μλ©΄
func incrementer() -> Int {
    runningTotal += amount
    return runningTotal
}
```
- `runningTotal`κ³Ό `amount`κ° μμ§λ§ μ΄ ν¨μλ λμκ°.
- `runningTotal`κ³Ό `amount`κ° `μΊ‘μ³λ§` λμ κ·Έλ° κ².

π¨ `μ΅μ ν` μ΄μ λ‘ `Swift`λ λ§μ½ λ μ΄μ ν΄λ‘μ μ μν΄ κ°μ΄ μ¬μ©λμ§ μμΌλ©΄ κ·Έ κ°μ `λ³΅μ¬ν΄ μ μ₯νκ±°λ μΊ‘μ³λ§ νμ§ μμ`. `Swift`λ `νΉμ  λ³μ`κ° λ μ΄μ νμνμ§ μμ λ `μ κ±°`νλ κ²κ³Ό κ΄λ ¨ν λͺ¨λ  `λ©λͺ¨λ¦¬ κ΄λ¦¬`λ₯Ό μμμ `μ²λ¦¬`.
```swift
//μ€μ²©ν¨μ μ€ν
let incrementByTen = makeIncrementer(forIncrement: 10)
```
```swift
incrementByTen()
// κ°μΌλ‘ 10μ λ°νν©λλ€.
incrementByTen()
// κ°μΌλ‘ 20μ λ°νν©λλ€.
incrementByTen()
// κ°μΌλ‘ 30μ λ°νν©λλ€.
```
- `makeIncrementer` λ΄λΆμ `incrementer` ν¨μλ₯Ό μ€ννλ λ©μλλ₯Ό λ°ν
- ν¨μκ° κ°κΈ° μ€ν λμ§λ§ μ€μ λ‘λ λ³μ `runningTotal`κ³Ό `amount`κ° `μΊ‘μ³λ§` λμ κ·Έ λ³μλ₯Ό κ³΅μ νκΈ° λλ¬Έμ κ³μ°μ΄ `λμ `

```swift
//μλ‘μ΄ ν΄λ‘μ  μμ±
let incrementBySeven = makeIncrementer(forIncrement: 7)
incrementBySeven()
// returns a value of 7
```
- λ€λ₯Έ ν΄λ‘μ μ΄κΈ° λλ¬Έμ κ³ μ μ μ μ₯μμ `runningTotal`κ³Ό `amount`λ₯Ό `μΊ‘μ³λ§` ν΄μ μ¬μ©

```swift
//μ΄μ  ν΄λ‘μ  μ€ν
incrementByTen()
// κ°μΌλ‘ 40μ λ°νν©λλ€.
```


## β ν΄λ‘μ λ μ°Έμ‘°νμ(Closures Are Reference Types)
π `incrementBySeven`κ³Ό `incrementByTen`μ μμ. ν¨μμ ν΄λ‘μ λ μ°Έμ‘° νμμ΄κΈ° λλ¬Έμ `runningTotal`λ³μλ₯Ό κ³μ μ¦κ° μν¬ μ μμ. ν¨μμ ν΄λ‘μ λ₯Ό μμλ λ³μμ ν λΉν  λ μ€μ λ‘λ μμμ λ³μμ ν΄λΉ ν¨μλ ν΄λ‘μ μ `μ°Έμ‘°(reference)`κ° ν λΉ. κ·Έλμ λ§μ½ ν ν΄λ‘μ λ₯Ό λ μμλ λ³μμ ν λΉνλ©΄ κ·Έ λ μμλ λ³μλ κ°μ ν΄λ‘μ λ₯Ό `μ°Έμ‘°`(`ν¨μ ν¬μΈν°`μ μ μ¬).

```swift
let alsoIncrementByTen = incrementByTen
alsoIncrementByTen()
// 50μ λ°νν©λλ€.
```
- μμμ μ¬μ©νλ ν΄λ‘μ λ₯Ό μμμ ν λΉνκ³  μ€νμν€λ©΄ μ¬μ©ν ν΄λ‘μ μ λ§μ§λ§ μνμμ 10μ μ¦κ°μμΌ κ²°κ³Ό κ°μΌλ‘ 50μ λ°ν

## β Escaping Closures
π ν΄λ‘μ λ₯Ό ν¨μμ νλΌλ―Έν°λ‘ λ£μ μ μλλ°, ν¨μ λ°(ν¨μκ° λλκ³ )μμ μ€νλλ ν΄λ‘μ  μλ₯Όλ€μ΄, λΉλκΈ°λ‘ μ€νλκ±°λ `completionHandler`λ‘ μ¬μ©λλ ν΄λ‘μ λ νλΌλ―Έν° νμ μμ `@escaping`μ΄λΌλ ν€μλλ₯Ό λͺμν΄μΌ ν¨.

```swift
var completionHandlers: [() -> Void] = []
func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
    completionHandlers.append(completionHandler)
}
```
- μ ν¨μμμ μΈμλ‘ μ λ¬λ `completionHandler`λ `someFunctionWithEscapingClosure` ν¨μκ° λλκ³  λμ€μ μ²λ¦¬
- λ§μ½ ν¨μκ° λλκ³  μ€νλλ ν΄λ‘μ μ `@escaping` ν€μλλ₯Ό λΆμ΄μ§ μμΌλ©΄ `μ»΄νμΌ μ μ€λ₯ λ°μ`

```swift
func someFunctionWithNonescapingClosure(closure: () -> Void) {
    closure()    // ν¨μ μμμ λλλ ν΄λ‘μ 
}

class SomeClass {
    var x = 10
    func doSomething() {
        someFunctionWithEscapingClosure { self.x = 100 } // λͺμμ μΌλ‘ selfλ₯Ό μ μ΄μ€μΌ ν©λλ€.
        someFunctionWithNonescapingClosure { x = 200 }
    }
}

let instance = SomeClass()
instance.doSomething()
print(instance.x)
// Prints "200"

completionHandlers.first?()
print(instance.x)
// Prints "100"
```
- `@escaping` λ₯Ό μ¬μ©νλ ν΄λ‘μ μμλ selfλ₯Ό λͺμμ μΌλ‘ μΈκΈν΄μΌ ν¨

## β Autoclosures
```swift
var customersInLine = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]
print(customersInLine.count)
// Prints "5"

let customerProvider = { customersInLine.remove(at: 0) }
print(customersInLine.count)
// Prints "5"

print("Now serving \(customerProvider())!")
// Prints "Now serving Chris!"
print(customersInLine.count)
// Prints "4"
```
- `let customerProvider = { customersInLine.remove(at: 0) }` μ΄ ν΄λ‘μ  μ½λλ₯Ό μ§λ¬μμλ λΆκ΅¬νκ³  `customersInLine.count` λ λ³ν¨μμ΄ 5 
- κ·Έ ν΄λ‘μ λ₯Ό μ€νμν¨ `print("Now serving \(customerProvider())!")` μ΄νμμΌ λ°°μ΄μμ κ°μ΄ νλ μ κ±°λμ΄ λ°°μ΄μ μμ κ°μκ° 4λ‘ μ€μ΄λ¬
- `μλ ν΄λ‘μ `λ μ νμ§ λΌμΈ μμλλ‘ λ°λ‘ μ€νλμ§ μκ³ , μ€μ  μ¬μ©λ  λ `μ§μ° νΈμΆ`

```swift
//μλν΄λ‘μ λ₯Ό ν¨μμ μΈμ κ°μΌλ‘ λ£λ μμ 
// customersInLine is ["Alex", "Ewa", "Barry", "Daniella"]
func serve(customer customerProvider: () -> String) {
    print("Now serving \(customerProvider())!")
}
serve(customer: { customersInLine.remove(at: 0) } )
// Prints "Now serving Alex!"
```
- `serve`ν¨μ`() -> String` : μΈμκ° μκ³ , `String`μ λ°ννλ ν΄λ‘μ λ₯Ό λ°λ ν¨μ
- `ν¨μ μ€ν` : `serve(customer: { customersInLine.remove(at: 0) } )`μ κ°μ΄ ν΄λ‘μ `{ customersInLine.remove(at: 0) }`λ₯Ό `λͺμμ `μΌλ‘ μ§μ  λ£μ μ μμ

```swift
// customersInLine is ["Ewa", "Barry", "Daniella"]
func serve(customer customerProvider: @autoclosure () -> String) {
    print("Now serving \(customerProvider())!")
}
serve(customer: customersInLine.remove(at: 0))
// Prints "Now serving Ewa!"
```
- `@autoclosure` ν€μλλ₯Ό μ΄μ©ν΄μ λ³΄λ€ κ°κ²°νκ² μ¬μ©
- `serve`ν¨μμ μΈμλ₯Ό λ°λ λΆλΆ `customerProvider: @autoclosure ()`μμ ν΄λ‘μ μ μΈμ()μμ `@autoclosure`λΌλ ν€μλ. 
- μ΄ ν€μλλ₯Ό λΆμμΌλ‘μ¨ μΈμ κ°μ `μλμΌλ‘ ν΄λ‘μ λ‘ λ³ν` 
-  `serve(customer: { customersInLine.remove(at: 0) } )` : `@autoclosure`ν€μλλ₯Ό μ¬μ©νκΈ° λλ¬Έμ `serve(customer: customersInLine.remove(at: 0))` μ΄λ κ² `{} μμ΄ μ¬μ©`. 
- `μ λ¦¬` : ν΄λ‘μ  μΈμμ `@autoclosure`λ₯Ό μ μΈνλ©΄ ν¨μκ° μ΄λ―Έ ν΄λ‘μ  μΈκ²μ μκΈ° λλ¬Έμ `λ¦¬ν΄κ° νμκ³Ό κ°μ κ°`μ λ£μ΄μ€ μ μμ

π¨ `μλν΄λ‘μ `λ₯Ό λλ¬΄ λ¨μ©νλ©΄ μ½λλ₯Ό μ΄ν΄νκΈ° μ΄λ €μ μ§ μ μμ. κ·Έλμ λ¬Έλ§₯κ³Ό ν¨μ μ΄λ¦μ΄ `autoclosureλ₯Ό μ¬μ©νκΈ°μ λΆλͺ`ν΄μΌ ν©λλ€.

```swift
//μλν΄λ‘μ @autoclosure, μ΄μ€μΌμ΄ν@escaping κ°μ΄ μ¬μ©

// customersInLine is ["Barry", "Daniella"]
var customerProviders: [() -> String] = []        //  ν΄λ‘μ λ₯Ό μ μ₯νλ λ°°μ΄μ μ μΈ
func collectCustomerProviders(_ customerProvider: @autoclosure @escaping () -> String) {
    customerProviders.append(customerProvider)
} // ν΄λ‘μ λ₯Ό μΈμλ‘ λ°μ κ·Έ ν΄λ‘μ λ₯Ό customerProviders λ°°μ΄μ μΆκ°νλ ν¨μλ₯Ό μ μΈ
collectCustomerProviders(customersInLine.remove(at: 0))    // ν΄λ‘μ λ₯Ό customerProviders λ°°μ΄μ μΆκ°
collectCustomerProviders(customersInLine.remove(at: 0))

print("Collected \(customerProviders.count) closures.")
// Prints "Collected 2 closures."        // 2κ°μ ν΄λ‘μ κ° μΆκ° λ¨
for customerProvider in customerProviders {
    print("Now serving \(customerProvider())!")    // ν΄λ‘μ λ₯Ό μ€ννλ©΄ λ°°μ΄μ 0λ²μ§Έ μμλ₯Ό μ κ±°νλ©° κ·Έ κ°μ μΆλ ₯
}
// Prints "Now serving Barry!"
// Prints "Now serving Daniella!"
```
- `collectCustomerProviders`ν¨μμ μΈμ `customerProvider`λ `@autoclosure`μ΄λ©΄μ `@escaping`λ‘ μ μΈ
- `@autoclosure`λ‘ μ μΈλκΈ° λλ¬Έμ ν¨μμ μΈμλ‘ λ¦¬ν΄κ° `String`λ§ λ§μ‘±νλ `customersInLine.remove(at: 0)`ννλ‘ ν¨μ μΈμμ λ£μ μ μμ
- `collectCustomerProviders`ν¨μκ° `μ’λ£λ νμ μ€ν`λλ ν΄λ‘μ  μ΄κΈ° λλ¬Έμ μΈμ μμ `@escaping` ν€μλ
