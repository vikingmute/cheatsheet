##Javascript types

两种类型的type 一种叫Primitive types 基本类型 一种叫Reference types 引用类型

####Primitive types

**种类**

* Boolean  true or false
* String 'i am viking'
* Number 整数 浮点数 124 0.234
* Null
* Undefined

**声明和赋值**

```javascript
// strings
var name = "Nicholas";
var selection = "a";
// numbers
var count = 25;
var cost = 1.51;
// boolean
var found = true;
// null
var object = null;
// undefined
var flag = undefined;
var ref;    // assigned undefined automatically

```

**确定是何种类型**

>The best way to identify primitive types is with the typeof operator, which works on any variable and returns a string indicating the type of data. The typeof operator works well with strings, numbers, Booleans, and undefined.

```javascript
console.log(typeof "Nicholas");
console.log(typeof 10);
console.log(typeof 5.1);
console.log(typeof true);
console.log(typeof undefined);
// "string"
// "number"
// "number"
// "boolean"
// "undefined"
``` 
The tricky part involves null.
You wouldn’t be the first developer to be confused by the result of this line of code:

```javascript
console.log(typeof null) //'object'
```

The best way to determine if a value is null is to compare it against null directly, like this:

```javascript
console.log(value === null) // true
```
当然你引用第三方库来更好的判断类型 比如说underscore http://underscorejs.org/#isString 


**方法**

>Despite the fact that they’re primitive types, strings, numbers, and Booleans actually have methods. (The null and undefined types have no methods.) Strings, in particular, have numerous methods to help you work with them. For example:

```javascript
var name = "Nicholas";
var lowercaseName = name.toLowerCase();
var firstLetter = name.charAt(0);
var middleOfName = name.substring(2, 5);
var count = 10;
var fixedCount = count.toFixed(2);
var hexCount = count.toString(16);
var flag = true;
var stringFlag = flag.toString();
```

**基本类型包装类**
>Perhaps one of the most confusing parts of JavaScript is the concept of primitive wrapper types. There are three primitive wrapper types (String, Number, and Boolean). These special reference types exist to make working with primitive values as easy as working with objects. (It would be very confusing if you had to use a different syntax or switch to a procedural style just to get a substring of text.)

The primitive wrapper types are reference types that are automati- cally created behind the scenes whenever strings, numbers, or Booleans are read. 当基本类型调用一个方法的时候 神奇的事情发生了 有一个引用类型自动创建并调用 再调用方法完毕后 这个变量会自动销毁 看看例子

```javascript
var name = "Nicholas";
var firstChar = name.charAt(0);
console.log(firstChar);
```
This is what happens behind the scenes:

```javascript
var name = "Nicholas";
var temp = new String(name);
var firstChar = temp.charAt(0);
temp = null;
console.log(firstChar);
```


**比较是否相等**

**null vs undefined**
