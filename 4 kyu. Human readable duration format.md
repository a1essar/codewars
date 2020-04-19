
https://www.codewars.com/kata/52742f58faf5485cae000b9a/

### Description:

Your task in order to complete this Kata is to write a function which formats a duration, given as a number of seconds, in a human-friendly way.

The function must accept a non-negative integer. If it is zero, it just returns "now". Otherwise, the duration is expressed as a combination of years, days, hours, minutes and seconds.

It is much easier to understand with an example:

```
formatDuration(62)    // returns "1 minute and 2 seconds"
formatDuration(3662)  // returns "1 hour, 1 minute and 2 seconds"
For the purpose of this Kata, a year is 365 days and a day is 24 hours.
```

Note that spaces are important.

Detailed rules
The resulting expression is made of components like 4 seconds, 1 year, etc. In general, a positive integer and one of the valid units of time, separated by a space. The unit of time is used in plural if the integer is greater than 1.

The components are separated by a comma and a space (", "). Except the last component, which is separated by " and ", just like it would be written in English.

A more significant units of time will occur before than a least significant one. Therefore, 1 second and 1 year is not correct, but 1 year and 1 second is.

Different components have different unit of times. So there is not repeated units like in 5 seconds and 1 second.

A component will not appear at all if its value happens to be zero. Hence, 1 minute and 0 seconds is not valid, but it should be just 1 minute.

A unit of time must be used "as much as possible". It means that the function should not return 61 seconds, but 1 minute and 1 second instead. Formally, the duration specified by of a component must not be greater than any valid more significant unit of time.

### Test Cases:

```javascript
describe("basic tests", () => {
  Test.assertEquals(formatDuration(0), "now");
  
  Test.assertEquals(formatDuration(1), "1 second");
  Test.assertEquals(formatDuration(62), "1 minute and 2 seconds");
  Test.assertEquals(formatDuration(120), "2 minutes");
  Test.assertEquals(formatDuration(3600), "1 hour");
  Test.assertEquals(formatDuration(3662), "1 hour, 1 minute and 2 seconds");
  
  Test.assertEquals(formatDuration(15731080), "182 days, 1 hour, 44 minutes and 40 seconds");
  Test.assertEquals(formatDuration(132030240), "4 years, 68 days, 3 hours and 4 minutes");
  Test.assertEquals(formatDuration(205851834), "6 years, 192 days, 13 hours, 3 minutes and 54 seconds");
  Test.assertEquals(formatDuration(253374061), "8 years, 12 days, 13 hours, 41 minutes and 1 second");
  Test.assertEquals(formatDuration(242062374), "7 years, 246 days, 15 hours, 32 minutes and 54 seconds");
  Test.assertEquals(formatDuration(101956166), "3 years, 85 days, 1 hour, 9 minutes and 26 seconds");
  Test.assertEquals(formatDuration(33243586), "1 year, 19 days, 18 hours, 19 minutes and 46 seconds");
});

describe("random tests", () => {
  function sol(seconds) {
    if (seconds == 0) return 'now';
    function formatComponents(x) {
      var firsts = x.slice(0, -1).join(', ');
      return (firsts && firsts + ' and ') + x[x.length - 1];
    }
  
    var components = ["year", "day", "hour", "minute", "second"];
    var times = [31536000, 86400, 3600, 60, 1];
  
    return formatComponents(
      times.map((secondsByUnit, i) => {
        var value = (seconds / secondsByUnit) | 0;
        seconds %= secondsByUnit;
        return value == 0 ? '' : value + ' ' + components[i] + (value > 1 ? 's' : '');
      }).filter(Boolean));
  }
  for (let i = 0; i < 100; i++) {
    const n = Math.floor(Math.random() * 10000000);
    Test.assertEquals(formatDuration(n), sol(n));
  }
});
```

### My solution:

```javascript
function formatDuration (seconds) {
  let output = '';
  let values = [];
  let lastValue = '';
  
  if (seconds <= 0) {
    return 'now';
  }
  
  formatDuration.units.forEach((unit) => {
    let number = Math.floor(seconds / unit.number);
    
    if (number >= 1) {
      values.push(number + ' ' + formatDuration.getPlural(number, unit.title));
      seconds -= number * unit.number
    }
  });
  
  if (values.length > 1) {
    lastValue = values.pop();
  }
  
  output = values.join(formatDuration.separates[0]);
  
  if (lastValue) {
    output += formatDuration.separates[1] + lastValue;
  }
  
  return output;
}

formatDuration.getPlural = (number, title) => (number !== 1) ? title + 's' : title;

formatDuration.SECOND = 1;
formatDuration.MINUTE = 60 * formatDuration.SECOND;
formatDuration.HOUR = 60 * formatDuration.MINUTE;
formatDuration.DAY = 24 * formatDuration.HOUR;
formatDuration.YEAR = 365 * formatDuration.DAY;

formatDuration.units = [
  {title: 'year', number: formatDuration.YEAR},
  {title: 'day', number: formatDuration.DAY},
  {title: 'hour', number: formatDuration.HOUR},
  {title: 'minute', number: formatDuration.MINUTE},
  {title: 'second', number: formatDuration.SECOND},
]

formatDuration.separates = [', ', ' and '];

```
