+++
title = "Exercise 04"
+++


### 1. Translate class diagram 1 into a relational model

Given the following UML class diagram 1:

**Translate class diagram 1 into a relational model. Use the rules that you have
seen in the lecture. Highlight primary keys (underlined) and foreign keys 
(italics).**

- Director(<u>DirID</u>, DirFirstName, DirLastName)
- Film(<u>FilmID</u>, Title, Year, Country, _DirID_)
- Actor(<u>ActorID</u>, FirstName, LastName, Birthdate, Birthplace)
- Plays_in(<u>Role, isMain, _FilmID_, _ActorID_</u>)

### 2. Translate class diagram 2 into a relational model

Given the following UML class diagram 2:


**Translate class diagram 2 into a relational model. Use the rules that you have
seen in the lecture. Highlight primary keys (underlined) and foreign keys 
(italics).**

- Pharmacy(<u>PharmacyID</u>, PharmacyName, PharmacyAddress, PharmacyPhone)
- TestStation(<u>StationID</u>, StationName, Address, _PharmacyID_)
- CoronaTest(<u>TestID</u>, Type, Result, Timestamp)
- Patient(<u>SVNR</u>, FirstName, LastName, Birthdate, PatientAddress, 
    PatientPhone, PatientEmail)
- takes(<u>_StationID_, _TestID_, _SVNR_</u>)

### 3. Translate class diagram 3 into a relational model

#### a) Floor Strategy

- Mobile(<u>IMEI</u>, BrandName, ModelName, Year, 
    Memory, Carrier)
- Laptop(<u>IMEI</u>, BrandName, ModelName, Year, 
    CPU, RAM, Storage, ScreenSize)
- SmartSpeaker(<u>IMEI</u>, BrandName, ModelName, Year, 
    Color)
- Reparation(<u>ReparationID</u>, Date, Price, _IMEI_)


#### b) Ceiling Strategy

Type refers to either Mobile, Laptop or Smartspeaker.

- Device(<u>IMEI</u>, BrandName, ModelName, Year, 
    Memory, Carrier,
    CPU, RAM, Storage, ScreenSize,
    Color,
    type)
- Reparation(<u>ReparationID</u>, Date, Price, _IMEI_)


#### c) Cohesion Strategy

- Device(<u>IMEI</u>, BrandName, ModelName, Year)
- Mobile(<u>Memory, Carrier, _IMEI_</u>)
- Laptop(<u>CPU, RAM, Storage, ScreenSize, _IMEI_</u>)
- SmartSpeaker(<u>Color, _IMEI_</u>)
- Reparation(<u>ReparationID</u>, Date, Price, _IMEI_)


### 4. Show the results oft the operations in tabular form

**Film:**

| ID    | Titel                 | Regisseur         |
|:-----:|:----------------------|:------------------|
| 21201 | The dark knight       | Christopher Nolan |
| 21202 | Isle of dogs          | Wes Anderson      |
| 21203 | In the mood for love  | Wong Kar-wai      |
| 22341 | The lord of the rings | Peter Jackson     |
| 22342 | Inception             | Christopher Nolan |
| 22965 | Memento               | Chritopher Nolan  |
| 23546 | Hong Kong Express     | Wong Kar-wai      |
| 26545 | The Grandmaster       | Wong Kar-wai      |
| 26546 | Fantastic Mr. Fox     | Wes Anderson      |

**Bietet:**

| ID    | PlattformID |
|:-----:|:-----------:|
| 21201 | P2          |
| 21202 | P1          |
| 21203 | P1          |
| 22341 | P3          |
| 22342 | P1          |
| 22965 | P2          |
| 23546 | P2          |
| 26545 | P3          |
| 26546 | P2          |
| 21201 | P3          |
| 21202 | P2          |
| 21203 | P3          |
| 22341 | P1          |
| 22342 | P2          |

**Plattform:**

| PlattformID | Name       | PreisProMonat |
|:-----------:|:-----------|:-------------:|
| P1          | Netflix    | 9.99          |
| P2          | PrimeVideo | 7.99          |
| P3          | Disney+    | 9.99          |

a) {{ katex(body="\sigma_{\text{PreisProMonat}=7.99}(\text{Plattform})") }} 

| PlatformID | Name       | PreisProMonat |
|:----------:|:-----------|:-------------:|
| P2         | PrimeVideo | 7.99          |

b) {{ katex(body="\sigma_{\text{Regisseur}='\text{Wes Anderson}'}(\text{Plattform})") }} 

| ID    | Titel             | Regisseur    |
|:-----:|:------------------|:-------------|
| 21202 | Isle of dogs      | Wes Anderson |
| 26546 | Fantastic Mr. Fox | Wes Anderson |

c) {{ katex(body="\pi_{\text{Titel}}(\sigma_{\text{ID} > 23000}(\text{Film}))")}}

| Titel             |
|:------------------|
| Hong Kong Express |
| The Grandmaster   |
| Fantastic Mr. Fox |

d) {{ katex(body="\text{Film} \Join \text{Bietet}")}}

