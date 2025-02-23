---
title: 运算符
layout: page
category: grammar
date: 2013-02-04
modifiedOn: 2014-02-04
---

运算符是用来处理数据的基本方法。JavaScript与其他编程语言一样，提供了多种运算符。

## 算术运算符

JavaScript提供9个算术运算符。

- **加法运算符**（Addition）：`x + y`
- **减法运算符**（Subtraction）： `x - y`
- **乘法运算符**（Multiplication）： `x * y`
- **除法运算符**（Division）：`x / y`
- **余数运算符**（Remainder）：`x % y`
- **自增运算符**（Increment）：`++x` 或者 `x++`
- **自减运算符**（Decrement）：`--x` 或者 `x--`
- **求负运算符**（Negate）：`-x`
- **数值运算符**（Convert to number）： `+x`

减法、乘法、除法运算法比较单纯，就是执行相应的数学运算。下面介绍其他几个算术运算符。

### 加法运算符

加法运算符（`+`）需要注意的地方是，它除了用于数值的相加，还能用于字符串的连接。

```javascript
1 + 1 // 2
'1' + '1' // "11"
'1.1' + '1.1' // "1.11.1"
```

上面代码中，如果两个运算子都是数值，加号运算符就执行数值的加法运算；如果两个运算子都是字符串，加号运算符就执行字符串的连接运算，变成字符串连接运算符。这种由于参数不同，而改变自身行为的现象，叫做“重载”（overload）。

如果两个运算子之中，一个是字符串，另一个是数值，加法运算符执行字符串连接运算。

```javascript
1 + '1' // "11"
```

上面代码表示，两个运算子之中有一个是字符串，另一个运算子就会被自动转为字符串。

```javascript
'3' + 4 + 5 // "345"
3 + 4 + '5' // "75"
```

上面代码中，由于加法运算符遇到字符串，会发生重载，导致运算结果的不同。

由于这个特性，下面的写法有时用于将一个值转为字符串。

```javascript
x + ''
```

上面代码表示，一个值加上空字符串，会使得该值转为字符串形式。

布尔值和复合类型的值，也可以使用加法运算符，但是会导致数据类型的自动转换，关于这方面的详细讨论，参见《数据类型转换》一节。

加法运算符以外的其他算术运算符，都不会发生重载。它们的规则是：所有运算子一律转为数值，再进行相应的数学运算。

```javascript
1 - '1' // 0
+'3' // 3
-true // -1
```

上面代码表示，减法运算符将字符串“1”自动转为数值1，数值运算符（+）将字符串“3”转为数值3，求负运算符（-）将布尔值true转为-1。

由于加法运算符与其他算术运算符的这种差异，会导致一些意想不到的结果，计算时要小心。

```javascript
var now = new Date();
typeof (now + 1) // "string"
typeof (now - 1) // "number"
```

上面代码中，`now`是一个Date对象的实例。加法运算时，`now`转为字符串，加一个数字，得到还是字符串；减法运算时，now转为数值，减一个数字，得到的是数字。

### 余数运算符

余数运算符返回前一个运算子被后一个运算子除，所得的余数。

{% highlight javascript %}

12 % 5 // 2

{% endhighlight %}

需要注意的是，运算结果的正负号由第一个运算子的正负号决定。

{% highlight javascript %}

-1 % 2 // -1
1 % -2 // 1

{% endhighlight %}

为了得到正确的负数的余数值，需要先使用绝对值函数。

{% highlight javascript %}

// 错误的写法
function isOdd(n) {
    return n % 2 === 1;
}
isOdd(-5) // false
isOdd(-4) // false

// 正确的写法
function isOdd(n) {
    return Math.abs(n % 2) === 1;
}
isOdd(-5) // true
isOdd(-4) // false

{% endhighlight %}

余数运算符还可以用于浮点数的运算。但是，由于浮点数不是精确的值，无法得到完全准确的结果。

{% highlight javascript %}

6.5 % 2.1 
// 0.19999999999999973

{% endhighlight %}

