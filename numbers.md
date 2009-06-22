---
title: Numbers
layout: default
---

## Neko Numbers

Numbers in Neko may be integers (whole numbers) or floats. Integers are 31-bits, so they have a range from -1073741824 to 1073741823. Floats are stored as 64-bit doubles. There is also a library provided for manipulating 32-bit integers [here](http://nekovm.org/doc/view/int32).

## Number Operations

The following operations can be performed with any two numbers:

+ `-` - Subtraction
+ `+` - Addition
+ `/` - Division
+ `*` - Multiplication
+ `%` - Modulo

Note that division of two integers may return a float.

## Integer Operations

The following operations can only be used with integers:

+ `<<` - Left bit shift
+ `>>` - Right bit shift
+ `>>>` - Right unsigned bit shift
+ `|` - Perform bitwise or
+ `&` - Perform bitwise and
+ `^` - Perform bitwise xor

## Integer Functions

The following functions can be used with integers and are more efficient than the operators above:

+ `$iadd` - Add two integers
+ `$isub` - Subtract two integers
+ `$idiv` - Divides two integers using integer divison. Raises error for division by zero
+ `$imult` - Multiplies two integers

## Number Conversions

+ `$int` - Converts any value to an integer or `null` if it cannot
+ `$float` - Converts any value to a float or `null` if it cannot

## Number Checks

+ `$isnan` - Returns true if the value given is the float value of NaN
+ `$isinfinite` - Returns true if the value given is the float value of infinity

## Integer Overflow

Neko does not deal with integer overflow. Positive overflow will result in the value of -1, negative overflow results in 1. Keep in mind the range for integers given above.
