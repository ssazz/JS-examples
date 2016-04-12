Template literals are string literals allowing embedded expressions. You can use multi-line strings and string interpolation features with them. They were called "template strings" in prior editions of the ES2015 / ES6 specification.
#[Template literals from MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
##Tagged template literals
A more advanced form of template literals are tagged template literals. With them you are able to modify the output of template literals using a function. The first argument contains an array of string literals ("Hello " and " world" in this example). The second, and each argument after the first one, are the values of the processed (or sometimes called cooked) substitution expressions ("15" and "50" here). In the end, your function returns your manipulated string. There is nothing special about the name tag in the following example. The function name may be anything you want.
```js
var a = 5;
var b = 10;

function tag(strings, ...values) {
  console.log(strings[0]); // "Hello "
  console.log(strings[1]); // " world "
  console.log(values[0]);  // 15
  console.log(values[1]);  // 50

  return "Bazinga!";
}

tag`Hello ${ a + b } world ${ a * b }`;
// "Bazinga!"
```
Tag functions need not return a string, as shown in the following example.
```js
function template(strings, ...keys) {
  return (function(...values) {
    var dict = values[values.length - 1] || {};
    var result = [strings[0]];
    keys.forEach(function(key, i) {
      var value = Number.isInteger(key) ? values[key] : dict[key];
      result.push(value, strings[i + 1]);
    });
    return result.join('');
  });
}

var t1Closure = template`${0}${1}${0}!`;
t1Closure('Y', 'A');  // "YAY!" 
var t2Closure = template`${0} ${'foo'}!`;
t2Closure('Hello', {foo: 'World'});  // "Hello World!"
```
