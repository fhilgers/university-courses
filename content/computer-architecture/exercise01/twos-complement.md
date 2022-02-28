+++
title = "1. Two's Complement"
weight = 1
+++

<h3>
1. Explain the representation of signed integer values using the two's 
complement representation.
</h3>

<h4>
(a) Which range of values can be covered with an n-bit two's complement
representation?
</h4>

{% katex(block=true) %}
-2^{n - 1} \lt x \lt 2^{n - 1} - 1
{% end %}

<h4>
(b) What are the advantages of using two's complement compared to other
types of signed integer value representations (e.g. one's complement)?
</h4>

- The two's complement representation can represent one more number with the
same amount of bits, because zero is well defined.
- It simplifies arithmetic operations.

<h4>
(c) What is arithmetic overflow and how do you detect it?
</h4>

An arithmetic overflow occurs when a number is to small or too big to represent
it with a certain amount of bits. For example:

One can only represent integers ranging from -128 to 127 in two's complement
representation. That means that adding 1 to the integer 127 results in an 
overflow. This overflow can be detected by just looking at the highest order
bit which flips in this case.

<h4>
(d) How can you tell in two's complement representation that a number is
positive/negative or even/odd?
</h4>

The sign of a number can be recognized by looking at the highest order bit. 
If this is bit is zero, then the number is positive. If it is one, then the
number is negative.
To tell if a number is even or odd, one can look at the lowest order bit. An
integer is even if this bit is zero and odd if it is one.
