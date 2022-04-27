---
title: "Databases - Assignment sheet 06"
author: [Felix Hilgers]
date: "26.04.2022"
---

# Exercise 1 (Functional dependencies)

Given the following relation:

\scriptsize

| BestellNr | KundenNr | Name        | ArtikelNr | KategorieNr | Kategorie  | Status | Statusname      | Bestellmenge |
|:---------:|:--------:|:-----------:|:---------:|:-----------:|:----------:|:------:|:---------------:|:------------:|
| 1001      | 100      | Mueller     | 11        | 2           | MS Office  | OP     | vergriffen      | 10           |
| 1001      | 100      | Mueller     | 12        | 2           | MS Office  | AV     | lieferbar       | 40           |
| 1002      | 101      | Schulz      | 13        | 1           | Internet   | OP     | vergriffen      | 20           |
| 1003      | 101      | Schulz      | 11        | 2           | MS Office  | AV     | lieferbar       | 30           |
| 1003      | 101      | Schulz      | 12        | 2           | MS Office  | AV     | lieferbar       | 50           |
| 1003      | 101      | Schulz      | 13        | 1           | Internet   | OP     | vergriffen      | 20           |
| 1004      | 102      | Meyer       | 11        | 2           | MS Office  | AV     | lieferbar       | 50           |
| 1004      | 102      | Meyer       | 18        | 3           | Wirtschaft | IP     | in Vorbereitung | 20           |
| 1005      | 103      | Beta Design | 12        | 2           | MS Office  | AV     | lieferbar       | 30           |
| 1006      | 104      | Lange       | 11        | 2           | MS Office  | AV     | lieferbar       | 40           |
| 1006      | 104      | Lange       | 13        | 1           | Internet   | OP     | vergriffen      | 20           |
| 1007      | 104      | Lange       | 17        | 4           | Management | OR     | auf Anfrage     | 30           |

\normalsize

a) Name as many functional dependencies as possible that apply to the relation
shown. To minimize paperwork, use abbreviations for the attributes.

- `[ BestellNr, KundenNr, Name ]`
- `[ ArtikelNr, KategorieNr, Kategorie ]`
- `[ Kategorie, KategorieNr ]`
- `[ Status, Statusname ]`
- `[ Statusname, Status ]`

b) List all key candidates for this relation.

- `[ BestellNr, ArtikelNr, Status ]`

c) What anomalies can occur in this relation? Give an example of each.

- `KundenNr` can have different `Name` associated with it
- `ArtikelNr` can have different `KategorieNr` associated with it
- `KategorieNr` can have different `Kategorie` associated with it
- `Status` can have different `Statusname` associated with it

\pagebreak

d) How could the quality of this relationship be improved?

Turn it into the third normal form:

1. `Order(<u>OrderNr</u>, *CustomerNr*)`

\scriptsize

| OrderNr | CustomerNr |
|:-------:|:----------:|
| 1001    | 100        |
| 1002    | 101        |
| 1003    | 101        |
| 1004    | 102        |
| 1005    | 103        |
| 1006    | 104        |
| 1007    | 104        |

\normalsize

2. `OrderArticle(<u>*OrderNr*, *ArticleNr*</u>, *StatusType*, Amount)`

\scriptsize

| OrderNr | ArticleNr | StatusType | Amount |
|:-------:|:---------:|:----------:|:-------------:|
| 1001    | 11        | OP         | 10     |
| 1001    | 12        | AV         | 40     |
| 1002    | 13        | OP         | 20     |
| 1003    | 11        | AV         | 30     |
| 1003    | 12        | AV         | 50     |
| 1003    | 13        | OP         | 20     |
| 1004    | 11        | AV         | 50     |
| 1004    | 18        | IP         | 20     |
| 1005    | 12        | AV         | 30     |
| 1006    | 11        | AV         | 40     |
| 1006    | 13        | OP         | 20     |
| 1007    | 17        | OR         | 30     |

\normalsize

3. `Customer(<u>CustmerNr</u>, CustomerName)`

\scriptsize

| CustomerNr | CustomerName |
|:----------:|:------------:|
| 100        | Mueller      |
| 101        | Schulz       |
| 102        | Meyer        |
| 103        | Beta Design  |
| 104        | Lange        |

\normalsize

4. `Article(<u>ArticleNr</u>, CategorieNr)`

\scriptsize

| ArticleNr | CategorieNr |
|:---------:|:-----------:|
| 11        | 2           |
| 12        | 2           |
| 13        | 1           |
| 17        | 4           |
| 18        | 3           |

