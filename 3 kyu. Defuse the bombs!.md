https://www.codewars.com/kata/54d558c72a5e542c0600060f

###Description:
There are a series of 10 bombs about to go off! Defuse them all! Simple, right?

Note: This is not an ordinary Kata, but more of a series of puzzles. The point is to figure out what you are supposed to do, then how to do it. Instructions are intentionally left vague.

###Test Cases:
```javascript
Test.assertEquals( Object.isFrozen(Bomb)||Object.isSealed(Bomb)||!Object.isExtensible(Bomb), false, 'The bomb refuses to be frozen and blew up anyway');
Test.assertEquals( Bomb.theBombsAreAllDiffused, true, 'Boom!');
```

###My solution:
```javascript
// Defuse all of the Bombs!
Bomb.diffuse(Bomb.key);
Bomb.diffuse(Bomb.key);
Bomb.diffuse(Bomb.key);
Bomb.diffuse(Bomb.key);
Bomb.diffuse(Bomb.key);
Bomb.diffuse(Bomb.key);

Bomb.diffuse(global.BombKey);

var diffuseTheBomb = () => true;
Bomb.diffuse();

Bomb.diffuse(Math.PI.toFixed(5));

Bomb.diffuse(new Date().setFullYear( new Date().getFullYear() - 4 ));

Bomb.diffuse(Object.freeze({key: 43}));

Bomb.diffuse(obj = {
  i: 0,
  valueOf: function() {
    let res = this.i > 0 ? 11 : 9
    this.i++;
    return res;
  }
});

Math = new Proxy({random: (function() {
  let index = 0;
  
  return () => {
    index++;
    return index === 3 ? 0.5 : 1;
  };
})()}, function() {});

Bomb.diffuse(42);

Array.prototype.valueOf = () => 14;
Bomb.diffuse('eWVz')
```
