

![header](https://capsule-render.vercel.app/api?type=waving&color=timeGradient&height=300&section=header&fontSize=35&text=Reading%20Dart%20Documentation&animation=fadeIn&fontAlignY=42&fontAlign=33)

### Contetents

- [01. Varibales ](#01-variables)<br/>
- [02. Operators ](#02-operators)<br/>
- [03. Metadata ](#03-metadata)<br/>
- [04. Libraries ](#03-libraries)<br/>



---
<br/>

### 01. Variables 



```Dart
String name = 'Bob';
Object name = 'Bob';
```
- Varibale stores reference
- If an object isn’t restricted to a single type, specify the Object type
<br/>

#

#### Null safety

```Dart
String? name
String? name
```

- Nullable variables default to null, so they are initialized by default. 
- Dart doesn’t set initial values to non-nullable types. 
- You can’t access properties or call methods on an expression with a nullable type.
<br/>

#

#### Default value 
```Dart
int? lineCount;
int lineCount = 0;
```
- With null safety, you must initialize the values of non-nullable variables before you use them

<br/>

~~~Dart
int lineCount;

if (weLikeToCount) {
  lineCount = countLines();
} else {
  lineCount = 0;
}

print(lineCount);
~~~
- You don’t have to initialize a local variable where it’s declared, but you do need to assign it a value before it’s used.
<br/>

#

#### Late variables 

~~~Dart
late String description;

void main() {
  description = 'Feijoada!';
  print(description);
}
~~~
~~~Dart
// This is the program's only call to readThermometer().
late String temperature = readThermometer(); // Lazily initialized.
~~~
-  The late modifier has two use cases:
1. Declaring a non-nullable variable that’s initialized after its declaration.
2. Lazily initializing a variable.
- This lazy initialization is handy in a couple of cases:
1. The variable might not be needed, and initializing it is **costly**.
2. You’re initializing an instance variable, and its initializer needs access to this.
<br/>

# 

#### Final and const

~~~Dart
final name = 'Bob'; // Without a type annotation
final String nickname = 'Bobby';
~~~
~~~Dart
name = 'Alice';
 // Error: a final variable can only be set once.
~~~
- If you never intend to change a variable, use final or const

<br/>

~~~Dart
var foo = const [];
final bar = const [];
const baz = []; // Equivalent to `const []`
~~~
~~~Dart
baz = [42];
// Error: Constant variables can't be assigned a value.
~~~
- Use const for variables that you want to be **compile-time constants**.(A compile-time constant is a value that is determined at the time of compiling the code, not at runtime. )
-  If the const variable is at the class level, mark it **static const**. 

<br/>

~~~Dart
const Object i = 3; // Where i is a const Object with an int value...
const list = [i as int]; // Use a typecast.
const map = {if (i is int) i: 'int'}; // Use is and collection if.
const set = {if (list is List<int>) ...list}; // ...and a spread.
~~~
- You can define constants that use type checks and casts (is and as), collection if, and spread operators (... and ...?):

<br/>

---

### 02. Operators

#### Operator precedence example

```Dart
// Parentheses improve readability.
if ((n % i == 0) && (d % i == 0)) ...

// Harder to read, but equivalent.
if (n % i == 0 && d % i == 0) ...
```
- In the operator table, each operator has **higher precedence** than the operators in the rows that follow it.


#

#### Arithmetic operators

```Dart
int a;
int b;

a = 0;
b = ++a; // Increment a before b gets its value.
assert(a == b); // 1 == 1

a = 0;
b = a++; // Increment a after b gets its value.
assert(a != b); // 1 != 0

a = 0;
b = --a; // Decrement a before b gets its value.
assert(a == b); // -1 == -1

a = 0;
b = a--; // Decrement a after b gets its value.
assert(a != b); // -1 != 0
```
- Dart also supports both prefix and postfix increment and decrement operators.

<br/>

```Dart
assert(5 / 2 == 2.5); // Result is a double
assert(5 ~/ 2 == 2); // Result is an int
```
- **~/**:	Divide, returning an integer result

#

#### Equality and relational operators

- If x or y is null, return true if both are null, and false if only one is null.


#


#### Type test operators

```Dart
(employee as Person).firstName = 'Bob';
```
```Dart
if (employee is Person) {
  // Type check
  employee.firstName = 'Bob';
}
```
- **as**: Typecast
- **is**:True if the object has the specified type
- **is!**: True if the object doesn’t have the specified type
  
#

#### Assignment operators

~~~Dart
a *= 3; // Assign and multiply: a = a * 3

// Assign value to b if b is null; otherwise, b stays the same
b ??= value;
~~~

#

#### Logical operators

~~~Dart
if (!done && (col == 0 || col == 3)) {
  // ...Do something...
}
~~~

#

#### Bitwise and shift operators

~~~Dart
final value = 0x22;
final bitmask = 0x0f;

assert((value << 4) == 0x220); // Shift left
assert((value >> 4) == 0x02); // Shift right
~~~
- the bitwise shift operators (<< and >>) are being used to create new values based on **shifting the bits of the original value**. 
- These operations don't change the original value itself but rather produce new values
- value << 4: This shifts the bits of value 4 places to the left, effectively multiplying value by 
2
4
2 
4
 . Since value is 0x22, the result of this operation is 0x220.
 - value >> 4: This shifts the bits of value 4 places to the right, effectively dividing value by 
2
4
2 
4
 . Since value is 0x22, the result of this operation is 0x02

#

#### Conditional expressions

~~~Dart
var visibility = isPublic ? 'public' : 'private';
String playerName(String? name) => name ?? 'Guest';
~~~
~~~Dart
// Slightly longer version uses ?: operator.
String playerName(String? name) => name != null ? name : 'Guest';

// Very long version uses if-else statement.
String playerName(String? name) {
  if (name != null) {
    return name;
  } else {
    return 'Guest';
  }
}
~~~
- If the boolean expression tests for null, consider using ??.

#

#### Cascade notation

~~~Dart
var paint = Paint()
  ..color = Colors.black
  ..strokeCap = StrokeCap.round
  ..strokeWidth = 5.0;
~~~
~~~Dart
var paint = Paint();
paint.color = Colors.black;
paint.strokeCap = StrokeCap.round;
paint.strokeWidth = 5.0;
~~~
- Cascades (.., ?..) allow you to make a sequence of operations on the same object. 

<br/>

~~~dart
querySelector('#confirm') // Get an object.
  ?..text = 'Confirm' // Use its members.
  ..classes.add('important')
  ..onClick.listen((e) => window.alert('Confirmed!'))
  ..scrollIntoView();
~~~
~~~dart
var button = querySelector('#confirm');
button?.text = 'Confirm';
button?.classes.add('important');
button?.onClick.listen((e) => window.alert('Confirmed!'));
button?.scrollIntoView();
~~~
- If the object that the cascade operates on can be null, then use a null-shorting cascade (?..) for the first operation.

<br/>

#

#### Other operators

- **?[]**: example: fooList?[1] passes the int 1 to fooList to access the element at index 1 unless fooList is null 
- **?.**: example: foo?.bar selects property bar from expression foo unless foo is null.

#

<br/>


#### 03. Metadata

~~~dart
class Television {
  /// Use [turnOn] to turn the power on instead.
  @Deprecated('Use turnOn instead')
  void activate() {
    turnOn();
  }

  /// Turns the TV's power on.
  void turnOn() {...}
  // ···
}
~~~
- A metadata annotation begins with the character **@**, followed by either a reference to a compile-time constant (such as deprecated) or a call to a constant constructor.
- Three annotations are available to all Dart code: **@Deprecated**, **@deprecated**, and **@override**. 

<br/>

~~~dart
class Todo {
  final String who;
  final String what;

  const Todo(this.who, this.what);
}
~~~
~~~dart
@Todo('Dash', 'Implement this function')
void doSomething() {
  print('Do something');
}
~~~
- You can define your own metadata annotations.
- Imagine you're a novelist working on several chapters of a book simultaneously. 
- **Sticky Note Class**: Each sticky note is like a class that defines an annotation. The color and message on the note correspond to the properties of the class.
- **Placing Sticky Notes**: When you place a sticky note on a page, it's like using an annotation in your code. The sticky note provides additional information about the page without changing its content.
- **Reading Sticky Notes**: Later, an editor or assistant may go through the manuscript and perform specific actions based on the sticky notes (e.g., proofreading pages marked with yellow).


#

<br/>

#### 04. Libraries