### 自增和自减运算符

自增和自减运算符，是一元运算符，只需要一个运算子。它们的作用是将运算子首先转为数值，然后加上1或者减去1。

{% highlight javascript %}

var x = "1";
++x // 2

{% endhighlight %}

上面代码的x是一个字符串，使用递增运算符后，x首先被转为数值1，然后进行递增，返回2。

它们有一个需要注意的地方，就是放在变量之后，表示先返回变量操作前的值，再进行递增/递减操作；放在变量之前，表示先进行递增/递减操作，再返回变量操作后的值。

{% highlight javascript %}

var x1 = 1;
var x2 = 1;

x1++ // 1
++x2 // 2

{% endhighlight %}

上面代码中，x1是先返回后递增，所以得到1；x2是先递增后返回，所以得到2。

### 数值运算符

数值运算符（+）同样使用加号，但是加法运算符是二元运算符（需要两个操作数），它是一元运算符（只需要一个操作数）。

它的重要作用在于可以将任何值转为数值（与Number函数的作用相同）。

{% highlight javascript %}

+true // 1
+[] // 0
+{} // NaN

{% endhighlight %}

上面代码表示，非数值类型的值经过数值运算符以后，都变成了数值（包括最后一个NaN）。具体的类型转换规则，参见《数据类型转换》一节。

求负运算符（-），也同样具有将一个值转为数值的功能，所以下面的写法等同于求值运算符。

{% highlight javascript %}

-(-x)

{% endhighlight %}

上面代码的圆括号不可少，否则会变成递减运算符。

## 赋值运算符

赋值运算符（Assignment Operators）用于给变量赋值。

最常见的赋值运算符，当然就是等号（=），表达式`x=y`表示将y赋值给x。除此之外，JavaScript还提供其他11个赋值运算符。

{% highlight javascript %}

x += y // 等同于 x = x + y
x -= y // 等同于 x = x - y
x *= y // 等同于 x = x * y
x /= y // 等同于 x = x / y
x %= y // 等同于 x = x % y
x >>= y // 等同于 x = x >> y
x <<= y // 等同于 x = x << y
x >>>= y // 等同于 x = x >>> y
x &= y // 等同于 x = x & y
x |= y // 等同于 x = x | y
x ^= y // 等同于 x = x ^ y

{% endhighlight %}

## 比较运算符

比较运算符比较两个值，然后返回一个布尔值，表示是否满足比较条件。JavaScript提供了8个比较运算符。

- **==** 相等
- **===** 严格相等
- **!=** 不相等
- **!==** 严格不相等
- **<** 小于
- **<=** 小于或等于
- **\>** 大于
- **\>=** 大于或等于

其中，比较两个值是否相等的运算符有两个：一个是相等运算符（==），另一个是严格相等运算符（===）。

相等运算符（==）比较两个“值”是否相等，严格相等运算符（===）比较它们是否为“同一个值”。两者的一个重要区别是，如果两个值不是同一类型，严格相等运算符（===）直接返回false，而相等运算符（==）会将它们转化成同一个类型，再用严格相等运算符进行比较。

我们先看严格相等运算符。

### 严格相等运算符

严格相等运算符的运算规则如下：

**（1）不同类型的值**

如果两个值的类型不同，直接返回false。

{% highlight javascript %}

1 === "1" // false

true === "true" // false

{% endhighlight %}

上面代码比较数值的1与字符串的“1”、布尔值的true与字符串“true”，因为类型不同，结果都是false。

**（2）同一类的原始类型值**

同一类型的原始类型的值（数值、字符串、布尔值）比较时，值相同就返回true，值不同就返回false。

{% highlight javascript %}

1 === 0x1 // true

{% endhighlight %}

上面代码比较十进制的1与十六进制的1，因为类型和值都相同，返回true。

需要注意的是，NaN与任何值都不相等（包括自身）。另外，正0等于负0。

{% highlight javascript %}

NaN === NaN  // false

+0 === -0 // true

{% endhighlight %}

**（3）同一类的复合类型值**

