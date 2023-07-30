

![header](https://capsule-render.vercel.app/api?type=waving&color=timeGradient&height=300&section=header&fontSize=35&text=Reading%20Dart%20Documentation&animation=fadeIn&fontAlignY=42&fontAlign=33)

### Contetents

- [01. Varibales ](#01-Variables)<br/>
- [02. Operators ](#0-Operators)<br/>
- [03. Comments ](#03-Comments)<br/>

---
<br/>

### 01. Variables 



```
String name = 'Bob';
Object name = 'Bob';
```
- Varibale stores reference
- If an object isn’t restricted to a single type, specify the Object type
<br/><br/>

#### Null safety

```
String? name
String? name
```

- Nullable variables default to null, so they are initialized by default. 
- Dart doesn’t set initial values to non-nullable types. 
- You can’t access properties or call methods on an expression with a nullable type.
<br/><br/>

#### Default value 
```
int? lineCount;
int lineCount = 0;
```
- With null safety, you must initialize the values of non-nullable variables before you use them

<br/>

~~~
int lineCount;

if (weLikeToCount) {
  lineCount = countLines();
} else {
  lineCount = 0;
}

print(lineCount);
~~~
- You don’t have to initialize a local variable where it’s declared, but you do need to assign it a value before it’s used.
<br/><br/>

#### Late variables 

~~~


~~~


<br/><br/>
 
#### Final and const

<br/><br/>



---

### 02. Operators

### 03. Comments




