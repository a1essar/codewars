Description:

Given the string representations of two integers, return the string representation of the sum of those integers.

For example:

```javascript
sumStrings('1','2') // => '3'
```

A string representation of an integer will contain no characters besides the ten numerals "0" to "9".

Test Cases:

```javascript
function msg(a,b) {
  if(typeof returned !== 'string') {
    return 'Function must return a string value'
  } else {
    return "sumStrings('" + a + "', '" + b + "')"
  }
}
function t(a,b,ans) {
  returned = sumStrings(a,b)
  Test.assertEquals(returned,ans, msg(a,b, returned))
}
t('123', '456', '579')

t('8797', '45', '8842')
t('800', '9567', '10367')
t('99','1','100') 
t('00103', '08567', '8670')
t('','5','5')
t('712569312664357328695151392',
       '8100824045303269669937',
  '712577413488402631964821329')
t('50095301248058391139327916261',
  '81055900096023504197206408605',
  '131151201344081895336534324866')
```

My solution:
```javascript
function sumStrings(a,b) {
  return a >= 9007199254740992 - 1 || b >= 9007199254740992 - 1 ? bigInt(a,b) : (a*1 + b*1) + '';
}

function bigInt(a,b){
  var c = '';
  var d = 0;
  
  var zero = new Array((Math.abs(a.length - b.length))+1).join('0')
  
  a.length >= b.length ? b = zero + b : a = zero + a;
  
  for(var i = b.length-1; i >= 0; i--){
   var sum = (a[i]*1 + b[i]*1) + d;
   if(sum >= 10){
    sum = sum - 10;
    d = 1;
   }else{
    d = 0;
   }
   c = sum + c;
  }
  
  return d > 0 ? d + c : c;
}
```