两个复合类型（对象、数组、函数）的数据比较时，不是比较它们的值是否相等，而是比较它们是否指向同一个对象。

{% highlight javascript %}

({}) === {} // false

[] === [] // false

(function (){}) === function (){} // false

{% endhighlight %}

上面代码分别比较两个空对象、两个空数组、两个空函数，结果都是不相等。原因是对于复合类型的值，严格相等运算比较的是它们的内存地址是否一样，而上面代码中空对象、空数组、空函数的值，都存放在不同的内存地址，结果当然是false。另外，之所以要把第一个空对象放在括号内，是为了避免JavaScript引擎把这一行解释成代码块，从而报错；把第一个空函数放在括号内，是为了避免这一行被解释成函数的定义。

如果两个变量指向同一个复合类型的数据，则它们相等。

{% highlight javascript %}

var v1 = {};
var v2 = v1;

v1 === v2 // true

{% endhighlight %}

**（4）undefined和null**

undefined 和 null 与自身严格相等。

{% highlight javascript %}

undefined === undefined // true

null === null // true

{% endhighlight %}

由于变量声明后默认值是undefined，因此两个只声明未赋值的变量是相等的。

{% highlight javascript %}

var v1;
var v2;

v1 === v2 // true

{% endhighlight %}

**（5）严格不相等运算符**

严格相等运算符有一个对应的“严格不相等运算符”（!==），两者的运算结果正好相反。

{% highlight javascript %}

1 !== "1" // true

{% endhighlight %}

### 相等运算符

相等运算符在比较相同类型的数据时，与严格相等运算符完全一样。

在比较不同类型的数据时，相等运算符会先将数据进行类型转换，然后再用严格相等运算符比较。类型转换规则如下：

**（1）原始类型的值**

原始类型的数据会转换成数值类型再进行比较。

{% highlight javascript %}

1 == true // true
0 == false // true

"true" == true // false

'' == 0 // true

'' == false  // true
'1' == true  // true

"2" == true // false
2 == true // false
2 == false // false

'\n  123  \t' == 123 // true
// 因为字符串转为数字时，省略前置和后置的空格

{% endhighlight %}

上面代码将字符串和布尔值都转为数值，然后再进行比较。字符串与布尔值的类型转换规则，参见《数据类型转换》一节。

**（2）对象与原始类型值比较**

对象（这里指广义的对象，包括数值和函数）与原始类型的值比较时，对象转化成原始类型的值，再进行比较。

{% highlight javascript %}

[1] == 1 // true
[1] == "1" // true
[1] == true // true

{% endhighlight %}

上面代码将只含有数值1的数组与原始类型的值进行比较，数组[1]会被自动转换成数值1，因此结果都是true。数组的类型转换规则，参见《数据类型转换》一节。

**（3）undefined和null**

undefined和null与其他类型的值比较时，结果都为false，它们互相比较时结果为true。

{% highlight javascript %}

false == null // false
0 == null // false

undefined == null // true

{% endhighlight %}

**（4）相等运算符的缺点**

相等运算符隐藏的类型转换，会带来一些违反直觉的结果。

{% highlight javascript %}

'' == '0'           // false
0 == ''             // true
0 == '0'            // true

false == 'false'    // false
false == '0'        // true

false == undefined  // false
false == null       // false
null == undefined   // true

' \t\r\n ' == 0     // true

{% endhighlight %}

上面这些表达式都很容易出错，因此不要使用相等运算符（==），最好只使用严格相等运算符（===）。

**（5）不相等运算符**

相等运算符有一个对应的“不相等运算符”（!=），两者的运算结果正好相反。

{% highlight javascript %}

1 != "1" // false

{% endhighlight %}

## 布尔运算符

布尔运算符用于将表达式转为布尔值。

### 取反运算符（!）

取反运算符形式上是一个感叹号，用于将布尔值变为相反值，即true变成false，false变成true。

{% highlight javascript %}

!true // false
!false // true

{% endhighlight %}

