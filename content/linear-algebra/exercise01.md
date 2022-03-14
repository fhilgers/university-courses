+++
title = "Exercise 01"
+++

### 1. Solve the following systems of linear equations

(a)

{% katex(block=true) %}
\begin{align}
  x_{1} + 3 x_{2} + 2 x_{3} &=  2  \tag{1} \\
2 x_{1} + 6 x_{2} + 9 x_{3} &= -6  \tag{2} \\
2 x_{1} + 8 x_{2} + 8 x_{3} &= -4  \tag{3} \\
			           \notag  \\
  x_{1} + 3 x_{2} + 2 x_{3} &=  2  \tag{1} \\
          2 x_{2} + 4 x_{3} &= -8  \tag{3} \\
	            5 x_{3} &= -10 \tag{2} \\
                                   \notag  \\
  x_{1} + 3 x_{2} + 2 x_{3} &=  2  \tag{1} \\
            x_{2} + 2 x_{3} &= -4  \tag{3} \\
	              x_{3} &= -2  \tag{2} \\
                                   \notag  \\
                      x_{1} &=  6  \notag  \\
                      x_{2} &=  0  \notag  \\
	              x_{3} &= -2  \notag  \\
\end{align}
{% end %}

(b)

{% katex(block=true) %}
\begin{align}
   x_{1} + 2 x_{2} +   x_{3} &= 0 \tag{1} \\
   x_{1} +   x_{2} - 2 x_{3} &= 0 \tag{2} \\
-2 x_{1} - 3 x_{2} +   x_{3} &= 0 \tag{3} \\
			          \notag  \\
   x_{1} + 2 x_{2} +   x_{3} &= 0 \tag{1} \\
         -   x_{2} - 3 x_{3} &= 0 \tag{2} \\
	     x_{2} + 3 x_{3} &= 0 \tag{3} \\
			          \notag  \\
   x_{1} + 2 x_{2} +   x_{3} &= 0 \tag{1} \\
	     x_{2} + 3 x_{3} &= 0 \tag{3} \\
                           0 &= 0 \tag{2} \\
			     	  \notag  \\
                       x_{1} &=   5 x_{3} \notag \\
	               x_{2} &= - 3 x_{3} \notag \\
		       x_{3} &=     x_{3} \notag \\
	        
\end{align}
{% end %}

### 2. Matrix-Vector Multiplication

The coffee machine at the Institute of Mathematics can produce espresso, 
cappuccino and cocoa. For an espresso, it requires 1 unit of water and 2 units
of coffee. For a cappuccino it needs 2 units of water, 2 units of coffee and 1
unit of milk. For a cocoa 1 unit of water, 2 units of milk, and 2 units of
cocoa are needed.

On Thursday, the exercise leaders drink 5 cups of espresso, 3 cups of
cappuccino, and one cup of cocoa. Use matrix-vector multiplication to calculate
how many units of coffee, cocoa, milk, and water need to be put into the
vending machine in the morning on Thursday so that the instructors can get the
drinks they want.

{% katex(block=true) %}
\left( \begin{array}{ccc}
1 & 2 & 1 \\
0 & 2 & 2 \\
2 & 1 & 0 \\
2 & 0 & 0 \\
\end{array} \right) 
\cdot 
\left( \begin{array}{cl}
1 & \text{(cocoa)}      \\
3 & \text{(cappuccino)} \\
5 & \text{(espresso)}   \\
\end{array} \right)
=
\left( \begin{array}{cl}
12 & \text{(water)}  \\
16 & \text{(coffee)} \\
 5 & \text{(milk)}   \\
 2 & \text{(cocoa)}  \\
\end{array} \right)
{% end %}

### 3. Interpretation of Matrix-Vector Multiplication

A pizzeria produces {{ katex(body="n") }} types of pizza and uses 
{{ katex(body="m") }} ingredients. For {{ katex(body="1 \le i \le m") }} and
{{ katex(body="1 \le j \le n") }} let {{ katex(body="a_{ij}") }} be the
quantity of ingredient {{ katex(body="i") }} used to make pizza
{{ katex(body="j") }}. For {{ katex(body="1 \le j \le n") }} let
{{ katex(body="x_{j}") }} denote the number of pizzas of variety
{{ katex(body="j") }} sold in a day. Let {{ katex(body="A = (a_{ij})") }} and
{{ katex(body="x = (x_{j})") }}.

**Interpret the matrix-vector multiplication {{ katex(body="Ax") }} in this
context.**

The result of this multiplication is a vector of all ingedients and their
quantities similar to the previous task to produce all the pizzas specified by
{{ katex(body="x_{j}") }}.


### 4. Magic Square

A {{ katex(body="3 \times 3") }} square is called a magic square if each number
from 1 to 9 occurs exactly once and the sum of each of the three rows, the sum
of each of the three columns, and the sums of the two diagonals are equal.

#### (a) What is the value of this sum?

The sum has to be 15. The reason for this is that the digits from 1 to 9 all
summed up equals to 45. That means that the sum of three rows or columns added
together has to amount to 45 which in return results in each row and column
adding up to 15.

#### (b) Formulate the sum properties.
Formulate the sum properties regarding column, row and diagonal sums that a
magic square must have, as a linear system of equations.

{% katex(block=true) %}
\left( \begin{array}{}
1 & 1 & 1 & 0 & 0 & 0 & 0 & 0 & 0 \\
0 & 0 & 0 & 1 & 1 & 1 & 0 & 0 & 0 \\
0 & 0 & 0 & 0 & 0 & 0 & 1 & 1 & 1 \\
1 & 0 & 0 & 1 & 0 & 0 & 1 & 0 & 0 \\
0 & 1 & 0 & 0 & 1 & 0 & 0 & 1 & 0 \\
0 & 0 & 1 & 0 & 0 & 1 & 0 & 0 & 1 \\
1 & 0 & 0 & 0 & 1 & 0 & 0 & 0 & 1 \\
0 & 0 & 1 & 0 & 1 & 0 & 1 & 0 & 0 \\
\end{array} \right) 
\cdot 
\left( \begin{array}{}
a \\
b \\
c \\
d \\
e \\
f \\
g \\
h \\ 
i \\
\end{array} \right)
=
\left( \begin{array}{}
15 \\
15 \\
15 \\
15 \\
15 \\
15 \\
15 \\
15 \\
\end{array} \right)
{% end %}


#### (c) Complete the following square to a magic square

{% katex(block=true) %}
\left[ \begin{array}{}
8 & 3 & 4 \\
1 & 5 & 9 \\
6 & 7 & 2 \\
\end{array} \right]
{% end %}