| ID    | Titel                 | Regisseur         | PlatformID |
|:-----:|:----------------------|:------------------|:----------:|
| 21201 | The dark knight       | Christopher Nolan | P2         |
| 21201 | The dark knight       | Christopher Nolan | P3         |
| 21202 | Isle of dogs          | Wes Anderson      | P1         |
| 21202 | Isle of dogs          | Wes Anderson      | P2         |
| 21203 | In the mood for love  | Wong Kar-wai      | P1         |
| 21203 | In the mood for love  | Wong Kar-wai      | P3         |
| 22341 | The lord of the rings | Peter Jackson     | P1         |
| 22341 | The lord of the rings | Peter Jackson     | P3         |
| 22342 | Inception             | Christopher Nolan | P1         |
| 22342 | Inception             | Christopher Nolan | P2         |
| 22965 | Memento               | Chritopher Nolan  | P2         |
| 23546 | Hong Kong Express     | Wong Kar-wai      | P2         |
| 26545 | The Grandmaster       | Wong Kar-wai      | P3         |
| 26546 | Fantastic Mr. Fox     | Wes Anderson      | P2         |

e) {{ katex(body="\pi_{\text{Titel,Name,Preis}}((\text{Film} \Join \text{Bietet}) \Join \text{Platform})")}}

| Titel                 | Name       | PreisProMonat |
|:----------------------|:-----------|:-------------:|
| The dark knight       | PrimeVideo | 7.99          |
| The dark knight       | Disney+    | 9.99          |
| Isle of dogs          | Netflix    | 9.99          |
| Isle of dogs          | PrimeVideo | 7.99          |
| In the mood for love  | Netflix    | 9.99          |
| In the mood for love  | Disney+    | 9.99          |
| The lord of the rings | Netflix    | 9.99          |
| The lord of the rings | Disney+    | 9.99          |
| Inception             | Netflix    | 9.99          |
| Inception             | PrimeVideo | 7.99          |
| Memento               | PrimeVideo | 7.99          |
| Hong Kong Express     | PrimeVideo | 7.99          |
| The Grandmaster       | Disney+    | 9.99          |
| Fantastic Mr. Fox     | PrimeVideo | 7.99          |


### 5. Formulate the queries from 4 in Tuple calculus.

a) {{ katex(body="\sigma_{\text{PreisProMonat}=7.99}(\text{Plattform})") }} 

{% katex(block=true) %}

res = \{ t | t \in \text{Platform} \land t.\text{PreisProMonat} = 7.99 \}

{% end %}


b) {{ katex(body="\sigma_{\text{Regisseur}='\text{Wes Anderson}'}(\text{Plattform})") }} 

{% katex(block=true) %}

res = \{ t | t \in \text{Film} \land t.\text{Regisseur} = '\text{Wes Anderson}' \}

{% end %}

c) {{ katex(body="\pi_{\text{Titel}}(\sigma_{\text{ID} > 23000}(\text{Film}))")}}

{% katex(block=true) %}

\begin{align*}
x   &= \{ t | t \in \text{Film} \land t.\text{ID} > 23000 \} \\
res &= \{ s.\text{Titel} | s \in x \}
\end{align*}

{% end %}


d) {{ katex(body="\text{Film} \Join \text{Bietet}")}}

{% katex(block=true) %}

res = \{ t | t.\text{ID} \in \text{Film} \land 
             t.\text{ID} \in \text{Bietet} \land 
             t.\text{ID} = t.\text{ID} \}

{% end %}

e) {{ katex(body="\pi_{\text{Titel,Name,Preis}}((\text{Film} \Join \text{Bietet}) \Join \text{Platform})")}}

{% katex(block=true) %}

\begin{align*}
a   &= \{ t | t.\text{ID} \in \text{Film} \land 
           t.\text{ID} \in \text{Bietet} \land 
           t.\text{ID} = t.\text{ID} \} \\
b   &= \{ t | t.\text{ID} \in a \land 
           t.\text{ID} \in \text{Platform} \land 
           t.\text{ID} = t.\text{ID} \} \\
res &= \{ t.\text{Titel}, t.\text{Name}, t.\text{Preis} | t \in b \}
\end{align*}

{% end %}


### 6. Formulate the queries from 4 in SQL.

a) {{ katex(body="\sigma_{\text{PreisProMonat}=7.99}(\text{Plattform})") }} 

```sql
SELECT * FROM Platform WHERE PreisProMonat = 7.99
```

b) {{ katex(body="\sigma_{\text{Regisseur}='\text{Wes Anderson}'}(\text{Plattform})") }} 

```sql
SELECT * FROM Film WHERE Regisseur = "Wes Anderson"
```

c) {{ katex(body="\pi_{\text{Titel}}(\sigma_{\text{ID} > 23000}(\text{Film}))")}}

```sql
SELECT Film.Titel FROM Film WHERE ID > 23000
```

d) {{ katex(body="\text{Film} \Join \text{Bietet}")}}

```sql
SELECT * 
FROM Film
FULL JOIN Bietet ON Film.ID = Bietet.ID
```

e) {{ katex(body="\pi_{\text{Titel,Name,Preis}}((\text{Film} \Join \text{Bietet}) \Join \text{Platform})")}}

```sql
SELECT Titel, Name, Preis
FROM Film
    FULL JOIN Bietet ON Film.ID = Bietet.ID
    FULL JOIN Platform ON Film.ID = Platform.ID
```