对于非布尔值的数据，取反运算符会自动将其转为布尔值。规则是，以下六个值取反后为true，其他值取反后都为false。

- undefined
- null
- false
- 0（包括+0和-0）
- NaN
- 空字符串（""）

这意味着，取反运算符有转换数据类型的作用。

{% highlight javascript %}

!undefined // true
!null // true
!0 // true
!NaN // true
!"" // true

!54 // false
!'hello' // false
![] // false
!{} // false

{% endhighlight %}

上面代码中，不管什么类型的值，经过取反运算后，都变成了布尔值。

如果对一个值连续做两次取反运算，等于将其转为对应的布尔值，与Boolean函数的作用相同。这是一种常用的类型转换的写法。

{% highlight javascript %}

!!x

// 等同于

Boolean(x)

{% endhighlight %}

上面代码中，不管x是什么类型的值，经过两次取反运算后，变成了与Boolean函数结果相同的布尔值。所以，两次取反就是将一个值转为布尔值的简便写法。

取反运算符的这种将任意数据自动转为布尔值的功能，对下面三种布尔运算符（且运算符、或运算符、三元条件运算符）都成立。

### 且运算符（&&）

且运算符的运算规则是：如果第一个运算子的布尔值为true，则返回第二个运算子的值（注意是值，不是布尔值）；如果第一个运算子的布尔值为false，则直接返回第一个运算子的值，且不再对第二个运算子求值。

{% highlight javascript %}

"t" && "" // ""
"t" && "f" // "f"
"t" && (1+2) // 3
"" && "f" // ""
"" && "" // ""

var x = 1;
(1-1) && (x+=1) // 0
x // 1

{% endhighlight %}

上面代码的最后一部分表示，由于且运算符的第一个运算子的布尔值为false，则直接返回它的值0，而不再对第二个运算子求值，所以变量x的值没变。

这种跳过第二个运算子的机制，被称为“短路”。有些程序员喜欢用它取代if结构，比如下面是一段if结构的代码，就可以用且运算符改写。

{% highlight javascript %}

if (i !== 0 ){
	doSomething();
}

// 等价于

i && doSomething();

{% endhighlight %}

上面代码的两种写法是等价的，但是后一种不容易看出目的，也不容易除错，建议谨慎使用。

且运算符可以多个连用，这时返回第一个布尔值为false的表达式的值。

{% highlight javascript %}

true && 'foo' && '' && 4 && 'foo' && true
// ''

{% endhighlight %}

上面代码中第一个布尔值为false的表达式为第三个表达式，所以得到一个空字符串。

### 或运算符（||）

或运算符的运算规则是：如果第一个运算子的布尔值为true，则返回第一个运算子的值，且不再对第二个运算子求值；如果第一个运算子的布尔值为false，则返回第二个运算子的值。

{% highlight javascript %}

"t" || "" // "t"
"t" || "f" // "t"
"" || "f" // "f"
"" || "" // ""

{% endhighlight %}

短路规则对这个运算符也适用。

或运算符可以多个连用，这时返回第一个布尔值为true的表达式的值。

{% highlight javascript %}

false || 0 || '' || 4 || 'foo' || true
// 4

{% endhighlight %}

上面代码中第一个布尔值为true的表达式是第四个表达式，所以得到数值4。

或运算符常用于为一个变量设置默认值。

{% highlight javascript %}

function saveText(text) {
    text = text || '';
    // ...
}

// 或者写成

saveText(this.text||'')

{% endhighlight %}

上面代码表示，如果函数调用时，没有提供参数，则该参数默认设置为空字符串。

### 三元条件运算符（ ? :）

三元条件运算符用问号（？）和冒号（：），分隔三个表达式。如果第一个表达式的布尔值为true，则返回第二个表达式的值，否则返回第三个表达式的值。

{% highlight javascript %}

"t" ? true : false // true

0 ? true : false // false

{% endhighlight %}

上面代码的“t”和0的布尔值分别为true和false，所以分别返回第二个和第三个表达式的值。

