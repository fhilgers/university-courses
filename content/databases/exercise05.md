+++
title = "Exercise 05"
+++

### 1. Import Database with sql instructions

In the online course of the lecture you will find the file
'dbschema-postgres.sql'. This file contains DDL and DML statements for the
creation of the exercise database "Friends". Download the file from the online
course and execute it in your personal Postgres installation (see notes on the
exercise environment in the online course of the lecture). Describe briefly
which elements the file contains, which steps were necessary to create the
friends database, and which problems you might have encountered.

```bash
#!/bin/sh
iconv -f latin1 -t utf8 dbschema-postgres.sql > schema.sql
psql -U postgres -c "CREATE DATABASE friends;"
psql -U postgres friends -c "SET session_replication_role = 'replica';" -f schema.sql
```

### 2. Create UML diagram from schema

Create a UML class diagram for the "Friends" database schema.

<img src="/databases/exercise05/uml.svg" alt="" width="100%" style="margin-left: auto;margin-right: auto;display: block;">

### 3. Extend the database

You need to extend your "Friends" database (using pgAdmin) with a table
Geraet(GID, GName, status, email), in which data around devices used by people
are stored. For attribute 'status' only the values 'aktiv' and 'passiv' should
be allowed. No NULL values are allowed for any attribute. 

a) Write the necessary SQL DDL statements to create the table 'Geraet'. 

```sql
CREATE TYPE status AS ENUM('aktiv', 'passiv');

CREATE TABLE geraet(
GID VARCHAR(60) PRIMARY KEY NOT NULL,
GName VARCHAR(255) NOT NULL,
status status NOT NULL,
email VARCHAR(60) references person(email) NOT NULL
);
```

b) Insert at least 3 tuples in the table using the INSERT statements. 

```sql
insert into geraet(GID, GName, status, email) 
values (
    '158f789f-0142-4575-bf3f-68c1d933fa8b',
    'testDevice01',
    'aktiv',
    'H.Mueller@yahoo.com'
);

insert into geraet(GID, GName, status, email) 
values (
    '145035cd-96fb-4e28-8896-e256f8a2de9c',
    'testDevice02',
    'aktiv',
    'H.Mueller@yahoo.com'
);

insert into geraet(GID, GName, status, email) 
values (
    'd5760e45-626f-4cd2-9720-aae5b9e0b0cc',
    'testDevice03',
    'aktiv',
    'H.Mueller@yahoo.com'
);
```

c) Modify the status of a tuple in the table (e.g., from ‚aktiv' to ‚passiv'),
using the UPDATE statement. What happens if you try to set a status to 
'gesperrt'?

```sql
UPDATE geraet
SET status = 'passiv'
WHERE gid = 'd5760e45-626f-4cd2-9720-aae5b9e0b0cc'

UPDATE geraet
SET status = 'gesperrt'
WHERE email = 'H.Mueller@yahoo.com'
```

### 4. SQL Filtering and Ordering

Write SQL queries for the "Friends" database schema, which provide the following
results: 

a) All data of all persons.

```sql
SELECT * 
FROM person
```


b) The birthdate, first and last name of all women, sorted alphabetically
ascending on the last name.

```sql
SELECT vorname, nachname, geburtsdatum
FROM person
WHERE geschlecht = 'W'
ORDER BY nachname ASC
```


c) The birthdate of persons with first name 'Sophia' and last name 'Krüger'.

```sql
SELECT geburtsdatum 
FROM person
WHERE vorname = 'Sophia' AND nachname = 'Krüger'
```


### 5. SQL Joining

Write SQL queries for the "Friends" database schema, which provide the following
results: 

a) The title of all photos that belong to Sophia Krüger. 

```sql
SELECT titel
FROM person
JOIN photo ON person.email = photo.personemail 
WHERE vorname = 'Sophia' AND nachname = 'Krüger'
```

b) The first and last name of members of the group 'Villach'. 

```sql
SELECT vorname, nachname
FROM istingruppe JOIN person 
  ON istingruppe.email = person.email
WHERE istingruppe.gruppename = 'Villach'
```


c) The birthdate of persons with first name 'Sophia' and last name 'Krüger',
and of persons with first name 'Lena' and last name 'Wagner'.

```sql
SELECT geburtsdatum
FROM person
WHERE (vorname = 'Sophia' AND nachname = 'Krüger') 
OR (vorname = 'Lena' AND nachname = 'Wagner')
```

 
### 6. SQL Grouping

Write SQL queries for the "Friends" database schema, which answer the following
questions: 

a) What is the name of groups that have an owner? 

```sql
SELECT name
FROM gruppe
WHERE emailowner IS NOT NULL
```


b) What are the first and last names of friends of Sophia Krüger? 

```sql
SELECT p2.vorname, p2.nachname
FROM person 
JOIN hatfreund ON person.email = hatfreund.email
JOIN person as p2 ON hatfreund.emailfreund = p2.email
WHERE person.vorname = 'Sophia' AND person.nachname = 'Krüger'
```


c) What are the first and last names of men who are members of both group 
'Villach' and also group 'Klagenfurt'? Sort in ascending order on the last name.

```sql
SELECT vorname, nachname
FROM person p
JOIN istingruppe i ON p.email = i.email
WHERE i.gruppename IN ('Villach', 'Klagenfurt') AND p.geschlecht = 'M'
GROUP BY p.email
HAVING COUNT(DISTINCT i.gruppename) = 2
```


### 7. SQL Distinct

Write SQL queries for the "Friends" database schema, which answer the following
questions: 

a) How many groups are there that have an owner?

```sql
SELECT COUNT(*)
FROM gruppe
WHERE emailowner IS NOT NULL
```


b) What are the names of persons that are tagged in a photo that belongs to the
person with the email address 'L.Wagner@gmx.net'?

```sql
SELECT pe.vorname, pe.nachname
FROM photo p
JOIN istabgebildet i ON p.url = i.photourl
JOIN person pe ON i.personemail = pe.email
WHERE p.personemail = 'L.Wagner@gmx.net'
```


c) What are the names of persons (without repetitions) that have sent a message
to a person who is a friend of Timm Lang? Sort the result in ascending order on
the last name and in ascending order on the first name.

```sql
SELECT DISTINCT p2.vorname, p2.nachname
FROM person p
  JOIN hatfreund h ON p.email = h.email
  JOIN nachricht n ON h.emailfreund = n.anemail
  JOIN person p2 ON n.vonemail = p2.email
WHERE p.vorname = 'Timm' AND p.nachname = 'Lang'
ORDER BY p2.vorname ASC
```
