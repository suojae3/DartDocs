

![header](https://capsule-render.vercel.app/api?type=waving&color=timeGradient&height=300&section=header&fontSize=35&text=Reading%20Dart%20Documentation&animation=fadeIn&fontAlignY=42&fontAlign=33)

### Contetents

- [01. Varibales ](#01-variables)<br/>
- [02. Operators ](#02-operators)<br/>
- [03. Metadata ](#03-metadata)<br/>
- [04. Libraries ](#04-libraries)<br/>
- [05. Built-in types ](#05-built-in-types)<br/>
- [06. Records ](#06-records)<br/>
- [07. Collections](#07-collectinos)<br/>


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

### 04. Libraries

<br/>

#### Specifying a library prefix

```dart
import 'package:lib1/lib1.dart';
import 'package:lib2/lib2.dart' as lib2;

// Uses Element from lib1.
Element element1 = Element();

// Uses Element from lib2.
lib2.Element element2 = lib2.Element();
```
- If you import two libraries that have conflicting identifiers, then you can specify a prefix for one or both libraries.

<br/>


```dart
// Import only foo.
import 'package:lib1/lib1.dart' show foo;

// Import all names EXCEPT foo.
import 'package:lib2/lib2.dart' hide foo;
````
- If you want to use only part of a library, you can selectively import the library.

<br/>

```dart
//To lazily load a library, you must first import it using deferred as.
import 'package:greetings/hello.dart' deferred as hello;

//When you need the library, invoke loadLibrary() using the library’s identifier.
Future<void> greet() async {
  await hello.loadLibrary();
  hello.printGreeting();
}
```
- Dart implicitly inserts loadLibrary() into the namespace that you define using deferred as namespace. The loadLibrary() function returns a Future.
- Laily loading a library's advantages are
  1. To reduce a web app’s initial startup time.
  2. To perform A/B testing—trying out alternative implementations of an algorithm, for example.
  3. To load rarely used functionality, such as optional screens and dialogs.

#

<br/>

### 05. Built-in types

<br/>

- **every variable in Dart refers to an object** — an instance of a class—you can usually use constructors to initialize variables.

~~~dart
// String -> int
var one = int.parse('1');
assert(one == 1);

// String -> double
var onePointOne = double.parse('1.1');
assert(onePointOne == 1.1);

// int -> String
String oneAsString = 1.toString();
assert(oneAsString == '1');

// double -> String
String piAsString = 3.14159.toStringAsFixed(2);
assert(piAsString == '3.14');
~~~

- turn a string into a number, or vice versa:

<br/>

```dart
assert((3 << 1) == 6); // 0011 << 1 == 0110
assert((3 | 4) == 7); // 0011 | 0100 == 0111
assert((3 & 4) == 0); // 0011 & 0100 == 0000
```
- The int type specifies the traditional bitwise shift (<<, >>, >>>), complement (~), AND (&), OR (|), and XOR (^) operators, which are useful for manipulating and masking flags in bit fields.

<br/>

```dart
var s = 'string interpolation';

assert('Dart has $s, which is very handy.' ==
    'Dart has string interpolation, '
        'which is very handy.');
```
- You can put the value of an expression inside a string by using ${expression}.

<br/>

#

### 06. Records

<br/>

- Records are an anonymous, immutable, aggregate type.
- Unlike other collection types, records are fixed-sized, heterogeneous, and typed.

```dart
var record = ('first', a: 2, b: true, 'last');

// Record type annotation in a variable declaration:
({int a, bool b}) record;

// Initialize it with a record expression:
record = (a: 123, b: true);
```

<br/>

```dart
(num, Object) pair = (42, 'a');

var first = pair.$1; // Static type `num`, runtime type `int`.
var second = pair.$2; // Static type `Object`, runtime type `String`.
```
- There is no type declaration for individual record types.
- The type system is aware of each field’s type wherever it is accessed from the record

<br/>


```dart
({int x, int y, int z}) point = (x: 1, y: 2, z: 3);
({int r, int g, int b}) color = (r: 1, g: 2, b: 3);

print(point == color); // Prints 'false'. Lint: Equals on unrelated types.
```
- Two records are equal if they have the same shape (set of fields), and their corresponding fields have the same values. 
- Since named field order is not part of a record’s shape, the order of named fields does not affect equality.

<br/>

```dart
// Returns multiple values in a record:
(String, int) userInfo(Map<String, dynamic> json) {
  return (json['name'] as String, json['age'] as int);
}

final json = <String, dynamic>{
  'name': 'Dash',
  'age': 10,
  'color': 'blue',
};

// Destructures using a record pattern:
var (name, age) = userInfo(json);

/* Equivalent to:
  var info = userInfo(json);
  var name = info.$1;
  var age  = info.$2;
*/
```
- Records allow functions to return multiple values bundled together

<br/>

#

### 07. Collections

<br/>

- Dart has built-in support for **list, set, and map** collections.

<br/>

```dart
var list = [1, 2, 3];
assert(list.length == 3);
assert(list[1] == 2);

list[1] = 1;
assert(list[1] == 1);
```

- Perhaps the most common collection in nearly every programming language is the array, or ordered group of objects.
- Lists use zero-based indexing, where 0 is the index of the first value and list.length - 1 is the index of the last value.

<br/>

```dart
var halogens = {'fluorine', 'chlorine', 'bromine', 'iodine', 'astatine'};
```
- A set in Dart is an unordered collection of unique items

<br/>

``` Dart
var names = <String>{};
// Set<String> names = {}; // This works, too.
// var names = {}; // Creates a map, not a set.
```
- The syntax for map literals is similar to that for set literals. Because map literals came first, {} defaults to the Map type.
- If you forget the type annotation on {} or the variable it’s assigned to, then Dart creates an object of type **Map<dynamic, dynamic>**.

<br/>

```dart
final constantSet = const {
  'fluorine',
  'chlorine',
  'bromine',
  'iodine',
  'astatine',
};
// constantSet.add('helium'); // This line will cause an error.
```
- To create a set that’s a compile-time constant, add const before the set literal:

<br/>