通常来说，三元条件表达式与if...else语句具有同样表达效果，前者可以表达的，后者也能表达。但是两者具有一个重大差别，if...else是语句，没有返回值；三元条件表达式是表达式，具有返回值。所以，在需要返回值的场合，只能使用三元条件表达式，而不能使用if..else。

{% highlight javascript %}

var check = true ? console.log('T') : console.log('F');

console.log(true ? 'T' : 'F');

{% endhighlight %}

上面代码是赋值语句和console.log方法的例子，它们都需要使用表达式，这时三元条件表达式就能满足需要。如果要用if...else语句，就必须改变整个代码写法了。

## 位运算符

### 简介

位运算符用于直接对二进制位进行计算，一共有7个。

- **或运算**（or）：符号为|，表示两个二进制位中有一个为1，则结果为1，否则为0。

- **与运算**（and）：符号为&，表示两个二进制位都为1，则结果为1，否则为0。

- **否运算**（not）：符号为～，表示将一个二进制位变成相反值。

- **异或运算**（xor）：符号为&#710;，表示两个二进制位中有且仅有一个为1时，结果为1，否则为0。

- **左移运算**（left shift）：符号为<<，详见下文解释。

- **右移运算**（right shift）：符号为>>，详见下文解释。

- **带符号位的右移运算**（zero filled right shift）：符号为>>>，详见下文解释。

这些位运算符直接处理每一个比特位，所以是非常底层的运算，好处是速度极快，缺点是很不直观，许多场合不能使用它们，否则会带来过度的复杂性。

有一点需要特别注意，位运算符只对整数起作用，如果一个运算子不是整数，会自动转为整数后再运行。另外，虽然在JavaScript内部，数值都是以64位浮点数的形式储存，但是做位运算的时候，是以32位带符号的整数进行运算的，并且返回值也是一个32位带符号的整数。

{% highlight javascript %}

i = i|0;

{% endhighlight %}

上面这行代码的意思，就是将i转为32位整数。

### “或运算”与“与运算”

这两种运算比较容易理解，就是逐位比较两个运算子。“或运算”的规则是，如果两个二进制位之中至少有一个位为1，则返回1，否则返回0。“与运算”的规则是，如果两个二进制位之中至少有一个位1为0，则返回0，否则返回1。

{% highlight javascript %}

0 | 3 // 3
0 & 3 // 0

{% endhighlight %}

上面两个表达式，0和3的二进制形式分别是00和11，所以进行“或运算”会得到11（即3），进行”与运算“会得到00（即0）。

位运算只对整数有效，遇到小数时，会将小数部分舍去，只保留整数部分。所以，将一个小数与0进行或运算，等同于对该数去除小数部分，即取整数位。

{% highlight javascript %}

2.9 | 0
// 2

-2.9 | 0
// -2

{% endhighlight %}

需要注意的是，这种取整方法不适用超过32位整数最大值2147483647的数。

{% highlight javascript %}

2147483649.4 | 0;
// -2147483647

{% endhighlight %}

### 否运算

“否运算”将每个二进制位都变为相反值（0变为1，1变为0）。它的返回结果有时比较难理解，因为涉及到计算机内部的数值表示机制。

{% highlight javascript %}

~ 3 // -4

{% endhighlight %}

上面表达式对3进行“否运算”，得到-4。之所以会有这样的结果，是因为位运算时，JavaScirpt内部将所有的运算子都转为32位的二进制整数再进行运算。3在JavaScript内部是00000000000000000000000000000011，否运算以后得到11111111111111111111111111111100，由于第一位是1，所以这个数是一个负数。JavaScript内部采用2的补码形式表示负数，即需要将这个数减去1，再取一次反，然后加上负号，才能得到这个负数对应的10进制值。这个数减去1等于11111111111111111111111111111011，再取一次反得到00000000000000000000000000000100，再加上负号就是-4。考虑到这样的过程比较麻烦，可以简单记忆成，一个数与自身的取反值相加，等于-1。

{% highlight javascript %}

~ -3 // 2

{% endhighlight %}