\normalsize

5. `Categorie(<u>CategorieNr</u>, CategorieName)`

\scriptsize

| CategorieNr | CategorieName  |
|:-----------:|:--------------:|
| 1           | Internet       |
| 2           | MS Office      |
| 3           | Wirtschaft     |
| 4           | Management     |

\normalsize

6. `Status(<u>StatusType</u>, StatusName)`

\scriptsize

| StatusType | StatusName      |
|:----------:|:---------------:|
| OP         | vergriffen      |
| AV         | lieferbar       |
| IP         | in Vorbereitung |
| OR         | auf Anfrage     |

\normalsize

# Exercise 2 (Normal forms)

Given the following relational schema:

`Employee (MNR, SVNR, Name, DepartmentNr, DepartmentDesignation)`

Each Employee has a unique MNR and a unique SVNR. Each employee is assigned to
exactly one department and a department has a unique department number. The name
and department designation are not unique.

a) State the functional dependencies of this relational schema.

`SVNR` is functionally dependent on `MNR` while `Name` is in turn dependent on
`SVNR`. The `DepartmentNr` is dependent on `MNR` and the `DepartmentDesignation`
is dependent on the `DepartmentNr`.

b) Specify superkeys and all candidate keys.

- Superkeys are:

  - `[ MNR, (SVNR, Name, DepartmentNr, DepartmentDesignation) ]`
  - `[ SVNR, (MNR, Name, DepartmentNr, DepartmentDesignation) ]`

- Candidate keys are:

  - `[ PatNr ]`
  - `[ SVNR ]`

**NOTE:** The superkeys can optionally contain any permutation of the keys
inside of the parentheses.

c) Determine the normal form of this relational schema.

It satisfies the conditions of the first normal form, because each column
contains only a single value.

It satisfies the conditions for second normal form because every not
candidate-key depends on the whole candidate key because it is just a single
key.

It fails to satisfy the conditions for third normal form because the relational
scheme has a transitive functional dependency. `Name` is dependent on `SVNR`
while `SVNR` is in turn dependent on `MNR`, also `DepartmentDesignation` is
dependent on `DepartmentNr`.

# Exercise 3 (Normal forms)

a) Decompose the relational schema Employee from Exercise 2 in such a way that
all partial schemas are at least in the 3rd normal form. Determine all
functional dependencies and key candidates of the sub-schemas.

- `Person(SVNR, Name)`
 
  `SVNR` is the key candidate and `Name` is funcionally dependent on it.

- `Employee(MNR, SVNR, DepartmentNr)`

  `MNR` is the key candidate and both `SVNR` and `DepartmentNr` are dependent on
  it.

- `Department(DepartmentNr, DepartmentDesignation)`

  `DepartmentNr` is the key candidate and `DepartmentDesignation` is the key
  candidate.

b) Write an SQL query that returns the original schema from Exercise 2 from the
relational schema broken down in Exercise 3a).

```sql
SELECT
  e.mnr,
  p.svnr,
  p.name,
  d.departmentnr,
  d.departmentdesignation 
FROM
  employee e 
  JOIN
    person 
    ON e.svnr = p.svnr 
  JOIN
    department d 
    ON e.departmentnr = d.departmentnr
```

# Exercise 4 (Normal forms)

In order to record which patient(s) received which vaccination, it was suggested
to you to use the following relational schema:

`VaccinationData(PatNr, SVNR, FirstName, LastName, Birthdate, VaccinationNr,
VaccinationName)`

A patient can receive several vaccinations. The first name, last name and date
of birth of patients as well as the vaccination names are not unique.


a) Give the functional dependencies of this relational schema according to the
description:

`FirstName`, `LastName`, `Birthdate` are funcionally dependent on `SVNR`, `SVNR`
is dependent on `PatNr`. `VaccinationName` is functionally dependent on the
combination of `PatNr` and `VaccinationNr`.

b) Give the superkeys and all key candidates:

- Superkeys are:

  - `[ PatNr, VaccinationNr, (SVNR, FirstName, LastName, Birthdate,
    VaccinationName) ]`
  - `[ SVNR, VaccinationNr, (PatNr, FirstName, LastName, Birthdate,
    VaccinationName) ]`

- Candidate keys are:

  - `[ PatNr, VaccinationNr ]`
  - `[ SVNR, VaccinationNr ]`

**NOTE:** The superkeys can optionally contain any permutation of the keys
inside of the parentheses.

c) Determine the normal form of this relational schema:

The relational schema is in first normal form.

It satisfies the conditions of the first normal form, because each column
contains only a single value.

