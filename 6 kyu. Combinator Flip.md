###Description:

Create a combinator function named flip that takes a function as an argument and returns that function with it's arguments reversed.

For example:

```javascript
flip(print)(4,5) // returns "5 -> 4"

function print(a,b) {
  return a + " -> " + b;
}
```

###Test Cases:

```javascript
flip(print)(4,5) // returns "5 -> 4"

function print(a,b) {
  return a + " -> " + b;
}
```

###My solution:

```javascript
function flip(fn) {
  return function(){
    return fn.apply(null, Array.prototype.slice.call(arguments).reverse());
  }
}

function print(a,b) {
   return a + " -> " + b;
}
```