上面表达式可以这样算，-3的取反值等于-1减去-3，结果为2。

对一个整数连续两次“否运算”，得到它自身。

{% highlight javascript %}

~~3 // 3

{% endhighlight %}

所有的位运算都只对整数有效。否运算遇到小数时，也会将小数部分舍去，只保留整数部分。所以，对一个小数连续进行两次否运算，能达到取整效果。

{% highlight javascript %}

~~2.9
// 2

{% endhighlight %}

使用否运算取整，是所有取整方法中最快的一种。

对字符串进行否运算，JavaScript引擎会先调用Number函数，将字符串转为数值。

```javascript

// 以下例子相当于~Number('011')
~'011'  // -12
~'42 cats' // -1
~'0xcafebabe' // 889275713
~'deadbeef' // -1

// 以下例子相当于~~Number('011')
~~'011';        // 11        
~~'42 cats';    // 0
~~'0xcafebabe'; // -889275714
~~'deadbeef';   // 0

```

Number函数将字符串转为数值的规则，参见《数据的类型转换》一节。否运算对特殊数值的处理是：超出32位的整数将会被截去超出的位数，NaN和Infinity转为0。

### 异或运算

“异或运算”在两个二进制位不同时返回1，相同时返回0。

{% highlight javascript %}

0^3 // 3

{% endhighlight %}

上面表达式中，0的二进制形式是00，3的二进制形式是11，它们每一个二进制位都不同，所以得到11（即3）。

“异或运算”有一个特殊运用，连续对两个数a和b进行三次异或运算，a&#710;=b, b&#710;=a, a&#710;=b，可以互换它们的值（详见[维基百科](http://en.wikipedia.org/wiki/XOR_swap_algorithm)）。这意味着，使用“异或运算”可以在不引入临时变量的前提下，互换两个变量的值。

{% highlight javascript %}

var a = 10;
var b = 99;

a^=b, b^=a, a^=b;

a // 99
b // 10

{% endhighlight %}

这是互换两个变量的值的最快方法。

异或运算也可以用来取整。

```javascript

12.9^0 // 12

```

### 左移运算符（<<）

左移运算符表示将一个数的二进制形式向前移动，尾部补0。

{% highlight javascript %}

4 << 1
// 8
// 因为4的二进制形式为100，左移一位为1000（即十进制的8）

-4 << 1
// -8

{% endhighlight %}

上面代码中，-4左移一位之所以得到-8，是因为-4的二进制形式是11111111111111111111111111111100，左移一位后得到11111111111111111111111111111000，该数转为十进制（减去1后取反，再加上负号）即为-8。

如果左移0位，就相当于取整，对于正数和负数都有效。

```javascript

13.5 << 0
// 13

-13.5 << 0
// -13

```

左移运算符用于二进制数值非常方便。

{% highlight javascript %}

var color = {r: 186, g: 218, b: 85};

// RGB to HEX
var rgb2hex = function(r, g, b) {
    return '#' + ((1 << 24) + (r << 16) + (g << 8) + b).toString(16).substr(1);
}

rgb2hex(color.r,color.g,color.b)
// "#bada55"

{% endhighlight %}

上面代码使用左移运算符，将颜色的RGB值转为HEX值。

### 右移运算符（>>）

右移运算符表示将一个数的二进制形式向右移动，头部补上最左位的值，即整数补0，负数补1。

{% highlight javascript %}

4 >> 1
// 2
/* 
// 因为4的二进制形式为00000000000000000000000000000100，
// 右移一位得到00000000000000000000000000000010，
// 即为十进制的2
*/

-4 >> 1
// -2
/*
// 因为-4的二进制形式为11111111111111111111111111111100，
// 右移一位，头部补1，得到11111111111111111111111111111110,
// 即为十进制的-2
*/

{% endhighlight %}

右移运算可以模拟2的整除运算。

```javascript

5 >> 1 
// 相当于 5 / 2 = 2
 
21 >> 2 
// 相当于 21 / 4 = 5
 
21 >> 3 
// 相当于 21 / 8 = 2

21 >> 4 
// 相当于 21 / 16 = 1

```

