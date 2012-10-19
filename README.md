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

    OR ( A + B )
    0 0 => 0
    0 1 => 1
    1 0 => 1
    1 1 => 1

    AND ( A · B )
    0 0 => 0
    0 1 => 0
    1 0 => 0
    1 1 => 1

    NOT ( !A )
    0 => 1
    1 => 0

    XOR ( A x B )
    0 0 => 0
    0 1 => 1
    1 0 => 1
    1 1 => 0

Often we use symbols similar to basic arithmetic.
Beside the name of each gate I have put the symbols used in this paper.

Boolean Subtraction has the following gate:

    EXCEPT ( A - B )
    0 0 => 0
    0 1 => 0
    1 0 => 1
    1 1 => 0
    
The output from this gate depends on the order of the inputs.

Gates operates on bitstreams that change over time.
The output from a gate is also another bitstream.
It can be described as function:

    result = function( input0, input1, ... ) where type( result ) and type( input ) is bitstream.

When a function returns the same type as input, we call it "complete".
Some authors suggests that Boolean Algebra is not subtraction-complete [A].
The motivation is that it would require the existense of negative bits:

    a - b = a + (-b) 

The error done here is assuming that the non-existence of negative bits is preventing Boolean Subtraction.
Instead, the non-existence of negative bits can be used to show how this gives well defined output.

    0 - 0 = 0 + (-0) = 0
    0 - 1 = 0 + (-1) = constant, but not 1
    1 - 0 = 1 + (-0) = 1
    1 - 1 = 1 + (-1) = constant, but not 1
    
In the cases of negative bits, the output of the gate is a constant, but not 1.
We can create an axiom that this constant is 0.
Any more complex gate would use the output from EXCEPT as a result, therefore well defined output.

However, it is not necessary to do create this axiom to show that Boolean Subtraction is well defined:

    0 - 0 = 0 · !0 = 0
    0 - 1 = 0 · !1 = 0
    1 - 0 = 1 · !0 = 1
    1 - 1 = 1 · !1 = 0

By transforming from EXCEPT to AND NOT and back we can derive all operations we need.
There is no need for an extra axiom.
Now remains to show that these transformations can be done.

##Venn Diagrams

We want to show the transformation

    C = A + B
    <=>
    C - B = A - B

The transformation can be illustrated with two Venn diagrams:

    C = A + B
     ___A_________________
    |=====================|___B_____
    |==============|======|=========|
    |==============|======|=========|
                   |================|

    C - B = A - B
     ___A_________________
    |=====================|___B_____
    |==============|      |         |
    |==============|______|         |
                   |________________|

The transformation goes as following:

    C = A + B
    C·!B = A·!B + B·!B
    C - B = A - B + 0
    C - B = A - B

Using subtraction in basic arithmetic, we would expect something like this:

    C = A + B
    C - B = A
    
    but we got
    
    C - B = A - B

This is because the equation only is valid per bit.
One equation might not be enought to define a bitstream.
Equations are not bitstream-complete.

##Information

Information is important to understand how bitstreams are function complete in circuits.
A circuit with one OR gate and one AND gate outputs the same information.

    f( A, B ) = A · B, A + B
    
    {2,4} · {3,5} = {3,4}
    {2,4} + {3,5} = {2,5}
    
In the example above, all numbers given as input is returned as output.
If we take the two outputs and put it in as input again, we end up where we started.
This is only valid as long there is intersection between the bitstreams.

A function "conserves information" when composed on itself N times returns the same output as input.

    f( f( A, B ) ) = A, B
    
    f^N ( A, B ) = A, B
    
When there is a function G that composed with F returns the same output as input, it is called "inverse function".

    F · G = I

The I is the identity function that returns the input.
For every function that returns input reordered there exists a function to reorder it back.
This property is called "conservation of information".

##Sources

A. http://www.allaboutcircuits.com/vol_4/chpt_7/2.html


