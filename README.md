learn-regex [Work-in-Progress]
===========

A simple REGular EXpression tutorial in JavaScript

- - -

![Regular Expression XKCD](http://imgs.xkcd.com/comics/regular_expressions.png "RegEx save the day")
http://xkcd.com/208/


I am yet to come across a Regular Expression tutorial for *complete* **beginners**.
So going to try and write one.

## What is a Regular Expression?

A regular expression is a pattern we can search for in text.

- **.** Matches any single character. For example the regular expression **c.t**
would match the strings cat, cut, c t, but not cart or clot 
(because there is more than one character between the **c** and the **t**)

```javascript
var text = "Its raining cats and dogs";
var match = text.match(/c.t/);
console.log(match);
// see: http://repl.it/MYS/1
```



## Background Reading

- Wikipedia Article: http://en.wikipedia.org/wiki/Regular_expression
- Essential Guide: http://coding.smashingmagazine.com/2009/06/01/essential-guide-to-regular-expressions-tools-tutorials-and-resources/
- Basic RegEx Tester: http://regexpal.com/ and http://www.myregextester.com/
- JavaScript RegEx Cheat Sheet: https://www.debuggex.com/cheatsheet/regex/javascript
- Toolbox: http://www.tripwiremagazine.com/2009/08/massive-regular-expressions-toolbox.html

- General Cheat Sheet: http://www.addedbytes.com/cheat-sheets/download/regular-expressions-cheat-sheet-v2.png
- GNU Grep tutorial: http://www.ibm.com/developerworks/aix/library/au-regexp/

### Books

- Text Processing in Python: http://www.amazon.com/exec/obidos/ASIN/0321112547/

### Bad Examples

- Atrocious UI: http://www.regular-expressions.info/javascriptexample.html
- What am I meant to do with this? https://www.debuggex.com/?flavor=javascript
- Text heavy, hard to read: http://www.linuxforums.org/articles/demystifying-regular-expressions_105.html