### 带符号位的右移运算符（>>>）

该运算符表示将一个数的二进制形式向右移动，不管正数或负数，头部一律补0。所以，该运算总是得到正值，这就是它的名称“带符号位的右移”的涵义。对于正数，该运算的结果与右移运算符（>>）完全一致，区别主要在于负数。

{% highlight javascript %}

4 >>> 1
// 2

-4 >>> 1
// 2147483646
/*
// 因为-4的二进制形式为11111111111111111111111111111100，
// 带符号位的右移一位，得到01111111111111111111111111111110，
// 即为十进制的2147483646。
*/

{% endhighlight %}

### 开关作用

位运算符可以用作设置对象属性的开关。

假定某个对象有四个开关，每个开关都是一个变量，取值为2的整数次幂。

{% highlight javascript %}

var FLAG_A = 1; // 0001
var FLAG_B = 2; // 0010
var FLAG_C = 4; // 0100
var FLAG_D = 8; // 1000

{% endhighlight %}

上面代码设置A、B、C、D四个开关，每个开关分别占有1个二进制位。

现在假设需要打开ABD三个开关，我们可以构造一个掩码变量。

{% highlight javascript %}

var mask = FLAG_A | FLAG_B | FLAG_D; // 0001 | 0010 | 1000 => 1011

{% endhighlight %}

上面代码对ABD三个变量进行“或运算”，得到掩码值为二进制的1011。

有了掩码，就可以用“与运算”检验当前设置是否与开关设置一致。

{% highlight javascript %}

if (flags & FLAG_C) { // 0101 & 0100 => 0100 => true
   // ...
}

{% endhighlight %}

上面代码表示，如果当前设置与掩码一致，则返回true，否则返回false。

“或运算”可以将当前设置改成开关设置。

{% highlight javascript %}

flags |= mask; 

{% endhighlight %}

“与运算”可以将当前设置中凡是与开关设置不一样的项，全部关闭。

{% highlight javascript %}

flags &= mask; 

{% endhighlight %}

“异或运算”可以切换（toggle）当前设置。

{% highlight javascript %}

flags = flags ^ mask; 

{% endhighlight %}

“否运算”可以翻转当前设置。

{% highlight javascript %}

flags = ~flags;

{% endhighlight %}

## 其他运算符

### 圆括号运算符

在JavaScript中，圆括号是一种运算符，它有两种用法：如果把表达式放在圆括号之中，作用是求值；如果跟在函数的后面，作用是调用函数。

把表达式放在圆括号之中，将返回表达式的值。

{% highlight javascript %}

(1) // 1
('a') // a
(1+2) // 3

{% endhighlight %}

把对象放在圆括号之中，则会返回对象的值，即对象本身。

{% highlight javascript %}

var o = {p:1};

(o)
// Object {p: 1}

{% endhighlight %}

将函数放在圆括号中，会返回函数本身。如果圆括号紧跟在函数的后面，就表示调用函数，即对函数求值。

{% highlight javascript %}

function f(){return 1;}

(f) // function f(){return 1;}
f() // 1

{% endhighlight %}

上面的代码先定义了一个函数，然后依次将函数放在圆括号之中、将圆括号跟在函数后面，得到的结果是不一样的。

由于圆括号的作用是求值，如果将语句放在圆括号之中，就会报错，因为语句没有返回值。

{% highlight javascript %}

(var a =1)
// SyntaxError: Unexpected token var

{% endhighlight %}

### void运算符

void运算符的作用是执行一个表达式，然后返回undefined。

{% highlight javascript %}

void 0 // undefined
void (0) // undefined

{% endhighlight %}

上面是void运算符的两种写法，都正确。建议采用后一种形式，即总是使用括号。因为void运算符的优先性很高，如果不使用括号，容易造成错误的结果。比如，void 4+7 实际上等同于 (void 4) +7 。

下面是void运算符的一个例子。

{% highlight javascript %}

var x = 3;
void (x = 5) //undefined
x // 5

