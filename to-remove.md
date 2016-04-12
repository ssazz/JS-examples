#Uncategorized


```js
var clear = console.clear,
    log   = console.log; 

function wrapValue(n) {
	var localVariable = n;
	return function() { return localVariable; };
}
var wrap1 = wrapValue(1),
    wrap2 = wrapValue(2);

//log("wrap1", wrap1());
//log("wrap2", wrap2());




function multiplier(factor) {
  return function(number) {
    return factor * number;
  };
}
var twice = multiplier(2);
//log("twice(6)", twice(6));




function min(a, b) {
  return a <= b ? a : b;
}
//log(min(10,8));




function isEven(number) {
  if(number === 1) {
    return console.log("nieparzysta");
  }
  else if(number === 0 ) {
    return console.log("parzysta");
  }
  return isEven(Math.abs(number - 2));
}
//isEven(-1);



function countBs(sentence) {
  var counter = 0;
  for (var i=0; i<sentence.length; i++) {
    if(sentence.charAt(i) == "B") counter++;
  }
  return console.log(counter);
}
//countBs("BaBka z Błażkowej koło Bytomia B");





function countChar(string, char) {
  var counter = 0, i=0;
  while(i<string.length) {
    if(string.charAt(i) == char) counter++;
    i++;
  }
  return {"string": string, "char": char, "counter": counter};
}
//log(countChar("BaBka z Błażkowej koło Bytomia B", "B")["counter"]);

var fizzbuzz;
for (var i=1; i<=15; i++) {
  fizzbuzz = i + " ";
  if (i % 3 === 0) fizzbuzz += "Fizz";
  if (i % 5 === 0) fizzbuzz += "Buzz";
  //log(fizzbuzz);
}



// rekurencja
var all_possibilities = [];
function rekurencja(num, tab) {
  var LICZBA = num; // liczba = 3;
  
  function tree(n, history) {
    if (n == LICZBA) {
      //return history;
      tab.push(history);
    } else if (n > LICZBA) {
      return null;
    }
      return tree(n * 3, "[" + history + " * 3]") || tree(n + 2, "[" + history + " + 2]");
  }
  return tree(1, "1");
}
rekurencja(15, all_possibilities);
//log(all_possibilities);
//log(all_possibilities.length);
all_posibilities = [];


// reverse
var tabka = [1, 2, 3, 4, 5, 6, 7, 8, 9];
function r(b)
{
  var a = [], i=0;
  while(i<b.length) a.unshift(b[i++]);
  return a;
}
//log(r(tabka));



function range(a, b) {
  var tab = [], i=0;
  while(i<=b-a) {
    tab.push(a+i);
    i++;
  }
  return tab;
}
function sum(tab) {
  var t=0, i=0;
  while(i < tab.length) t += tab[i++]; 
  return t;
}
//log(sum(range(1, 10)));



/*
var q = [1, 2, 3];

var newTab = q.reduce(function(sum, item){
  console.log("sum: ", sum, "item: ", item);
  return sum + item;
}, 20);
log(newTab);*/

var animals = ['dog', 'pig', 'cow', 'dog', 'cow', 'bird', 'dog'];
var kindOf = animals.reduce(function(obj, current) {
  obj[current] = (obj[current] + 1) || 1;
  return obj;
}, {});
//console.log(kindOf);

var forMap = [1, 2, 3, 4, 5];
var mapped = forMap.map(function(itemek){
  return itemek * 10;
});
//log("before map():", forMap, "after map():", mapped);

var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
var odd = numbers.filter(function(n){
  return n % 2 === 1;
});
log("metoda filter()", odd);





function numberToString(n, base)
{
  var result = '', sign = '';
  if (n < 0)
  {
    n = -n;
    sign = '-';
  }
  do
  {
    result = String(n % base) + result;
    n = Math.floor(n / base);
  } while (n > 0);
  return sign + result;
}
log(numberToString(4, 2));
clear();

function promptNumber(question)
{
  var result = Number(prompt(question, ''));
  if (isNaN(result)) return null;
  else return result;
}

log(promptNumber("Ile masz lat?"));

/* ==================wyjątki================== */
function promptDirection(question)
{
  var result = prompt(question, "");
  if (result.toLowerCase() === 'left') return "L";
  if (result.toLowerCase() === 'right') return "R";
  throw new Error("Invalid direction: " + result);
}
function look()
{
  if (promptDirection("W ktorą stronę?") == "L")
    return "dom";
  else 
    return "do dupki";
}
try
{
  log("Widzisz " + look());
} catch (error)
{
  log('Cos poszło nie tak: ' + error);
}
clear();

/*==============================*/
var context = null;
function withContext(newContext, body)
{
  var oldContext = context;
  context = newContext;
  try {
    return body();
  } finally {
    context = oldContext;
  }
}
try {
  withContext(5, function() {
    if (context < 10)
      throw new Error("za mało kontekstu!");
  });
} catch (e) {
  log("Ignorowanie: " + e);
}



log(numberToString(5,2));



/*
clear();

var box = {
  locked: true,
  unlock: function() { this.locked = false; },
  lock:   function() { this.locked = true;  },
  _content: [1, 2, 3],
  get content() {
    if (this.locked) throw new Error("Zamknięte!");
    return this._content;
  }
};

function withBoxUnlocked(func) {
  try {
    func.call(box);
    return box.content;
  } finally {
   box.lock();
  }
}

log(withBoxUnlocked(box.unlock));
*/

/* ===================================================== */

function AssertionFailed(message)
{
  this.message = message;
}

AssertionFailed.prototype = Object.create(Error.prototype);
AssertionFailed.prototype.name = "AssertionFailed";

function assert(test, message)
{
  if(!test)
    throw new AssertionFailed(message);
}
function lastElement(array)
{
  assert(array.length > 0, "Empty array!");
  return array[array.length - 1];
}

log(
  lastElement([])
);
```
