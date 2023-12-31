

![header](https://capsule-render.vercel.app/api?type=waving&color=timeGradient&height=300&section=header&fontSize=35&text=Reading%20Dart%20Documentation&animation=fadeIn&fontAlignY=42&fontAlign=33)

### Contetents

- [01. Varibales ](#01-variables)<br/>
- [02. Operators ](#02-operators)<br/>
- [03. Metadata ](#03-metadata)<br/>
- [04. Libraries ](#04-libraries)<br/>
- [05. Built-in types ](#05-built-in-types)<br/>
- [06. Records ](#06-records)<br/>
- [07. Collections](#07-collectinos)<br/>
- [08. Operators](#08-operators)<br/>


---
<br/>

### 01. Variables 



```Dart
String name = 'Bob';
Object name = 'Bob';
```
- Variables 은 주소(reference)를 저장한다
- 만약 객체가 single type이 아니라면 일단 Object 타입으로 지정하는 것이 좋다

<br/>

#

#### Null safety

```Dart
String? name // Nullable type. Can be `null` or string.
String name // Non-nullable type. Cannot be `null` but can be string.
```

- 변수를 사용하기 전에는 반드시 초기화(initialize)해야한다
- Nullable variables의 디폴트 값은 null이기 때문에 이미 초기화가 되어있다고 할 수 있다
- an expression with a nullable type 에 접근할 수 없다 -> Swift 처럼 optional(value)가 나오는 것이 아닌 그냥 접근이 안된다는 차이점
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
- Swift와 달리 직접 사용하기 전까지는 타입까지만 선언해도 괜찮다. 하지만 값을 할당하거나 사용하려면 반드시 그 전에 초기값을 넣어야한다. 
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
- To create a set that’s a compile-time constant, add const before the set literal.


<br/>


~~~dart
var gifts = {
  // Key:    Value
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings'
};

var nobleGases = {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};
~~~
- In general, a map is an object that associates keys and values. Both keys and values can be any type of object. 

<br/>

```dart
var gifts = {'first': 'partridge'};
gifts['fourth'] = 'calling birds';
assert(gifts.length == 2);
```
- Use .length to get the number of key-value pairs in the map

<br/>

```dart
final constantMap = const {
  2: 'helium',
  10: 'neon',
  18: 'argon',
};

// constantMap[2] = 'Helium'; // This line will cause an error.
```
- To create a map that’s a compile-time constant, add const before the map literal

<br/>

#

### 08. Operators

<br/>

```dart
var list = [1, 2, 3];
var list2 = [0, ...list];
assert(list2.length == 4);
```
- Dart supports the spread operator (...) and the null-aware spread operator (...?) in list, map, and set literals.

<br/>

```dart
var list2 = [0, ...?list];
assert(list2.length == 1);
```
- If the expression to the right of the spread operator might be null, you can avoid exceptions by using a null-aware spread operator (...?)

<br/>

```dart
var nav = ['Home', 'Furniture', 'Plants', if (promoActive) 'Outlet'];
```
- Dart offers collection if and collection for for use in list, map, and set literals.

<br/>

```dart
var listOfInts = [1, 2, 3];
var listOfStrings = ['#0', for (var i in listOfInts) '#$i'];
assert(listOfStrings[1] == '#1');
```
- using collection for to manipulate the items of a list before adding them to another list.

<br/>

#

### 09. Generics

<br/>

#### Why use generics?
- 제너릭을 통해 type safety를 보장할 수 있다
- 제너릭을 사용하면 코드 중복도를 낮출 수  있다

<br/>

```dart
var names = <String>[];
names.addAll(['Seth', 'Kathy', 'Lars']);
names.add(42); // Error
```
- 위 코드를 볼 때 만약 String 배열로 선언된 배열에 이외 타입이 들어가면 바로 error가 뜬다.
- 이러한 문제를 방지하기 위해 type safety를 부여하고 싶다면 generic을 사용한다

<br/>

```dart
//a string-specific version 
abstract class StringCache {
  String getByKey(String key);
  void setByKey(String key, String value);

//Later, you decide you want a number-specific version of this interface… You get the idea.
  abstract class Cache<T> {
  T getByKey(String key);
  void setByKey(String key, T value);
}
```
- 제너릭은 코드 중복도를 낮춘다. 다양한 type으로 단일 인터페이스 및 구현물을 나눌 수 있다. -> 다형성의 장점 보유
- 위 코드에서 보면 처음에는 String 타입으로 지정해서 class를 짯다가 이후에 아이디어가 떠올라 int값으로 바꿔야 하는 상황이 올 수 도 있다고 가정해보자
- 만약 전자의 예시를 사용할경우 class를 다시 int 타입으로 써야하는 엄청난 비효율적인 코딩이 탄생한다
- 이를 방지하기 위해 제너릭 코드를 사용한다 -> T는 place holder로 나중에 개발자가 정의하면 되는 부분

<br/>

#### Restricting the parameterized type

- 아무리 제너릭으로 아무 타입이나 쓰게하더라도 특정 타입으로 제한시켜서 제너릭을 사용하고 싶을 때가 있다
- 이렇 때는 extends 키워드를 사용해보자


<br/>

```dart
class Foo<T extends Object> {
  // Any type provided to Foo for T must be non-nullable.
}
```
- 이 코드는 non-nullable한 타입으로 restrict한 경우이다(디폴트값은 Object?이다)

<br/>

```dart
class Foo<T extends SomeBaseClass> {
  // Implementation goes here...
  String toString() => "Instance of 'Foo<$T>'";
}

class Extender extends SomeBaseClass {...}

var foo = Foo<Object>(); //errror

```
- SomeBaseClass로 타입을 제한시킨 Foo클래스 
- 만약 마지막코드처럼 SomeBaseClass의 범위를 넘어서는 타입이 오면 error가 뜬다

<br/>

#### Using generic methods

```dart
T first<T>(List<T> ts) {
  // Do some initial work or error checking, then...
  T tmp = ts[0];
  // Do some additional checking or processing...
  return tmp;
}
```
- `first (<T>)` 라고 작성하면 Type argument 를 다양한 곳에 작성할 수 있다
- 리턴타입에다 T를 넣을 수 있다
- argument 타입으로 T를 넣을 수 있다 (List<T>).
- local varialbe의 타입으로 넣을 수 있다 (T tmp).

<br/>

#

### 10. Typedefs


#### Typedefs 는 Swift의 Type alias와 유사하다

<br/>

``` dart
typedef IntList = List<int>;
IntList il = [1, 2, 3]
```
- 이미 있는 타입의 이름을 내가 쓰고싶은 이름으로 바꿔준다
- 위 코드의 경우 List<int> 대신 IntList가 대신 사용된 것을 확인할 수 있다

<br/>

~~~dart
typedef ListMapper<X> = Map<X, List<X>>;

Map<String, List<String>> m1 = {}; // Verbose.
ListMapper<String> m2 = {}; // Same thing but shorter and clearer.
~~~
- Typedef는 type 파라미터를 가질 수 있다
- 위의 코드를 보면 똑같은 표현을 typedef를 통해 더 간결하게 표현 -> 타입파라미터가 중첩될 때 사용하면 좋다
- 하지만 공식문서에서는 왠만하면 inline function types(기본 내재된 타입)을 사용하라고 권장하고 있다

<br/>

#

### 11. The Dart type system

#### Dart 언어가 type safe 하기 때문에 얻는 장점

- static type checking 의 장점은 버그를 런타임이 아닌 컴파일 타임에서 잡을 수 있다는 것이다

<br/>

```dart
void printInts(List<int> a) => print(a);

void main() {
  final list = [];
  list.add(1);
  list.add('2');
  printInts(list);
}
//error - The argument type 'List<dynamic>' can't be assigned to the parameter type 'List<int>'. - argument_type_not_assignable

```
- `list`는 기본적으로 `List<dynamic>`이라는 static type을 지니고 있다
- 따라서 위의 코드의 경우에는 파라미터로 `List<dynamic>`을 받아야하는데 타입추론에 의해 `List<int>`를 받음으로서 에러가 나는 것을 확인할 수 있다.

<br/>

```dart
void printInts(List<int> a) => print(a);

void main() {
  final list = <int>[];
  list.add(1);
  list.add(2);
  printInts(list);
}
```
- 위 코드처럼 `List<int>`라는 타입을 맞춰주어야한다

<br/>

#### What is soundness?

- Soundness 하다는 것은 너가 짠 코드에 invalid states가 없다는 것이다
- 다시말해 코드에 타입들이 명확하게 제시되어 있는 것이다
- Dart는 compile time 과 run time 에서 type 을 이중체크한다

<br/>

#### The benefits of soundness

- soundness 할 때 장점은 다음과 같다
1. 타입 관련 버그를 런 타임으로 넘어가기전 컴파일 타임에서 잡을 수 있다
2. 코드의 가독성을 높일 수 있다.
3. 코드가 유지보수하기 더 용이해진다 
4. Ahead-of-Time(AOT)가 빨라진다<br/>
💡AOT란?<br/>
**Ahead-of-Time(AOT)**: 고수준언어(dart)에서 저수준언어(c++, 어셈블리...)로 바꾸는데 걸리는 시간 <br/>


<br>

#### Tips for passing static analysis

&nbsp;&nbsp;&nbsp;&nbsp;<img src="pic1.png" width="400" height="200"><br/>

```dart
class Animal {
  void chase(Animal a) { ... }
  Animal get parent => ...
}

//success
class HoneyBadger extends Animal {
  @override
  void chase(Animal a) { ... }

  @override
  HoneyBadger get parent => ...
}

// error -> Animal 타입에는 Root가 없음
class HoneyBadger extends Animal {
  @override
  void chase(Animal a) { ... }
  
  @override
  Root get parent => ...
}
```
- subclass method 의 return type 은 super class 의 타입과 같거나 subtype 이여야한다!

<br/>

#### Use sound parameter types when overriding methods

- 상위클래스로부터 재정의(override)한 메서드의 타입은 상위클래스의 메서드 타입과 같거나 상위타입이여야 한다
- 다시말해 재정의할 때는 반드시! 상위클래스 메서드의 타입을 포함시켜야한다는 의미이다. 아래 예제를 보자

<br/>

```dart
//super class
class Animal {
  void chase(Animal a) { ... }
  Animal get parent => ...
}

// sub class
class HoneyBadger extends Animal {
  @override
  void chase(Object a) { ... } //상위클래스 메서드 파라미터 타입 Animal을 포괄한다

  @override
  Animal get parent => ...
}

//error 
class Mouse extends Animal {...}

class Cat extends Animal {
  @override
  void chase(Mouse x) { ... } //Animal타입보다 더 하위 타입으로 재정의할시 error
}
```
- 상위클래스 `chase()`메서드 파라미터 타입이 `Animal`이기 때문에 재정의(override)할 경우 반드시 `Animal`을 포함시켜야 한다.  

<br/>

#### Don’t use a dynamic list as a typed list

~~~dart
class Cat extends Animal { ... }

class Dog extends Animal { ... }

void main() {
  List<Cat> foo = <dynamic>[Dog()]; // Error
  List<dynamic> bar = <dynamic>[Dog(), Cat()]; // OK
}
~~~

- 배열(list)의 타입으로 다이나믹은 쓰지말 것!

<br/>

#### Type inference

```Dart
Map<String, dynamic> arguments = {'argA': 'hello', 'argB': 42};

var arguments = {'argA': 'hello', 'argB': 42}; // Map<String, Object>
```
- argument의 타입은 사실상 `Map<String, dynamic>`이라고 볼 수 있다.
- 단지 두 번째 코드를 작성해도 타입추론에 의해 첫번째 코드 타입으로 자동적으로 인식한다

<br/>

#### Substituting Types

&nbsp;&nbsp;&nbsp;&nbsp;<img src="pic1.png" width="400" height="200"><br/>

~~~dart
Animal c = Cat();

MaineCoon c = Cat(); //error
Cat c = MaineCoon(); //success
~~~

- 하위 타입에 상위 타입을 할당하면 에러가 뜬다. 상위 타입에는 하위 타입에 속하지 않는 메서드나 속성이 있을 수 있기 때문에 type safety가 지켜지지 않기 때문이다
- 반면 상위타입에 하위타입을 할당하는 것은 가능하다. 100%의 확률로 상위 타입은 하위타입의 메서드나 속성을 가질 수 있고 type safety가 지켜지기 때문이다

<br/>

#### Generic type assignment

&nbsp;&nbsp;&nbsp;&nbsp;<img src="pic/1.png" width="400" height="200"><br/>


~~~dart
//success
List<MaineCoon> myMaineCoons = ...
List<Cat> myCats = myMaineCoons;

//error
List<Animal> myAnimals = ...
List<Cat> myCats = myAnimals;
~~~


- 위와 같은 타입 계층구조에 따른 type safety 보장 방식은 제너릭 타입에도 동일하게 적용된다.
- 하위타입인 Cat은 상위타입인 Animal을 할당받을 수 없다

<br/>

~~~dart
List<Animal> myAnimals = ...
List<Cat> myCats = myAnimals as List<Cat>;
~~~~

- 나는 곧죽어도 할당해야한다 싶으면 as를 통해 다운캐스팅을 해야한다

<br/>

```dart
class Animal {
    void chase(Animal a){}
    Animal get parent => ...
}
```
- get메서드에서도 똑같이 적용된다
- 위의 코드의 경우 parent는 `chase(Animal)`를 가지고 읽기(read)를 하는데 이때 당연히 parent의 클래스가 더 상위여야 한다.

<br/>

#

### 12. Patterns

#### What patterns do

~~~dart
//Matching
switch (number) {
  // Constant pattern matches if 1 == number.
  case 1:
    print('one');
}
~~~~

- 패턴의 예로는 할당연산자와 논리연산자 등이 있다. 즉 어떤 값이 특정 모양인지 비교해서 알아보는 체킹하는 행위와 같다.
- Pattern은 value값을 context에 맞게 매칭(Match)하거나 분해(Destruct)하는 기능을 수행한다
- Matching은 value가 패턴과 매칭하는지 알아보는 구문이다

<br/>

```dart
const a = 'a';
const b = 'b';
switch (obj) {
  // List pattern [a, b] matches obj first if obj is a list with two fields,
  // then if its fields match the constant subpatterns 'a' and 'b'.
  case [a, b]:
    print('$a, $b');
}
```

- 많은 패턴이 서브패턴을 사용한다 위 예제와 같이 먼저 Switch를 통해 case를 분류하고 또 case 내에서 a,b를 매칭시킨다.
- 이를 outer and innter 패턴이라 부른다

<br/>

#### Destructuring

```dart
var numList = [1, 2, 3];
// List pattern [a, b, c] destructures the three elements from numList...
var [a, b, c] = numList;
// ...and assigns them to new variables.
print(a + b + c);
```

- 만약 객체의 패턴이 매칭한다면 객체의 데이터에 접근이 가능하다, 즉 객체의 데이터를 뽑아낼 수 있다.
- 이렇게 패턴이 매칭된 객체의 데이터를 뽑아쓰는 것을 destruct한다고 부른다.

<br/>

#### Variable declaration

```dart
// Declares new variables a, b, and c.
var (a, [b, c]) = ('str', [1, 2]);
```

- 패턴 매칭은 지역변수 선언에서도 위와같이 활용할 수 있다.
- 패턴이 "Matching" 할 때 "Destruct" 할 수 있다

<br/>

#### Switch statements and expressions

```dart
switch (obj) {
  // Matches if 1 == obj.
  case 1:
    print('one');

  // Matches if the value of obj is between the constant values of 'first' and 'last'.
  case >= first && <= last:
    print('in range');

  // Matches if obj is a record with two fields, then assigns the fields to 'a' and 'b'.
  case (var a, var b):
    print('a = $a, b = $b');

  default:
}
```

- 결국 패턴은 조건이다
- 이때 case로 나타내는 조건을 **switch statment**라 부르고 조건에 매칭되 destruct하는 부분은 **expresion**이라 부른다
- 패턴은 refutable(거절가능)하다. 만약 case가 매칭되지 않는다면 다음 케이스로 넘어간다

<br/>

```dart
Map<String, int> hist = {
  'a': 23,
  'b': 100,
};

for (var MapEntry(key: key, value: count) in hist.entries) {
  print('$key occurred $count times');
}
```

- 패턴을 이용해 for-in루프를 이용할 수 있다.
- 예제와 같이 `var MapEntry(key: key, value: count)`와 `Map<String, int> hist`가 매칭됨에 따라 값을 하나씩 꺼내어 for-in루프를 돌릴 수 있다.

<br/>

#### Destructuring multiple returns

```dart
var info = userInfo(json);
var name = info.$1;
var age = info.$2;
```
- `Records` multiple value 들을 aggregate 하기도 하지만 returning 하기도 한다.

<br/>

#### Destructuring class instances

```dart
final Foo myFoo = Foo(one: 'one', two: 2);
var Foo(:one, :two) = myFoo;
print('one $one, two $two');
```
- 매칭만 된다면 위 예제와 같이 name type을 destruct하여 사용할 수 있다

<br/>

#### Validating incoming JSON

~~~Dart
var json = {
  'user': ['Lily', 13]
};
var {'user': [name, age]} = json;
~~~

- Map과 list는 패턴을 적용하기에 아주 좋은 짝꿍이다.
- 특히 key-value 쌍으로 되어있는 JSON data를 destruct 할 때 자주 이용한다


<br/>

```dart
if (json is Map<String, Object?> &&
    json.length == 1 &&
    json.containsKey('user')) {
  var user = json['user'];
  if (user is List<Object> &&
      user.length == 2 &&
      user[0] is String &&
      user[1] is int) {
    var name = user[0] as String;
    var age = user[1] as int;
    print('User $name is $age years old.');
  }
}
```
- 패턴을 적용하지 않을시 코드가 이렇게 verbose 해진다.

<br/>

```dart
if (json case {'user': [String name, int age]}) {
  print('User $name is $age years old.');
}
```
- case 패턴을 통해 위와 같은 예제를 크게 축약시킬 수 있다

<br/>

#

### 12. Pattern types

#### Logical-or

```dart
var isPrimary = switch (color) {
  Color.red || Color.yellow || Color.blue => true,
  _ => false
};
```
- or 패턴은 ||로 표현하며 왼쪽에서부터 오른쪽으로 매칭해본다. 만약 false가 한번 나면 오른쪽은 더이상 보지않고 바로 false를 뱉어버린다.
- 여기서도 예외없이 비교대상들의 타입이 매칭되어야한다

<br/>

#### Logical-and

```dart
switch ((1, 2)) {
  // Error, both subpatterns attempt to bind 'b'.
  case (var a, var b) && (var b, var c): // ...
}
```
- and는 &&로 표현한다 or 패턴과 마찬가지로 false 가 나오면 오른쪽은 더이상 안보고 바로 false를 리턴한다

<br/>

#### Relational


```dart
String asciiCharType(int char) {
  const space = 32;
  const zero = 48;
  const nine = 57;

  return switch (char) {
    < space => 'control',
    == space => 'space',
    > space && < zero => 'punctuation',
    >= zero && <= nine => 'digit',
    _ => ''
  };
}
```
- relational 패턴은 위와같이 and 패턴과 조합하면 유용하다

<br/>

#### Cast


```dart
(num, Object) record = (1, 's');
var (i as int, s as String) = record;
```
- 패턴에 match하기전에 cast패턴은 먼저 타입캐스팅을 하는 패턴이다
- 예제를 보면 먼저 record의 값을 타입캐스트하고 매칭하는 것을 확인할 수 있다

<br/>

#### Null-check

```dart

```


<br/>












