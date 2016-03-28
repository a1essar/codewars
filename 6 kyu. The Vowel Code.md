###Description:

Step 1: Create a function called encode() to replace all the lowercase vowels in a given string with numbers according to the following pattern:

a -> 1

e -> 2

i -> 3

o -> 4

u -> 5

For example, encode("hello") would return "h2ll4" There is no need to worry about uppercase vowels in this kata.

Step 2: Now create a function called decode() to turn the numbers back into vowels according to the same pattern shown above.

For example, decode("h3 th2r2") would return "hi there"

For the sake of simplicity, you can assume that any numbers passed into the function will correspond to vowels.

###Test Cases:

```javascript
Test.expect(encode('hello') == 'h2ll4', 'encode failed. Your result: '+encode('hello')+' Expected result: h2ll4');
Test.expect(encode('How are you today?') == 'H4w 1r2 y45 t4d1y?', 'encode did not work properly');

Test.expect(encode('This is an encoding test.') == 'Th3s 3s 1n 2nc4d3ng t2st.', 'encode did not work properly');

Test.expect(decode('h2ll4') == 'hello', 'decode did not work properly');

Test.expect(decode(encode('hello')) == 'hello', 'decode(encode) did not work properly');
```

###My solution:

```javascript
// turn vowels into numbers
var vowelsSymbols = ['a', 'e', 'i', 'o', 'u'];
var vowelsIndexes = ['1', '2', '3', '4', '5'];

function encode(string){
  var a = string.split('');
  a.map(function(el, i){
    if(vowelIndex = vowelsSymbols.indexOf(el), vowelIndex >= 0){
      a[i] = vowelsIndexes[vowelIndex];
    }
  });
  
  return a.join('');
}

//turn numbers back into vowels
function decode(string){
  var a = string.split('');
  a.map(function(el, i){
    if(vowelIndex = vowelsIndexes.indexOf(el), vowelIndex >= 0){
      a[i] = vowelsSymbols[vowelIndex];
    }
  });
  
  return a.join('');
}
```