{% endhighlight %}

这个运算符主要是用于书签工具（bookmarklet）或者用于在超级链接中插入代码，目的是返回undefined可以防止网页跳转。

{% highlight javascript %}

javascript:void window.open("http://example.com/")

{% endhighlight %}

比如，下面是常用于网页链接的触发鼠标点击事件的写法。

{% highlight html %}

<a href="#" onclick="f();">文字</a>

{% endhighlight %}

上面代码有一个问题，函数f必须返回false，或者onclick事件必须返回false，否则会引起浏览器跳转到另一个页面。

{% highlight html %}

function f(){
	// some code
	return false;
}

{% endhighlight %}

或者写成

{% highlight html %}

<a href="#" onclick="f();return false;">文字</a>

{% endhighlight %}

void运算符可以取代上面两种写法。

{% highlight html %}

<a href="javascript:void(0)" onclick="f();">文字</a>

{% endhighlight %}

### 逗号运算符

逗号运算符用于对两个表达式求值，并返回后一个表达式的值。

{% highlight javascript %}

"a", "b" // "b"

var x = 0;
var y = (x++, 10);
x // 1
y // 10

{% endhighlight %}

## 运算顺序

**（1）运算符的优先级**

JavaScript各种运算符的优先级别（Operator Precedence）是不一样的。优先级高的运算符先执行，优先级低的运算符后执行。

```javascript
4 + 5 * 6 // 34
```

上面的代码中，乘法运算符（*）的优先性高于加法运算符（+），所以先执行乘法，再执行加法，相当于下面这样。

```javascript
4 + (5 * 6) // 34
```

如果多个运算符混写在一起，常常会导致令人困惑的代码。

```javascript
var x = 1;
var arr = [];

var y = arr.length <= 0 || arr[0] === undefined ? x : arr[0];
```

上面代码中，变量`y`的值就很难看出来，因为这个表达式涉及5个运算符，到底谁的优先级最高，实在不容易记住。

根据语言规格，这五个运算符的优先级从高到低依次为：小于等于（<=)、严格相等（===）、或（||）、三元（?:）、等号（=）。因此上面的表达式，实际的运算顺序如下。

```javascript
var y = ((arr.length <= 0) || (arr[0] === undefined)) ? x : arr[0];
```

记住所有运算符的优先级，几乎是不可能的，也是没有必要的。

**（2）圆括号的作用**

圆括号可以用来提高运算的优先级，因为它的优先级是最高的，即圆括号中的运算符会第一个运算。

```javascript
(4 + 5) * 6 // 54
```

上面代码中，由于使用了圆括号，加法会先于乘法执行。

由于运算符的优先级别十分繁杂，且都是来自硬性规定，所以本书不打算列出具体的规则，只是建议读者总是使用圆括号，保证运算顺序清晰可读，这对代码的维护和除错至关重要。

**（3）左结合与右结合**

对于优先级别相同的运算符，大多数情况，计算顺序总是从左到右，这叫做运算符的“左结合”（left-to-right associativity），即从左边开始计算。

```javascript
x + y + z
```

上面代码先计算最左边的x与y的和，然后再计算与z的和。

但是少数运算符的计算顺序是从右到左，即从右边开始计算，这叫做运算符的“右结合”（right-to-left associativity）。其中，最主要的是赋值运算符（=）和三元条件运算符（?:）。

```javascript
w = x = y = z;
q = a ? b : c ? d : e ? f : g;
```

上面代码的运算结果，相当于下面的样子。

```javascript
w = (x = (y = z));
q = a ? b : (c ? d : (e ? f : g));
```

## 参考链接

- Michal Budzynski, [JavaScript: The less known parts. Bitwise Operators](http://michalbe.blogspot.co.uk/2013/03/javascript-less-known-parts-bitwise.html)
- Axel Rauschmayer, [Basic JavaScript for the impatient programmer](http://www.2ality.com/2013/06/basic-javascript.html)
- Mozilla Developer Network, [Bitwise Operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators)
