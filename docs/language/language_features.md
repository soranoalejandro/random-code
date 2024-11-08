# Language features
+ Objects
## Syntax
+ comments \#
+ lowercase id
+ number
+ string ' or " or `
## Supported operations
+ consume operator !, for consuming strings, array or buffer types

## Data types
+ object, number, float, string, buffer

## Automatic conversions
Support specifying a default value for when automatic conversion assignment fails.
|Targets|Detail|
|----|----|
|number -> string|can specify padding and format in an explicit call|
|string -> number|autodetect base or set explicitly with validation|

#### String to number
```python
x = 34
x = "23"          # 23
x = "Pear", 20    # as "Pear" can't be parsed, 20 will be used
```
#### Number to string
```python
text = ""
x = 27

text = x                # "27"
text = x.string(4)      # "0027", padding 4, decimal assumed
text = x.string(8, 2)   # "00001011", padding 8, base 2
text = x.string(4, 16)  # "001B", padding 4, base 16
```

## Exclude
Things that will be strived against:
+ use of math operators for strings or non-numerical types
+ use of math operators for starting a comment, or other tokens (//, /*)
+ use of operators for esoteric functions
(on this note, a set of keywords for operating on vectors may be considered as an alternative to 'dumb' operator overloading)

## Array access
Looping trough arrays in a for loop will have the following syntax, allowing nested levels to be accessed after a comma, can be used with nested properties of objects too.

`array = [12, 13, 14]`

```python
for array, item {

  # item will have the values 12, 13, 14
  item = 25

  # on each iteration, we replace the value for 25
  # the array will be [25, 25, 25] after the loop
}
```

Nested arrays can be accessed by adding more element names after the comma.

`colors = [ [40, 73, 116], [255, 180, 24], [120, 133, 143] ]`
```python
for colors, color, channel {
  # this will access each value in the array
  # for example for brightness correction to all channels 
  channel = channel * 0.25
}
```
If we want to get the current color and all its channels, the color variable will hold the current [ , , ] values for the current iteration.

### More multilevel cases:
On the colors example, we can define code that will be processed for each level, and even introduce new variables for the lower levels.
```python
for colors, color, channel {
  color:
  average = color[0] + color[1] + color[2] ) / 3
  #this will be done once for each color

  channel:
  channel = (color + average) / 2
  #this will be done for all the channels as before
}
```
The idea is to avoid nesting indentation. This representation replaces two `for` loops, and more levels can be added without adding more indentation.

### Notes on the array access syntax
There is redundancy, the level names are written twice when declaring the code blocks for the multilevel access case.
This can be evaluated further or be left as is.

Filters can be added to the syntax for the code block declarations.

This does not replace the traditional loop nesting case when there is processing at the beginning and 'after' each intermediate level. But. It can be solved be adding and 'after' tag or syntax to the current implementation? Will be worth considering.

Additionally, adding an 'after' vs just repeating the code level name leads to one situation where the order of the blocks declaration is important, and another where the order is not important.
