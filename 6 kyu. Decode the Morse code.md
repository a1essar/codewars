https://www.codewars.com/kata/54b724efac3d5402db00065e

### Description:

Part of Series 1/3
This kata is part of a series on the Morse code. After you solve this kata, you may move to the next one.

In this kata you have to write a simple Morse code decoder. While the Morse code is now mostly superseded by voice and digital data communication channels, it still has its use in some applications around the world.
The Morse code encodes every character as a sequence of "dots" and "dashes". For example, the letter A is coded as ·−, letter Q is coded as −−·−, and digit 1 is coded as ·−−−−. The Morse code is case-insensitive, traditionally capital letters are used. When the message is written in Morse code, a single space is used to separate the character codes and 3 spaces are used to separate words. For example, the message HEY JUDE in Morse code is ···· · −·−−   ·−−− ··− −·· ·.

NOTE: Extra spaces before or after the code have no meaning and should be ignored.

In addition to letters, digits and some punctuation, there are some special service codes, the most notorious of those is the international distress signal SOS (that was first issued by Titanic), that is coded as ···−−−···. These special codes are treated as single special characters, and usually are transmitted as separate words.

Your task is to implement a function that would take the morse code as input and return a decoded human-readable string.

For example:

decodeMorse('.... . -.--   .--- ..- -.. .')
//should return "HEY JUDE"
NOTE: For coding purposes you have to use ASCII characters . and -, not Unicode characters.

The Morse code table is preloaded for you as a dictionary, feel free to use it

### Test Cases:

```javascript
Test.describe("Example from description", function(){
  testAndPrint(decodeMorse('.... . -.--   .--- ..- -.. .'), 'HEY JUDE')
});

Test.describe("Basic Morse decoding", function(){
  testAndPrint(decodeMorse('.-'), 'A')
  testAndPrint(decodeMorse('.'), 'E')
  testAndPrint(decodeMorse('..'), 'I')
  testAndPrint(decodeMorse('. .'), 'EE')
  testAndPrint(decodeMorse('.   .'), 'E E')
  testAndPrint(decodeMorse('...---...'), 'SOS')
  testAndPrint(decodeMorse('... --- ...'), 'SOS')
  testAndPrint(decodeMorse('...   ---   ...'), 'S O S')
});

Test.describe("More complex tests", function(){
  testAndPrint(decodeMorse(' . '), 'E')
  testAndPrint(decodeMorse('   .   . '), 'E E')
  testAndPrint(decodeMorse('      ...---... -.-.--   - .... .   --.- ..- .. -.-. -.-   -... .-. --- .-- -.   ..-. --- -..-   .--- ..- -- .--. ...   --- ...- . .-.   - .... .   .-.. .- --.. -.--   -.. --- --. .-.-.-  '), 'SOS! THE QUICK BROWN FOX JUMPS OVER THE LAZY DOG.')
});
```

### My solution:

```javascript
decodeMorse = function(morseCode){
  const wordsMap = morseCode.split(' '.repeat(3)).map(words => words.split(' '));
  const decodeChars = char => MORSE_CODE[char];
  const decodeWords = words => words.map(decodeChars).join('');
  const decodedString = wordsMap.map(decodeWords).join(' ').trim();
  
  return decodedString;
}
```