It fails to satisfies the conditions for second normal form because not every
non candidate-key depends on the whole candidate key. `FirstName`, `LastName`,
`Birthdate` only depend on `SVNR` or `PatNr` respectively, only
`VaccinationName` depends on the `VaccinationNr` as well.

It also fails to satisfy the conditions for third normal form because the
relational scheme has a transitive functional dependency. `FirstName`,
`LastName` and `Birthdate` are functionally dependent on `SVNR` and `SVNR` is in
turn dependent on `PatNr`.

d) Decompose the relational scheme to achieve a higher normal form and check
which normal form is followed by the decomposition:

The following relational scheme is now in third normal form:

- `Person(SVNR, FirstName, LastName, Birthdate)`
- `Patient(PatNr, SVNR)`
- `Vaccination(PatNr, VaccinationNr, VaccinationName)`

e) Create an SQL query that returns a relation with the original schema from the
broken down relations:

```sql
SELECT
  p.patnr,
  p.svnr,
  pe.firstname,
  pe.lastname,
  pe.birthdate,
  v.vaccinationnr,
  v.vaccinationname 
FROM
  patient p 
  JOIN
    vaccination v 
    ON p.patnr = v.patnr 
  JOIN
    person pe 
    ON p.svnr = pe.svnr
```

# Exercise 5 (SQL)

Specify SQL queries that answer the following questions:

a) Which people (the email address is sufficient) have not yet received a
message?

```sql
SELECT DISTINCT
  p.email 
FROM
  person p 
EXCEPT
SELECT
  n.anemail 
FROM
  nachricht n
```

b) Which people (first name, last name) have sent messages to at least one of
their friends?

```sql
SELECT DISTINCT
  p.vorname,
  p.nachname 
FROM
  person p 
  FULL JOIN
    hatfreund h 
    ON p.email = h.email 
  FULL JOIN
    nachricht n 
    ON n.anemail = h.emailfreund 
WHERE
  p.email IS NOT NULL
```

c) Which people have never sent a message to one of their friends?

```sql
SELECT DISTINCT
  p.vorname,
  p.nachname 
FROM
  person p 
  FULL JOIN
    hatfreund h
    ON h.email = p.email 
  FULL JOIN
    nachricht n
    ON n.anemail = h.emailfreund 
WHERE
  n.id IS NULL
```

# Exercise 6 (SQL)

Specify SQL queries that answer the following questions.

a) Create a query that returns for each person (first name, last name) who has
already sent a message, the number of sent messages. Sort the result in
descending order of the number of messages.

```sql
SELECT
  p.vorname,
  p.nachname,
  COUNT(n.id)
FROM
  person p
  INNER JOIN nachricht n ON p.email = n.vonemail
GROUP BY
  p.email
ORDER BY
  COUNT(n.id) DESC
```

b) Which people (email address, first name, last name) have already received
exactly 2 messages?

```sql
SELECT
  p.vorname,
  p.nachname
FROM
  person p
  INNER JOIN nachricht n ON p.email = n.anemail
GROUP BY
  p.email
HAVING
  COUNT(n.id) = 2
```

# Exercise 7 (SQL)

Specify SQL queries that answer the following questions.

a) Who (email address, first name, last name) has already sent more messages
than Lara Neumann?

```sql
SELECT
  n.email,
  n.vorname,
  n.nachname
FROM
  person p
  INNER JOIN nachricht n ON p.email = n.vonemail
GROUP BY
  n.email
HAVING
  COUNT(n.id) > (
    SELECT
      COUNT(n.id)
    FROM
      nachricht n
    WHERE
      n.vonemail = 'Lara Neumann'
  )
```

b) Which person has as many friends as he/she has already sent messages?

```sql
SELECT
  h.email,
  COUNT(n.id) AS message_count,
  COUNT(h.emailfreund) AS friend_count
FROM
  nachricht n
  INNER JOIN hatfreund h ON n.vonemail = h.email
GROUP BY
  h.email
HAVING
  COUNT(h.emailfreund) >= COUNT(n.id)
```

c) Who has the most friends? Note that if multiple people have the same number
of friends, the result may contain more than one person.

```sql
SELECT
  h.email
FROM
  hatfreund h
GROUP BY
  h.email
HAVING
  COUNT(h.emailfreund) = (
    SELECT
      COUNT(h.emailfreund)
    FROM
      hatfreund h
    GROUP BY
      h.email
    ORDER BY
      COUNT(h.emailfreund) DESC
    LIMIT
      1
  )
```
