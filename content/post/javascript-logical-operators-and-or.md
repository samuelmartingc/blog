+++
title = "JavaScript Logical Operators (AND, OR)"
description = "JavaScript Logical Operators (AND, OR)"
tags = [
    "development",
    "javascript",
]
date = "2016-04-17"
categories = [
    "Development",
]

image = "empty.jpg" # optional
toc = true # optional, When set to TRUE this parameter, table of contents appears in only this article.
+++

Classical logical operators are used with Boolean values, and returns the corresponding Boolean.
However, in JavaScript, the && (and) and || (or) values ​​work in a most peculiar way.
When working with different non-Boolean types, they convert the left value on a boolean, and depending on the result of this conversion, they will return the original left value or the right one.

For example, the OR operator will return the value of its left if this has proved true, and if it was false, then it return the right.

AND operator works similarly, but in reverse. If the value of the left is true, it will return automatically the right one, and if not, the left one.
The AND truth table only return a true if both are true, so if the first value was false, it will return this without looking at the rest of the assertion, but if it was true, then it will have to look at the second element, which is the returned value.
We know the number 0 is false and any other is true. We will understand these concepts better with some basic examples.

```js
//OR
console.log(1 || 2) // 1
console.log(0 || 2) // 2
//AND
console.log(1 && 2) // 2
console.log(0 && 2) // 0
```

Another important property is that the right expression only runs when needed, so that although the implementation of the second part had important consequences, if not necessary, it will not be executed. This is called short-circuit evaluation.
