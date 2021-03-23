# OWEN
OWEN is a config file format that aims to be feature-full while maintaining a focus on accessibility.

Entries are expected to be of the form `KEY=VALUE`.

Blank lines are ignored.

OWEN serializers/deserializers should support [the Unicode specification](http://www.unicode.org/), specifically UTF-16.

## Keys
A key is one or more characters from [a-zA-Z0-9./+\:_-], with optional leading and trailing whitespace. The first character must be an alphabetic character.

## Values
A value is either an [Object](#objects), [Array](#arrays), [Literal](#literals) or [Empty](#empty), with optional leading whitespace.

### Objects
Objects are a collection of `KEY=VALUE` pairs, separated by the newline character. An object is denoted with an open square bracket, `[` and closed with a closed square bracket, `]`. The opening and closing brackets may appear on the same line if there is only whitespace between them. Closing brackets from nested objects or braces from nested arrays may appear on the same line. Such an object is [Empty](#empty). Each `KEY=VALUE` pair should have an entire line to itself. Blank lines in objects are ignored. Comments are allowed inside of objects. See [the examples folder](https://github.com/Haven-King/OWEN/tree/main/examples) for thorough examples.

### Arrays
Arrays are a collection of `VALUE`s, separated by the newline character. An array is denoted with an open curly brace, `{` and closed with a closed curly brace, `}`. The opening and closing braces may appear on the same line if there is only whitespace between them. Closing brackets from nested objects or braces from nested arrays may appear on the same line. Such an array is [Empty](#empty). Each `VALUE` should have an entire line to itself. Blank lines in arrays are ignored. Comments are allowed inside of arrays. See [the examples folder](https://github.com/Haven-King/OWEN/tree/main/examples) for thorough examples.

### Literals
A literal is one or more characters. White space following the value is not ignored, and is treated as part of the value. The characters backslash, newline, carriage return, and tab can be inserted with characters \\, \n, \r, and \t, respectively.

A literal can span several lines if each line is terminated by a backslash (‘\’) character, with whitespace at the beginning of each line ignored. For example:
```
fruits=\
    Mango, \
    Strawberry, \
    Watermelon
```
This is equivalent to
```
fruits=Mango, Strawberry, Watermelon
```

### Empty
Empty is a type-agnostic value used to represent an empty Object, Array, or Literal. It can be represented in code in any of the following ways:
```
empty_value1=[]
empty_value2={}
empty_value3=
```

## Comments
Lines whose first non-whitespace character is a `#` are treated as comments. Parsers can choose to either ignore comments entirely or attach them to the next available entry. Comments at the end of a file or after the last entry in an Object or Array should be discarded.