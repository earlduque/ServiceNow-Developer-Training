# Regular Expressions
Objective: Learn about regular expressions and how they can be used in ServiceNow

Login to the sandbox with your admin credentials via the side door https://ucdavisietsand.service-now.com/side_door.do

I highly recommend testing created regular expressions in an engine online like https://www.regexpal.com/

## Overview
Regular expressions, or regex for short, are ultimately used to properly define and match a pattern.

Regex can be used in different flavors and vary loosely based on the programming language they are used in. We will be focusing on regex in JavaScript.

## Utilizing Regex

#### Defining a regular expression
A regular expression can be defined by two forward slashes: /regex/. As a an example /john/ searches for a single instance of john in a provided string. The provided regex searches for each individual character and back traces when it does not find a match.

#### Literal characters
In the example of /john/ these are all literal characters and have no special meaning. These include all alphanumeric characters and many others. In the next section we will go over a few metacharacters, which have a special meaning.

#### Basic  Metacharacters
Here I will define some basic metacharacters. *I excluded the forward slashes, / /, that would usually accompany these expressions.*

| Metacharacter | Definition    | Example  |
| :-----------: | :-----------: | :------: |
| . | Wildcard, matches every character except \n | h.t = "hot" & "hit" &"h$t"... |
| \ | Allows literal meaning of metachar | 9\.0 = only "9.0" now|
| \t | Represent a tab character | \thi = "		hi"	|
| /r or /n | is a newline character| hi\n = "hi\n" |
| [] | Is a character set | h[ia]t = "hit" and "hat" |

#### Modes
These expressions can be modified to search to be **global, case-insensitive, multiline, and dot-matches-all** by adding a g, i, m, or s after the second forward slash in the regular expression. For example, /regex/g. 
- Global, g, tells the regex compiler to search for the regex throughout the entire provided string (instead of having it stop after finding 1 instance).
- Case-insensitive, i, makes it so */john/i* would match both "John" and "john"
- Multiline, m, makes the regex compiler treat the text after a new line character, \n, as the beginning of a new string (this will be clearer later).
- Dot-matches-all makes it so the wild character "." matches everything, including new line characters now. 

#### Character set metacharacters
Here I will define commonly used metacharacters in conjunction with character sets

| Metacharacter | Definition    | Example  |
| :-----------: | :-----------: | :------: |
| - | Used to define a range of characters | [a-z] = any *single* char b/w a & z|
| ^ | Negation. Everything not a char set | [^a] = **everything** not a including "0" and "$" |

This next table is going to list shorthands that can be used for common character sets

| Metacharacter | Definition    |
| :-----------: | :-----------: |
| \d | [0-9] |
| \w | [a-zA-Z0-9] |
| \s | [\t\r\n] |
| \D | [^0-9] |
| \W | [^a-zA-Z0-9] |
| \S | [^\t\r\n] |

It's important to note that these can be combined with each other and other literal characters. For example, *[\d\s&]00* will match "300", " 00", and
"&00". It's important to understand that a character set only represents a single character position.

There are also other short hands that can be utilized. Like the POSIX short hand, but these are typically used with older versions of regex. As a result, this shorthand isn't as relevant to people working in JavaScript. If you do use them, it's important to not mix the short hand styles.

#### Repetition
Repetition allows for a character set or literal character to be searched for multiple times. I will begin by defining the repetition metacharacters

| Metacharacter | Definition    | Example  |
| :-----------: | :-----------: | :------: |
| * | Preceding item zero or more times | [\d]* |
| + | Preceding item one or more times| [\d]+ |
| ? | Preceding item zero or one times | [\d]+?1 |
| {min,max} | Preceding item min - max times | [\d]{1,5} |

An example of these is [\d]`*`1 will match with "1", "232331", and "2321321321". Did you notice that the last string had multiple substrings that could be matched with? We will talk about this last example in a moment. The main difference between + and * is that [\d]+1 will not match "1". I encourage you to play with these operators a bit in regexpal. The ? mark operator is used to solve the previously mentioned case.

