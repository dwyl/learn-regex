learn-regex [Work-in-Progress]
===========

A simple REGular EXpression tutorial in JavaScript

![Regular Expression XKCD](http://imgs.xkcd.com/comics/regular_expressions.png "RegEx save the day")
<sup>http://xkcd.com/208/</sup>

If you have ever *wondered* how **search** works, 
its all about *finding* ***patterns***. <br />
While a *search engine* will have sophisticated 
[search algorithms](http://en.wikipedia.org/wiki/Search_algorithm) at their
*core* are searches for patterns in text.


I am yet to find a Regular Expression tutorial for ***complete beginners***.
So I'm *writing* one! <br />
**Note**: this tutorial is *specific* to **JavaScript**.





## What is a Regular Expression?

A regular expression is a pattern we search for in text.

Imagine you want to check if an email address is well correct when someone
is filling in a form.
One way of doing this would be to try *sending* an email to the address and
waiting for a reply or "[bounce](http://en.wikipedia.org/wiki/Bounce_message)" 
(error)...
(*obviously* this is a *terrible* idea! sending email is time consuming)
A far more efficient way of checking email validity is to use a regular
expression that will tell us in a milisecond 
if the email matches a valid pattern.



![email regex](http://i.imgur.com/7rV4c56.jpg "email regex")


## Searching for Character(s) in a Block of Text

There are **30** bits of knowledge you need to grasp in order to use
regular expressions effectively. Each one will only take a minute to learn.

### Basic Symbols

At the most *basic* level we need `/pattern/flags`
two forward slashes to show the **beginning** and **end** 
of the pattern we are searching for and after the last forward slash we have 
(optional) "**flags**" indicate *how* to search
(see below for the other available flags).

For example the regular expression **/th/g**
will find **all** occurences of **th** within a block of text.
(the **g** flag means "global" match - i.e. *find all*)

```javascript
var text = "The cat with the hat sat on the mat."
var pattern = /th/gi;
var match, matches = [];
while ( (match = pattern.exec(text)) ) {
    matches.push(match.index);
}
console.log(matches); // >> [ 0, 10, 13, 28 ]
```
Try: https://repl.it/MYU/2


**.** (*period*) Matches **any single character**. 
For example the regular expression **c.t**
would match the strings cat, cut, c t, but not cart or clot 
(because there is more than one character between the **c** and the **t**)

```javascript
var text = "Its raining cats and dogs";
var pattern = /c.t/;
var match = text.match(pattern);
console.log(match.index);       // >> 12
```
Try: https://repl.it/MYS/1


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
Try: https://repl.it/MYS/3


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
Try: https://repl.it/MYS/2


__*__ (*asterisk*) Matches zero or more occurences of the character 
immediately preceding. ma* means match any occurance of the characters
**ma** followed by any other character so it will find **ma**tt or **ma**rmite
but ignore **mom** because it does not contain **ma**.

```javascript
var text = "The matrix is all around us...";
var pattern = /ma*/;
var match = text.match(pattern);
console.log(match.index); // >> 4
```
Try: https://repl.it/MbE


__\\__ (*backslash*) The quoting/escaping character, 
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
Try: https://repl.it/MYY


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
Try: https://repl.it/MY2


An example of a **range** of characters we want to look for is: **[0-9]**
this means means find any digit (its *much* easier than writing [0123456789])

```javascript
var text = "The 49ers are an American football team based in San Francisco, California";
var pattern = /[0-9]/;
var match = text.match(pattern);
console.log(match.index);       // >> 4

var text = "The 49ers are an American football team based in San Francisco, California";
var pattern = /[0123456789]/;
var match = text.match(pattern);
console.log(match.index);       // >> 4
```
Try: https://repl.it/MbG

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
Try: https://repl.it/MY4


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

### Flags Tell us *How* to Search

Flags are placed at the end of the pattern (after the last forward slash)
and tell the regular expression parser *how* we want to search.

- **g** : "***global*** *search*" or "*find* ***all*** *occurences*"
- **i** : "*case* ***insensitive***" so find *both* **CAT** *and* **cat**
- **m** : "***multiline***" will match your pattern over **multiple lines**

### Special Characters

**\d** Matches a digit character in the basic Latin alphabet. Equivalent to **[0-9]**

**\D** Matches any character that is not a digit in the basic 
Latin alphabet. Equivalent to **[^0-9]**


>> Moar: http://linuxreviews.org/beginner/tao_of_regular_expressions/


## Background 

### Reading

- Wikipedia Article: http://en.wikipedia.org/wiki/Regular_expression
- Essential Guide: http://coding.smashingmagazine.com/2009/06/01/essential-guide-to-regular-expressions-tools-tutorials-and-resources/
- Basic RegEx Tester: http://regexpal.com/ and http://www.myregextester.com/
- JavaScript RegEx Cheat Sheet: https://www.debuggex.com/cheatsheet/regex/javascript
- Toolbox: http://www.tripwiremagazine.com/2009/08/massive-regular-expressions-toolbox.html
- **Mozilla** Dev article: **https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp**

- General Cheat Sheet: http://www.addedbytes.com/cheat-sheets/download/regular-expressions-cheat-sheet-v2.png
- GNU Grep tutorial: http://www.ibm.com/developerworks/aix/library/au-regexp/
- TAO: http://linuxreviews.org/beginner/tao_of_regular_expressions/
- Overcomplicated but useful examples: http://www.tripwiremagazine.com/2009/08/massive-regular-expressions-toolbox.html

### Video

- Good video by ***Lea Verou***: http://youtu.be/EkluES9Rvak 
+ interactive tutorial: http://leaverou.github.io/regexplained/

### Books

- Introduction to Regular Expressions: https://launchschool.com/books/regex
- Regular Expressions Cookbook: http://www.amazon.com/Regular-Expressions-Cookbook-Jan-Goyvaerts/dp/1449319432/
- Mastering Regular Expressions: http://www.amazon.co.uk/Mastering-Regular-Expressions-Powerful-Techniques/dp/1565922573/
- Text Processing in Python: http://www.amazon.com/exec/obidos/ASIN/0321112547/

### Bad Examples

- Atrocious UI: http://www.regular-expressions.info/javascriptexample.html
- What am I meant to do with this? https://www.debuggex.com/?flavor=javascript
- Text heavy, hard to read: http://www.linuxforums.org/articles/demystifying-regular-expressions_105.html


