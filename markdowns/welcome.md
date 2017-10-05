# Part 5 - Developer’s Guide: Built-in String Functions

Welcome back, In the [previous](https://tech.io/playgrounds/6671/modern-es6-javascript-pt--4) article we covered an Intro about Strings and Template Strings, now this article and Part 6 will look to cover all the **built-in** **String Properties and Methods** within JavaScript. Please note that we will only cover those properties that are currently available within the working draft of ECMAScript.

Now believe or not, Understanding these built-in methods/functions is the utmost important thing when it comes to programming in JavaScript. You would be using them a lot for generating the required data and even use them to create your own functions in JavaScript.

## length

The `length` property is used to reflect the number of elements within a particular String value. Once the String object is initialized, this property is immutable.

```javascript
str.length
```

**Example**

```javascript runnable
let name = 'Harry';
let empty = '';

console.log('Harry is ' + name.length + ' code units long');
/* => Harry is 5 code units long */

console.log('The empty string has a length of ' + empty.length);
/* => The empty string has a length of 0 */
```

## charAt()

The `charAt()` method is used to return a single element String containing the code unit at index position within a particular String value. 

Characters within a string are indexed from left to right. Please note that the index of the first character is 0, and the index of the last character in a string called `stringName` is `stringName.length - 1`. 

If the index you are supplying is out of range, it will return an empty string. If no index is provided, then 0 will be used as default value.

```javascript
str.charAt(index)
```

**Parameters**

`index`

> An integer between 0 and 1-less-than the length of the string. If no index is provided, `charAt()` will use `0`.

**Example**

```javascript runnable
let goodParts = 'JavaScript, The Good Parts!';
console.log("The character at index 0   is '" + goodParts.charAt()   + "'"); 
// No index was provided, used 0 as default

console.log("The character at index 0   is '" + goodParts.charAt(0)   + "'");
console.log("The character at index 1   is '" + goodParts.charAt(1)   + "'");
console.log("The character at index 2   is '" + goodParts.charAt(2)   + "'");
console.log("The character at index 3   is '" + goodParts.charAt(3)   + "'");
console.log("The character at index 4   is '" + goodParts.charAt(4)   + "'");
console.log("The character at index 999 is '" + goodParts.charAt(999) + "'");
// This will print blank '' as there isn't a index 199 within this String.
```

## charCodeAt()

The `charCodeAt()` method is used to return a non-negative integer between 0 and 65535 (2^16 - 1) representing the UTF-16 code unit at the given index. If there is no element at that index, the result is NaN. 

[keycodes.atjayjo.com](http://keycodes.atjayjo.com/) is a great website for getting character code for regular keyboard inputs.

Note that the `charCodeAt()` function is intentionally generic. It does not require that its **this** value be a String object. Thus, it can be transferred to other kinds of objects for use as a method.

```javascript
str.charCodeAt(index)
```

**Parameters**

`index`

> An integer greater than or equal to 0 and less than the length of the string; if it is not a number, it defaults to 0.

**Example**

```javascript runnable
const a = 'Larry Page'.charCodeAt(6); 
console.log(a);
/*=> returns 80 as character `P` is at index 6 */
```

## codePointAt()

Added in ECMAScript 6, It is used to return a non-negative integer that is less than 0x110000, the code point value of the UTF-16 encoded code point starting at the string element at index position within the String. If there is no element at the specified position, undefined is returned.

Same like `charCodeAt()`, the `codePointAt()` function is also intentionally generic. It does not require that its **this** value be a String object. Thus, it can be transferred to other kinds of objects for use as a method.

The whole list of the **unicode characters** can be found [here](http://www.fileformat.info/info/unicode/char/a.htm). Don’t worry, just keep it as reference, you don’t need to memorise them.

```javascript
str.codePointAt(pos)
```

**Parameters**

`pos`

> Position of an element in the String to return the code point value from.

**Example**

```javascript runnable
const b = 'Harry'.codePointAt(1);          
console.log(b); //=> 97

const c = '\uD800\uDC00'.codePointAt(0); 
console.log(c); //=> 65536

const d = 'Larry'.codePointAt(42); 
console.log(d); //=> undefined
```    

As this method is added in ECMAScript 6 and thus is not supported in all web browsers or environments. You can use this [code](https://github.com/mathiasbynens/String.prototype.codePointAt/blob/master/codepointat.js) as a polyfill.

## fromCharCode()

The `fromCharCode()` method is used to return a string that is created by using the specified sequence of Unicode values. As, `fromCharCode()` is a static method of String, you can always use it as String.fromCharCode(), rather than as a method of a String object you have created.

```javascript
String.fromCharCode(num1[, ...[, numN]])
```

**Parameters**

`num1, ..., num``*N*`


> A sequence of numbers that are Unicode values.

**Example**

```javascript runnable
const e = String.fromCharCode(72, 65, 82, 82, 89);
console.log(e); //=> HARRY
```

## fromCodePoint()

Added in ECMAScript 6, `fromCodePoint()` method is used to return a string that is created by using the specified sequence of code points. Please note that this method returns a string and not the String object.

```javascript
String.fromCodePoint(num1[, ...[, numN]])
```

**Parameters**

`num1, ..., numN`

> A sequence of code points.

**Example**

```javascript runnable
console.log(String.fromCodePoint(65));       //=> A
console.log(String.fromCodePoint(72, 89));   //=> HY
console.log(String.fromCodePoint(0x404));    //=> \u0404
console.log(String.fromCodePoint(0x2F804));  //=> \uD87E\uDC04
console.log(String.fromCodePoint(194564));   //=> \uD87E\uDC04
console.log(String.fromCodePoint(0x1D306, 0x61, 0x1D307)); 
//=> \uD834\uDF06a\uD834\uDF07
```

All the below code will produce RangeError. A RangeError is thrown if an invalid Unicode code point is given.

```javascript runnable
console.log(String.fromCodePoint('_'));      // RangeError
console.log(String.fromCodePoint(Infinity)); // RangeError
console.log(String.fromCodePoint(-1));       // RangeError
console.log(String.fromCodePoint(3.14));     // RangeError
console.log(String.fromCodePoint(3e-2));     // RangeError
console.log(String.fromCodePoint(NaN));      // RangeError
```

As this method is added in ECMAScript 6 and thus is not supported in all web browsers or environments. You can use this [code](https://github.com/mathiasbynens/String.fromCodePoint/blob/master/fromcodepoint.js) as a polyfill.

## concat()

The concat() method is used to combines the text of two strings and returns a new string. Please note that the result is a String value, and not a String object.

The `concat()` function is intentionally generic. It does not require that its **this** value be a String object. Thus, it can be transferred to other kinds of objects for use as a method.

It is strongly been recommended that assignment operators (`+`, `+=`) should be used instead of the `concat()` method. See this [performance test](http://jsperf.com/concat-vs-plus-vs-join).

```javascript
str.concat(string2[, string3, ..., stringN])
```

**Parameters**

`string2...string``*N*`

> Strings to concatenate to this string.

**Example**

```javascript runnable
let hello = 'Hello, ';
console.log(hello.concat('Larry', ' have a nice day.'));
/*=> Hello, Larry have a nice day. */

let wiseSeeker = ['Ok', ' ', 'Google', '!'];
console.log("".concat(...wiseSeeker)); //=> Ok Google
```    

## endsWith()

This method is used to determine whether the string ends with the characters of another string, returning `true` or `false` as appropriate. This method is case-sensitive.

```javascript
str.endsWith(searchString[, length])
```

**Parameters**

`searchString`

> The characters to be searched for at the end of this string.

`length`

> **Optional**. If provided overwrites the considered length of the string to search in. If omitted, the default value is the length of the string.

**Example**

```javascript runnable
let question = 'To be, or not to be, that is the question.';

console.log(question.endsWith('question.')); // true
console.log(question.endsWith('to be'));     // false
console.log(question.endsWith('to be', 19)); // true
```

## includes()

The `includes()` method is used to determine whether one string may be found within another string, returning true or false as appropriate. This method is case-sensitive.

```javascript
arr.includes(searchElement, fromIndex)
```

**Parameters**

`searchElement`

> The element to search for.

`fromIndex`

> **Optional**. The position in this array at which to begin searching for searchElement. A negative value searches from the index of array.length + fromIndex by asc. Defaults to 0.

**Example**

```javascript runnable
let question2 = 'To be, or not to be, that is the question.';
    
console.log(question2.includes('To be'));       //=> true
console.log(question2.includes('question'));    //=> true
console.log(question2.includes('nonexistent')); //=> false
console.log(question2.includes('To be', 1));    //=> false
console.log(question2.includes('TO BE'));       //=> false
```

## indexOf()

It is used to return an index within the calling String object of the first occurrence of the specified value, starting the search at `fromIndex`. Returns -1 if the value is not found.

Characters in a string are indexed from left to right. The index of the first character is 0, and the index of the last character of a string called `stringName` is `stringName.length - 1`.

The `indexOf()` function is intentionally generic. It does not require that its **this** value be a String object. Thus, it can be transferred to other kinds of objects for use as a method.

The `indexOf()` method is case sensitive.

```javascript
str.indexOf(searchValue[, fromIndex])
```

**Parameters**

`searchValue`

> A string representing the value to search for.

`fromIndex`

> An integer representing the index at which to start the search; the default value is `0`. If `fromIndex <= 0` the entire string is searched. If `fromIndex >= str.length`, the string is not searched and `-1` is returned. If `searchValue` is an empty string, the behaviour is as follows — if `fromIndex < str.length`, `fromIndex` is returned; if `fromIndex >= str.length`, `str.length` is returned.

**Example**

```javascript runnable
console.log('Harry Manchanda'.indexOf('Harry')); //=> returns  0
console.log('Harry Manchanda'.indexOf('Larry')); //=> returns -1
console.log('Harry Manchanda'.indexOf('Manchanda', 0)); //=> returns  6
console.log('Harry Manchanda'.indexOf('Manchanda', 6)); //=> returns  6
console.log('Harry Manchanda'.indexOf('Manchanda', 7)); //=> returns -1
console.log('Harry Manchanda'.indexOf(''));  //=> returns  0
console.log('Harry Manchanda'.indexOf('H')); //=> returns  0
```

## lastIndexOf()

It is used to return an index within the calling String object of the first occurrence of the specified value, starting the search at `fromIndex`. Returns -1 if the value is not found.

Characters in a string are indexed from left to right. The index of the first character is 0, and the index of the last character of a string called `stringName` is `stringName.length - 1`.

The `lastIndexOf()` function is intentionally generic. It does not require that its **this** value be a String object. Thus, it can be transferred to other kinds of objects for use as a method.

The `lastIndexOf()` method is case sensitive.

```javascript
str.lastIndexOf(searchValue[, fromIndex])
```

**Parameters**

`searchValue`

> A string representing the value to search for. If `searchValue` is an empty string, then `fromIndex` is returned.

`fromIndex`

> The index at which to start searching backwards in the string. Starting with this index, the left part of the string will be searched. It can be any integer. The default value is `+Infinity`. If `fromIndex >= str.length`, the whole string is searched. If `fromIndex < 0`,  the behavior will be the same as if it would be `0`.

**Example**

```javascript runnable
console.log('cena'.lastIndexOf('a'));     //=> returns 3
console.log('cena'.lastIndexOf('e', 2));  //=> returns 1
console.log('cena'.lastIndexOf('a', 0));  //=> returns -1
console.log('cena'.lastIndexOf('x'));     //=> returns -1
console.log('cena'.lastIndexOf('c', -5)); //=> returns 0
console.log('cena'.lastIndexOf('c', 0));  //=> returns 0
console.log('cena'.lastIndexOf(''));      //=> returns 4
console.log('cena'.lastIndexOf('', 2));   //=> returns 2
```

## localeCompare()

It is used to return a number indicating whether the reference string comes before or after or is the same as the given string in sort order.

Note that the new locales and options arguments help applications to specify the language whose sort order should be used and customize the behavior of the function. In older implementations, which ignore the locales and options arguments, the locale and sort order used is entirely implementation dependent.

Please note that you shouldn't rely on exact return values of -1 or 1. The negative and positive integer results vary between browsers (as well as between browser versions) because the W3C specification only mandates negative and positive values. Some browsers may return -2 or 2 or even some other negative or positive value.

```javascript
referenceStr.localeCompare(compareString[, locales[, options]])
```

**Parameters**

`compareString`

> The string against which the referring string is compared

`locales` & `options`

> **Optional**. Their usage, properties and Unicode extension keys can be found [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare#Browser_compatibility).

**Example**

```javascript runnable
// The letter "a" is before "c" yielding a negative value
console.log('a'.localeCompare('c')); // -2 or -1 (or some other negative value)

// Alphabetically the word "check" comes after "against" yielding a positive value
console.log('check'.localeCompare('against')); // 2 or 1 (or some other positive value)

// "a" and "a" are equivalent yielding a neutral value of zero
console.log('a'.localeCompare('a')); // 0
```

**Sort an array:** `localeCompare` enables a case-insensitive sort of an array.

```javascript runnable
let items = ['JavaScript', 'Php', 'Ruby', 'Perl', 'Python', 'Java'];

// Arrow function, we will discuss it soon!
console.log(items.sort((a, b) => a.localeCompare(b))); 
//=> [ 'Java', 'JavaScript', 'Perl', 'Php', 'Python', 'Ruby' ]
```

## match()

This method is used to retrieve the matches when matching a *string* against a *regular expression*. Wait! Regular expression*?* Don’t worry we will cover that soon, just follow along for now.

```javascript
str.match(regexp)
```

**Parameters**

`regexp`

> A regular expression object. If a non-RegExp object obj is passed, it is implicitly converted to a RegExp by using new RegExp(obj). If you don't give any parameter and use the match() method directly, you will get an Array with an empty string:[""].

**Example**

```javascript runnable
let str = 'For more information, see Chapter 3.4.5.1';
let reg = /see (chapter \d+(\.\d)*)/i;
let loggedResult = str.match(reg);

console.log(loggedResult);
```

This will log the code below:

```bash
[ 'see Chapter 3.4.5.1',
  'Chapter 3.4.5.1',
  '.1',
  index: 22,
  input: 'For more information, see Chapter 3.4.5.1' ]
```

**Why?**

- 'see Chapter 3.4.5.1' is the whole match.
- 'Chapter 3.4.5.1' was captured by '(chapter \d+(\.\d)*)'.
- '.1' was the last value captured by '(\.\d)'.
- The 'index' property (22) is the zero-based index of the whole match.
- The 'input' property is the original string that was parsed.
## normalize()

This method is used to retrieve the Unicode Normalization Form of a given string. If the value isn't a string, it will be converted to one first.

```javascript
str.normalize([form]);
```

**Parameters**

`form`

> One of "NFC", "NFD", "NFKC", or "NFKD", specifying the Unicode Normalization Form. If omitted or undefined, "NFC" is used.
> 
> NFC — Normalization Form Canonical Composition.
> NFD — Normalization Form Canonical Decomposition.
> NFKC — Normalization Form Compatibility Composition.
> NFKD — Normalization Form Compatibility Decomposition.

**Example**

```javascript runnable
// Initial string

// U+1E9B: LATIN SMALL LETTER LONG S WITH DOT ABOVE
// U+0323: COMBINING DOT BELOW
let wow = '\u1E9B\u0323';

// Canonically-composed form (NFC)
// U+1E9B: LATIN SMALL LETTER LONG S WITH DOT ABOVE
// U+0323: COMBINING DOT BELOW
console.log(wow.normalize('NFC')); //=> \u1E9B\u0323
// same as above
console.log(wow.normalize());      //=> \u1E9B\u0323

// Canonically-decomposed form (NFD)
// U+017F: LATIN SMALL LETTER LONG S
// U+0323: COMBINING DOT BELOW
// U+0307: COMBINING DOT ABOVE
console.log(wow.normalize('NFD')); //=> \u017F\u0323\u0307

// Compatibly-composed (NFKC)
// U+1E69: LATIN SMALL LETTER S WITH DOT BELOW AND DOT ABOVE
console.log(wow.normalize('NFKC')); //=> \u1E69

// Compatibly-decomposed (NFKD)
// U+0073: LATIN SMALL LETTER S
// U+0323: COMBINING DOT BELOW
// U+0307: COMBINING DOT ABOVE
console.log(wow.normalize('NFKD')); //=> \u0073\u0323\u0307
```

## Relax! Have a Break, To be continued…

**Woah! All of this is hard to grasp at one go. Isn’t it?** 

Don’t worry, Relax… have a break, enjoy the day and when you feel fresh, we will visit Part 6 (coming soon), and cover rest of the String methods available.

![](https://d2mxuefqeaa7sj.cloudfront.net/s_3D191AF1EE5302C5CFC73EBBDC320C676012D0390E23CB6E04D49E4F0A08F096_1506777038294_relax.png)

## References

This story has been proudly referenced from these links below:

- https://developer.mozilla.org/en-US/docs/Web/JavaScript
- https://tc39.github.io/ecma262/

## Thanks a lot…

***If you would like to hire me for your next cool project, or just want to say hello… my twitter handle is [@harmanmanchanda](http://bit.ly/tw-harry) for getting in touch with me! My DM’s are open to the public so just hit me up.***
