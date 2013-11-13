learn-regex [Work-in-Progress]
===========

A simple REGular EXpression tutorial in JavaScript

- - -

I am yet to come across a Regular Expression tutorial for *complete* **beginners**.
So going to try and write one. 

![Regular Expression XKCD](http://imgs.xkcd.com/comics/regular_expressions.png "RegEx save the day")
http://xkcd.com/208/


## What is a Regular Expression?

A regular expression is a pattern we can search for in text.



### Basic Symbols

**.** (*period*) Matches **any single character**. 
For example the regular expression **c.t**
would match the strings cat, cut, c t, but not cart or clot 
(because there is more than one character between the **c** and the **t**)

```javascript
var text = "Its raining cats and dogs";
var pattern = /c.t$/;
var match = text.match(pattern);
console.log(match.index);       // >> 12
// see: http://repl.it/MYS/1
```

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

// see: http://repl.it/MYS/3
```

**$** (*dollar*) Matches the **end** of a line. 
For example, the regular expression away$ would match the end of the string 
"I need to get away" but not the string "Up Up and away!" 
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

// see: http://repl.it/MYS/2
```






## Background Reading

- Wikipedia Article: http://en.wikipedia.org/wiki/Regular_expression
- Essential Guide: http://coding.smashingmagazine.com/2009/06/01/essential-guide-to-regular-expressions-tools-tutorials-and-resources/
- Basic RegEx Tester: http://regexpal.com/ and http://www.myregextester.com/
- JavaScript RegEx Cheat Sheet: https://www.debuggex.com/cheatsheet/regex/javascript
- Toolbox: http://www.tripwiremagazine.com/2009/08/massive-regular-expressions-toolbox.html

- General Cheat Sheet: http://www.addedbytes.com/cheat-sheets/download/regular-expressions-cheat-sheet-v2.png
- GNU Grep tutorial: http://www.ibm.com/developerworks/aix/library/au-regexp/
- TAO: http://linuxreviews.org/beginner/tao_of_regular_expressions/

### Books

- Text Processing in Python: http://www.amazon.com/exec/obidos/ASIN/0321112547/

### Bad Examples

- Atrocious UI: http://www.regular-expressions.info/javascriptexample.html
- What am I meant to do with this? https://www.debuggex.com/?flavor=javascript
- Text heavy, hard to read: http://www.linuxforums.org/articles/demystifying-regular-expressions_105.html


