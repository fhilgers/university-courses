+++
title = "Exercise 01"
+++

### 1. Problem with data systems

| Datum      | Ort                  | Zeit          | Vogelart     | Anzahl | Zugvogel | Familie        | Beobacher*in | Email         |
|------------|----------------------|---------------|--------------|--------|----------|----------------|--------------|---------------|
| 16.01.2021 | Klagenfurt, Kaernten | 09.00 - 11.00 | Blaumeise    | 2      | nein     | Meisen         | Anna Wert    | a.w@gmail.com |
| 16.01.2021 | Klagenfurt, Kaernten | 09.00 - 11.00 | Haussperling | 14     | nein     | Sperlingvogel  | Anna Wert    | a.w@gmail.com |
| 16.01.2021 | Klagenfurt, Kaernten | 09.00 - 11.00 | Kleiber      | 1      | nein     | Meisen         | Anna Wert    | a.w@gmx.at    |
| 02.05.2021 | Villach, Kaernten    | 12.00 - 13.00 | Blaumeise    | 1      | nein     | Meisen         | Jan Vogel    | j.v@gmail.com |
| 02.05.2021 | Villach, Kaernten    | 12.00 - 13.00 | Schwalbe     | 3      | ja       | Sperlingsvogel | Jan Vogel    | j.v@gmail.com |
| 01.08.2021 | Graz, Stmk           | 09.00 - 11.00 | Bachstelze   | 2      | ja       | Stelze         | Lea Berg     | l.b@gmail.com |
| 03.08.2021 | Villach, Kaernten    | 17.00 - 18.00 | Blaumeise    | 1      | ja       | Meisen         | Jan Vogel    | a.w@gmx.at    |
| 03.08.2021 | Villach, Kaernten    | 17.00 - 18.00 | Schwalbe     | 3      | ja       | Sperlingsvogel | Jan Vogel    | a.w@gmx.at    |


**Which redundancies and inconsistencies can you identify?**

Redundancies:

- Dates
- Locations
- Times
- etc.

Inconsistencies:

- Email: Anna Wert has multiple email addresses
- Spelling Mistake: Sperlingvogel
- Bluetit is migratory and non-migratory bird at the same time

**What typical problems can occur when an application uses 
files as described above to store its data?** 
*Assumption: Several different applications read and write the files 
and each application has several users.*

There is no standarisation of how the data is represented. This creates tight 
coupling between the application and the specifiic data representation chosen
and is a lot less flexible than a database. Also, as there is no good way to 
represent relations, there is a lot of redundancy and inconsistency as seen
in the table above.

### 2. ANSI SPARC

The ANSI SPARC model is a standard reference model for building a database. 

**Roughly sketch its layers and their functions.**

There are three layers in ANSI-SPARC:

1. External Level:
This level shows only the relevant part for a user/application and 
excludes unauthorized and irrelevant data.

2. Conceptual Level:
This level shows the whole database with all relations.

3. Internal Level:
This level specifies the physical storage of the data.

### 3. Benefits of databases

A database built according to the ANSI SPARC model provides physical and logical 
data independence. 

**What does this mean?**

Physical independence means that the *Internal Level*, meaning the physical
representation of the data on a storage medium, can be changed without the need
for a change in an application.

Logical independence means that the *Conceptual Level*, meaning the
representation of all data in the DB, can be changed without affecting
applications as long as the *External Level* can still be derived. 


**Which problems from task 1 does this solve?**

It pretty solves the problem of inflexibility outlined in task 1. The logical 
independence provides a lot of flexibility compared to a file based
representation of the data.

### 4. Database lifecycle

**What are the phases of the DB lifecycle and what happens roughly in each 
phase?**

The database lifecycle consists of five phases:

1. Requirements Analysis:
Find out who needs what data and in which quality.

2. Conceptual Design:
Specify the conceptual data model.

3. Logical Design:
Specify the logical data model.

4. Physical Design:
Specify the internal data model.

5. Usage, Maintenance and Reorganization:
Tune and adapt the database.

### 5. Semantic modeling 1

The ornithologists' association 'Buntspecht' would like to learn more about the
population of native birds. Therefore, it calls on interested people to observe
birds once a month for a limited period of time (e.g. for one hour) in a 
self-selected environment (at home, while hiking, etc.). These observations are
to be stored (via a website) in a database. In the requirements analysis, the
following text about the bird domain has been created: 

*People make observations. The **first name**, **surname**, **address** and
**date of birth** of each person should be stored. If available also the 
**TelNr.** and the **eMail**. Some persons are even **members of the 
association.***

*Each observation takes place on a **certain day** (e.g., on 15 February 2022) 
and in a **certain period** (e.g., from 13 to 14 h). The observation takes
place at a certain **Austrian district** and **province** and in a **typical
environment** like, e.g., English garden, natural garden, forest, mountain or
city center. For each environment there is a **short description.***

*Each observation includes **one or more bird species** observed and the 
**number of birds** of that species seen (e.g., an observation on 16 January 
(11-13h) in Klagenfurt/Carinthia includes 2 bluebirds, 14 house sparrows and a
nuthatch).*

*Each bird species has a **name**, a **scientific name** and a **description**.
Some bird species are **migratory birds**. Each bird species includes a **brief
description** and a **link to a website** with more information. Each bird 
species also **belongs to a family** (for example, nuthatches belong to the
Sittidae family).*

**Based on this text, create a semantic data model in the form of a UML class
diagram.**

<img src="/databases/exercise01/uml.svg" alt="" width="50%">

### 6. Semantic modeling 2

**Does your semantic data model from Task 6 include the information needed to do
this and if so, where can they be found?**

The association 'Buntspecht' would like to make the following evaluations, 
among others:

- **All observations with the respective number per observed bird species.**

    List all observations.

- **When and where were there observations in a forest in Carinthia?**

    List all observations and filter them by environment and district.

- **In which environment were the most magpies observed in Carinthia in October?**

    List all observations, filter them by day and district. List all species for
    all those observations and look where the most magpies where observed.

- **How many greenfinches were observed in Klagenfurt in January?**

    List all observations, filter them by day and province and add up all observed
    greenfinches.

- **What is the most observed species group observed in waterfront areas in the
district of Graz?**

    List all observations, filter them by environment and district and add up all
    the amounts for all observed species. Then take the maximum.

- **Which migratory bird species was observed most often in the district of
Villach in May?**

    List all observations, filter them by district and add up all the amounts for 
    every migratory species. Then take the maximum.

- **What is the name of the smallest observed species of Sittidae?**

    List all observations, add up all the amounts for every species which belongs 
    to the family of sittidae. Then find the minimum and return this species.

- **Which persons donated how much to the association last year?**

    List all persons and find the smallest donation.

- **Which individuals observed the most bird species last year?**

    List all persons, add up all the different species in their observations and 
    find the maximum.
