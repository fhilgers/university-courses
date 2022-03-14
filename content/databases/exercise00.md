+++
title = "Exercise 00"
slugify.anchors = "off"
+++

Given the sets:

{% katex(block=true) %}

\begin{align*}
A &= \{ 15, 30 \}                \\
B &= \{ 1, 5, 10 \}              \\
C &= \{ 1, 2, 3, 4, 5, 15, 30 \} \\
\end{align*}

{% end %}

### 1. Calculate the following sets:

a) {{ katex(body="A \cup B") }}

{% katex(block = true) %}
A \cup B = \{ 15, 30 \} \cup \{ 1, 5, 10 \} = \{ 1, 5, 10, 15, 30 \}
{% end %}

b) {{ katex(body="A \cap C") }}

{% katex(block = true) %}
A \cap C = \{ 15, 30 \} \cap \{ 1, 2, 3, 4, 5, 15, 30 \} = \{ 15, 30 \}
{% end %}

c) {{ katex(body="C \setminus A") }}

{% katex(block = true) %}
C \setminus A = \{ 1, 2, 3, 4, 5, 15, 30 \} \setminus \{ 15, 30 \} = \{ 1, 2, 3, 4, 5 \}
{% end %}

d) {{ katex(body="B \times A") }}

{% katex(block = true) %}
B \times A = \{ 1, 5, 10 \} \times \{ 15, 30 \} = 
\{ (1, 15), (1, 30), (5, 15), (5, 30), (10, 15), (10, 30) \}
{% end %}


### 2. Do these properties hold?

a) {{ katex(body="A \cup B \subset C") }}

{% katex(block = true) %}
A \cup B = \{ 1, 5, 10, 15, 30 \} \subset \{ 1, 2, 3, 4, 5, 15, 30\} = C
{% end %}

{{ katex(body="\Rightarrow") }} true

b) {{ katex(body="(15, 5, 15) \in A \times B \times C") }}

{% katex(block = true) %}
(15 \in A) \land (5 \in B) \land (15 \in C)
{% end %}

{{ katex(body="\Rightarrow") }} true

c) {{ katex(body="\{ (30, 1, 1), (15, 15, 15) \} \subseteq A \times B \times C") }}

{% katex(block = true) %}
15 \notin B
{% end %}

{{ katex(body="\Rightarrow") }} false

### 3. Give the following sets

a) {{ katex(body="X = \{ x | x > 1 \land x <= 15 \land x \in C \}")}}

{% katex(block = true) %}
X = \{ x | x > 1 \land x \le 15 \land x \in C \} = \{ 2, 3, 4, 5, 15 \}
{% end %}

b) {{ katex(body="Y = \{ x | (x \in A) \lor (x \in C)\}")}}

{% katex(block = true) %}
Y = \{ x | (x \in A) \lor (x \in C)\} = \{ 1, 2, 3, 4, 5, 15, 30 \}
{% end %}

c) {{ katex(body="Z = \{ x | (x \in A) \land (x \notin C)\}")}}

{% katex(block = true) %}
Z = \{ x | (x \in A) \land (x \notin C)\} = \{ \}
{% end %}

### 4. What is the cardinality of the following sets?

a) {{ katex(body="|C|")}}

{% katex(block = true) %}
|C| = |\{ 1, 2, 3, 4, 5, 15, 30 \}| = 7
{% end %}

b) {{ katex(body="|A \times B|")}}

{% katex(block = true) %}
|A \times B| = |A| \cdot |B| = 
|\{ 15, 30 \}| \cdot |\{ 1, 5, 10 \}| = 2 \cdot 3 = 6
{% end %}


### 5. Do the following hold?

a) {{ katex(body="\forall x \in A, \exists y \in B : x = y")}}

{{ katex(body="\Rightarrow \text{false, example: } 15 \notin B") }}

b) {{ katex(body="\forall x \in A, \exists y \in C : y = \frac{x}{15}")}}

{{ katex(body="\Rightarrow \text{true: } (1 \in C) \land (2 \in C)") }}

### 6. What is the cardinality of the following set?

{% katex(block = true) %}
|\{x | x \in B \land \exists y \in A : x = \frac{y}{3} \}| = |\{ 5, 10 \}| = 2
{% end %}

### 7. What is the cardinality of the following set?

{% katex(block = true) %}
|\{(x, x) \in A \times C \}| = |\{(15, 15), (30, 30)\}| = 2
{% end %}