By nature the +,`*`, and {} operators are all greedy. As a result the [\d]`*` or [\d]+ part of the regex will be preferred over the "1" to end the match. To solve this we use the ? operator. [\d]+?1 will match "2321", "321", "321" when given the string "2321321321". This is particularly useful when searching html files. When searching for tags in a html document using repetition "<em>Hello World</em>" a greedy approach would match the entire string, while we simply want the "<em>" and "</em>". Try using the regex /<.+>/ with "<em>Hello World</em>" and notice how it matches the whole string. To resolve this issue we use the ? operator creating the regular expression, /<.+?>/.

#### Anchors and word boundaries
Anchors and word boundaries are useful to further specify our regex's and improve the efficiency of our searches.

| Metacharacter | Definition    | Example  |
| :-----------: | :-----------: | :------: |
| ^ | Denotes the beginning of a string | ^03[\d]2 |
| $ | Denotes the end of a string | 03[\d]2$ |
| \b | Denotes word boundaries | \bHello\b |

Using the example ^03[\d]2 with the string "0382 0322 0372" would only match "0382", because we specified the start of a string, likewise 03[\d]2$ would match "0372", and ^03[\d]2$ would return neither. Do you remember the multiline mode that could be set for regexs? It is powerful when combined with anchors allowing new line characters, \n, to act as the end of a string and start of a new string. This lets us match our patterns against the beginning or end of multiple lines in a provided string.

Word boundaries can be used to drastically improve the performance of our regexs. This is due to the backtracking nature of the expressions and how utilizing these boundaries simplify the necessary checks. It's important to understand that these boundaries are not space characters themselves but rather the act of switching between alphanumeric characters and others. This is why the first character and last character in the string has a boundary as well. Other common boundaries are created with nonalphanumeric characters, like "group's". I would encourage playing with the regex /\b\w+\b/ and any block of text to best see this.

#### Grouping, backreferences, and alternation
Groups and backreferences are tools commonly used to find repetition in a string and organize our regex.

| Metacharacter | Definition    | Example  |
| :-----------: | :-----------: | :------: |
| () | Defines a group | (<\w+?>) |
| \1-\9 | Accesses a previously created group | (\w+) \1 |
| ?: | Invalidates backreferencing to a group | (?:\w+) |
| `|` | Is an *or* statement | (?:HI)|(?:Hello) |

The example, (\w+) \1,  is an example of backreferencing. Try this regex with "HELLO HELLO" and notice how it will only match if the words separated by a space are the same. This is because we backreferenced the first group and required the following group to be the same in our regex. When using multiple groups they can be backreferenced sequentially with \1, \2, \3, etc. Some languages allow for the usage of more than 9 groups. We also typically want to prevent backreferencing to a group if we don't plan to backreference it in our regex.

Alternation is regex's way of doing *or* statements. The `|` operator does not need to be in a group like the example.

## Regex in ServiceNow
In ServiceNow we will mainly be using regexs for validation. In this example we will create a regex that ensures that the user enters their full name. 

Begin by:
1. Navigate to our Sand Instance of ServiceNow.
2. Create a new catalog item.
3. Now in that catalog item create a new single line text variable.
4. Next create a new on change catalog client script. Make sure the UI Type is all and you select the variable name.

Regex:
In the client script we will begin by creating our regular expression. We want the first characters to be capitalized and the name to be separated by a space. We will declare a new variable and give it a regex.

```
function onChange(control, oldValue, newValue, isLoading) {
	if (isLoading || newValue == '') {
		return;
	}	

	var field = "u_regex"; //This is the name of the variable you created in this catalog item
	var regex = /^[A-Z][a-z]+ [A-Z][a-z]+$/;
	
	if(regex.test(g_form.getValue(field))) {
		g_form.showFieldMsg(field, "Valid", 'info');
	} else {
		g_form.showFieldMsg(field, "Invalid", 'error');
	}
}
```

Here is a rudimentary script using regex. It could be improved in many ways to account for different types of names such as "Ronald McDonald" or people with more than one last name. Feel free to practice by making changes to our regex to account for these cases!

## Conclusion
The goals of this document were to provide you with the tools necessary to begin implementing regexs in ServiceNow. I encourage you to play around with regexs more and think of interesting ways to utilize them.

