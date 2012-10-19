#Except - Boolean Subtraction and Finite Boolean Algebra

##Notes

This is a work in progress and is public available in its incomplete form.
Feedback is welcome.

##Introduction

In binary number systems, only two states are allowed: 0 and 1.
Other ways to describe these states are
- on, off
- true, false
- yes, no

A single binary number changing over time is called a "bitstream".
Reading from left to right, a bitstream can look like the following:

    00000111110101000100101010100111110100010101010010011111100000

This is called a "raw bitstream".
Because this form is a bit hard to read, using '_" for 0 and '-' for 1 is used:

    _____-----_-_-___-__-_-_-_-__-----_-___-_-_-_-__-__------_____

Also, this can be represented as a list of indices where the values change:

    {5,10,11,12,13,14,17,18,20,21,22,23,24,25,26,27,29,34,35,36,39,40,41,42,43,44,45,46,48,49,51,57}

This is called a "group bitstream".
Every even index is '_-' (up) and every odd index is '-_' (down).

A raw bitstream is always discrete, but a group bitstream can be continious.
Writing {3.5,7.8} is allowed, but can not be translated directly to raw bitstream.
One must multiply each number with a factor to make all entries an integer.
This works only for rational numbers, not for irrational.

##Logical Gates

In binary logic, a "gate" is an operation on one or more bitstreams.
A gate can be represented with a truth table:

    OR
    0 0 => 0
    0 1 => 1
    1 0 => 1
    1 1 => 1

    AND
    0 0 => 0
    0 1 => 0
    1 0 => 0
    1 1 => 1

    NOT
    0 => 1
    1 => 0

    XOR
    0 0 => 0
    0 1 => 1
    1 0 => 1
    1 1 => 0

