# Regular Expression

[Regular expression - Wikipedia](https://en.wikipedia.org/wiki/Regular_expression)

## Basic concepts

#####  Boolean 'or'

A vertical bar <kbd>|</kbd> separates alternatives.


##### Grouping

parentheses <kbd>(</kbd>, <kbd>)</kbd>are used to define the scope and precedence of the operators.


##### Quantification

| qunatifier           | description                                                                            |
| -------------------- | -------------------------------------------------------------------------------------- |
| <kbd>?</kbd>         | zero or one occurrences of the preceding element.                                      |
| <kbd>*</kbd>         | zere or more occurrences of the preceding element.                                     |
| <kbd>+</kbd>         | one or more occurrences of the preceding element.                                      |
| <kbd>{n}</kbd>       | The preceding item is matched exactly n times.                                         |
| <kbd>{min,}</kbd>    | The preceding item is matched min or more times.                                       |
| <kbd>{,max}</kbd>    | The preceding item is matched up to max times.                                         |
| <kbd>{min,max}</kbd> | The preceding item is matched matched at least min times, but not more than max times. |


##### Wildcard

The wildcard . matches any character


## IEEE POSIX Standard

| Metacharacter    | Description                                                                                                                    | Note     |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------ | -------- |
| <kbd>^</kbd>     | Matches the starting position within the string.                                                                               | BRE      |
| <kbd>.</kbd>     | Matches any single character.                                                                                                  | BRE      |
| <kbd>[ ]</kbd>   | Matches a single character that is contained within the brackets.                                                              | BRE      |
| <kbd>[^ ]</kbd>  | Matches a single character that is not contained within the brackets.                                                          | BRE      |
| <kbd>$</kbd>     | Matches the ending position of the string or the position just before a string-ending newline.                                 | BRE      |
| <kbd>( )</kbd>   | Defines a marked subexpression, also called a capturing group, which is essential for extracting the desired part of the text. | BRE      |
| <kbd>\n</kbd>    | Matches what the *n*th marked subexpression matched, where *n* is a digit from 1 to 9.                                         | BRE only |
| <kbd>*</kbd>     | Matches the preceding element zero or more times.                                                                              | BRE      |
| <kbd>{m,n}</kbd> | Matches the preceding element at least *m* and not more than *n* times.                                                        | BRE      |
| <kbd>?</kbd>     | Matches the preceding element zero or one time.                                                                                | ERE      |
| <kbd>+</kbd>     | Matches the preceding element one or more times.                                                                               | ERE      |
| <kbd>\|</kbd>    | The choice operator matches either the expression before or the expression after the operator.                                 | ERE      |