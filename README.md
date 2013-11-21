learn-regex [Work-in-Progress]
===========

A simple REGular EXpression tutorial in JavaScript

- - -

![Regular Expression XKCD](http://imgs.xkcd.com/comics/regular_expressions.png "RegEx save the day")

<sup>http://xkcd.com/208/</sup>

If you have ever *wondered* how **search** works, 
its all about *finding* ***patterns***.
While a *search engine* will have many sophisticated 
[search algorithms](http://en.wikipedia.org/wiki/Search_algorithm) at their
*core* are searches for patterns in text.


I am yet to find a Regular Expression tutorial for ***complete beginners***.
So I'm writing one! 
**Note**: this tutorial is *specific* to **JavaScript**.





## What is a Regular Expression?

A regular expression is a pattern we can search for in text.


## Searching for Character(s) in a Block of Text

### Basic Symbols

At the most *basic* level we need `/pattern/g`
two forward slashes to show the **beginning** and **end** 
of the pattern we are searching for.
For example the regular expression **/th/**
will find all occurences of **th** within a block of text.

```javascript
var text = "The cat with the hat sat on the mat."
var pattern = /th/gi;
var match, matches = [];
while ( (match = pattern.exec(text)) ) {
    matches.push(match.index);
}
console.log(indices); // >> [ 0, 10, 13, 28 ]
```
Try: http://repl.it/MYU


**.** (*period*) Matches **any single character**. 
For example the regular expression **c.t**
would match the strings cat, cut, c t, but not cart or clot 
(because there is more than one character between the **c** and the **t**)

```javascript
var text = "Its raining cats and dogs";
var pattern = /c.t$/;
var match = text.match(pattern);
console.log(match.index);       // >> 12
```
Try: http://repl.it/MYS/1


**^** (*caret* or "*circumflex*") Matches the **beginning** of a line. 
For example, the regular expression ^Once will match the beginning of 
"Once upon a time" but would not match "I only saw her cry once..."

```javascript
var text = "wake up its a beautiful morning!";
var pattern = /^wake/;
var match = text.match(pattern);
console.log(match.index);       // >> 0 

var text = "I'm wide awake";
var pattern = /^wake/;
var match = text.match(pattern);
console.log(match);             // >> null
```
Try: http://repl.it/MYS/3


**$** (*dollar*) Matches the **end** of a line. 
The pattern: **away$** would match the end of the string 
"I need to get **away**" but not the string "Up Up and away!" 
(because the away pattern is not at the *end* of the text/string/line) 

```javascript
var text = "this is the end";
var pattern = /end$/;
var match = text.match(pattern);
console.log(match.index);       // >> 12

var text = "is this the end?";
var pattern = /end$/;
var match = text.match(pattern);
console.log(match);             // >> null
```
Try: http://repl.it/MYS/2


* (*asterisk*) Matches zero or more occurences of the character 
immediately preceding. .* means match any number of any characters.
This is a bit of a useless example because it will always return a
match for strings with any number of characters (greater than zero!)

>> need a better example for asterisk! 

```javascript
var text = "A horse! a horse! my kingdom for a horse!";
var pattern = /end$/;
var match = text.match(pattern);
console.log(match.index);       // >> 12

var text = "is this the end?";
var pattern = /end$/;
var match = text.match(pattern);
console.log(match);             // >> null
```
Try: http://repl.it/MYS/2


**\ ** (*backslash*) The quoting/escaping character, 
use it to treat the next character as an ordinary character. 
For example: \$ is used to match the dollar sign ($) 
rather than the end of a line. Similarly, the expression \. is used to match 
the period character rather than any single character. 


```javascript
var text = "My Raspberry Pi Cost $45!";
var pattern = /\$/;
var match = text.match(pattern);
console.log(match.index);       // >> 21

var text = "Is this the end...?"
var pattern = /\./g;
var match, matches = [];
while ( (match = pattern.exec(text)) ) {
    matches.push(match.index);
}
console.log(matches); // >> [ 15, 16, 17 ]
```
Try: http://repl.it/MYY


**[ ]** (square brackets) Matches any one of the characters between 
the brackets For example, the regular expression **r[aou]t** 
matches **rat**, **rot**, and **rut**, but ***not ret***.

```javascript
var text = "The caged rat felt stuck in a rut.";
var pattern = /r[aou]t/g;
var match, matches = [];
while ( (match = pattern.exec(text)) ) {
    matches.push(match.index);
}
console.log(matches); // >> [ 10, 30 ]
```
Try: http://repl.it/MY2


An example of a **range** of characters we want to look for is: **[0-9]**
[0-9] means find any digit.

```javascript
var text = "The 49ers are an American football team based in San Francisco, California";
var pattern = /[0-9]/;
var match = text.match(pattern);
console.log(match.index);       // >> 4
```
Try: http://repl.it/MY2/1

We can find ***all*** the **numbers** *recursively* in a block of text:

```javascript
var text = "2486 runners started the race but only 1865 finished!";
var pattern = /[0-9]/g;
var match, matches = [];
while ( (match = pattern.exec(text)) ) {
    matches.push(match.index);
}
console.log(matches); // >> [ 0, 1, 2, 3, 39, 40, 41, 42 ]
```
Try: http://repl.it/MY4


**|** (*verticle bar* or "*pipe*") Allows us to serach for two conditions 
together. For example (him|her) matches the line "it belongs to him" and 
matches the line "it belongs to her" but does not match the line "it belongs 
to them."

```javascript
var text = "2486 runners started the race but only 1865 finished!";
var pattern = /[0-9]/g;
var match, matches = [];
while ( (match = pattern.exec(text)) ) {
    matches.push(match.index);
}
console.log(matches); // >> [ 0, 1, 2, 3, 39, 40, 41, 42 ]
```



>> Moar: http://linuxreviews.org/beginner/tao_of_regular_expressions/


## Background 

### Reading

- Wikipedia Article: http://en.wikipedia.org/wiki/Regular_expression
- Essential Guide: http://coding.smashingmagazine.com/2009/06/01/essential-guide-to-regular-expressions-tools-tutorials-and-resources/
- Basic RegEx Tester: http://regexpal.com/ and http://www.myregextester.com/
- JavaScript RegEx Cheat Sheet: https://www.debuggex.com/cheatsheet/regex/javascript
- Toolbox: http://www.tripwiremagazine.com/2009/08/massive-regular-expressions-toolbox.html

- General Cheat Sheet: http://www.addedbytes.com/cheat-sheets/download/regular-expressions-cheat-sheet-v2.png
- GNU Grep tutorial: http://www.ibm.com/developerworks/aix/library/au-regexp/
- TAO: http://linuxreviews.org/beginner/tao_of_regular_expressions/

### Video

- Good video by ***Lea Verou***: http://youtu.be/EkluES9Rvak 
+ interactive tutorial: http://leaverou.github.io/regexplained/

### Books

- Regular Expressions Cookbook: http://www.amazon.com/Regular-Expressions-Cookbook-Jan-Goyvaerts/dp/1449319432/
- Mastering Regular Expressions: http://www.amazon.co.uk/Mastering-Regular-Expressions-Powerful-Techniques/dp/1565922573/
- Text Processing in Python: http://www.amazon.com/exec/obidos/ASIN/0321112547/

### Bad Examples

- Atrocious UI: http://www.regular-expressions.info/javascriptexample.html
- What am I meant to do with this? https://www.debuggex.com/?flavor=javascript
- Text heavy, hard to read: http://www.linuxforums.org/articles/demystifying-regular-expressions_105.html


