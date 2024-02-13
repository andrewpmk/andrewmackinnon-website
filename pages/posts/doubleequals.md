---
title: Don't use double equals signs in JavaScript!
date: 2024-02-12
tag: javascript
author: Andrew MacKinnon
---

A common beginner mistake in JavaScript is to use double equals signs (```==```) or a not equals sign with one equals sign
(```!=```), for example:

```javascript
let x = 1;
if (x == 1) {
    console.log("x is equal to 1");
}
```

Don't do this. The reason is that unlike any other programming language that I am aware of, JavaScript coerces
values of one data type to another in such a way that values that are not equal are considered to be equal when using
the double equals sign. For example these expressions are all true:

```javascript
1 == "1"
1 == true
"1" == true
undefined == null
0 == "000"
0 == BigInt(0)
```

Similarly, these expressions evaluate to false even though they are in fact not equal:

```javascript
1 != "1"
1 != true
"1" != true
undefined != null
0 != "000"
0 != BigInt(0)
```

Instead, always use the triple equals sign ```===``` for equals, and a not equals sign with two equals
signs ```!==``` for not equals. Many linter tools e.g. eslint, or the ReShaper extension for Visual Studio
will automatically produce warnings for issue. For obvious reasons if you are modifying existing code,
make sure you don't introduce bugs accidentally if your code is dependent on the weird behaviour of the ```==``` or ```!=``` syntax.</p>

If you **really** need to reproduce the behaviour of ```==``` or ```!=``` for your code, try using a cast and using ```===``` or ```!==```
like this:

```javascript
1 === Number("1")
1 === Number("true")
```

This way it is obvious that you are doing a cast and it won't trigger warnings in eslint.

See also: [Equality comparisons and sameness (from Mozilla Developer)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)