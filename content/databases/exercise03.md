+++
title = "Exercise 03"
+++

A new database is to be developed for the WinDBö bakery to support sales, room
and personnel management and marketing. Discussions were held with responsible
persons and future users, and existing information systems were analyzed. The
texts in the tasks summarize the most important requirements for the data to be
stored as a result of the domain analysis. From this, model a semantic data
model in the form of a UML diagram.

### 1.

The database to be developed should contain data on products that the WinDBö
bakery produces itself (e.g. Easter Reindling) or purchases (marzipan
confectionery). In any case, a product has a name and a category (e.g. bread,
cake, pastry, confectionery). Furthermore, it must be possible to store the
production price or the purchase price as well as the gross sales price for each
product. It should also be possible to view the central warehouse stock for the
product in the database. A product contains zero or more ingredients.
Ingredients are only stored in the database if they are contained in at least
one product. The name and allergens of the ingredients are known.

<img src="/databases/exercise03/1.svg" alt="" width="30%" style="margin-left: auto;margin-right: auto;display: block;">

### 2.

WinDBö has several branches all over the country. For each branch, its address
is to be stored in the database. Each branch has a unique branch number. In the
branches the products are stored and sold in a certain quantity. For each sale,
the date of sale and the invoice amount should be recorded. Each branch includes
several rooms. Each room has a size in m2 and a purpose (e.g. sales, guest room,
warehouse, production).

<img src="/databases/exercise03/2.svg" alt="" width="50%" style="margin-left: auto;margin-right: auto;display: block;">

### 3.

A sale includes one or more products in a certain quantity or number, which
represent individual sales items of the sale. A product can be sold more often,
of course (if the stock allows it). Gift baskets are special products consisting
of at least five or more other products. The sales price of a gift basket may
differ from the sum of the sales prices of its components and therefore it must
be stored separately in the DB. Also the weight of the gift basket and the
number of products it contains must be recorded.

<img src="/databases/exercise03/3.svg" alt="" width="70%" style="margin-left: auto;margin-right: auto;display: block;">

### 4.

A sale is always made by an employee of the store. The employee's employee
number, first and last name, date of birth, home address (street, postal code,
city) and gross salary are known. An employee can handle several sales, but some
do not sell anything at all. This depends on the activity of the employee, which
is also stored in the DB. Each employee has to perform exactly one specific
activity. Each employee receives an employee card upon employment. An employee
ID card is assigned to exactly one employee. The card number, authorization and
expiration date are stored on the card. If an employee is deleted from the
system, the employee ID card should also be deleted.

<img src="/databases/exercise03/4.svg" alt="" width="90%" style="margin-left: auto;margin-right: auto;display: block;">

### 5.

Sometimes the customer of a sale is also known and should be saved. These
regular customers have a customer card with a customer number and are credited
with bonus points for each purchase, which should be stored. From regular
customers, in any case, the unique customer number, the first and last name, the
address and the date of birth is known. Sometimes also an e-mail, a Tel.Nr. and
their consent to send the customer a newsletter is to be stored.

<img src="/databases/exercise03/5.svg" alt="" width="100%" style="margin-left: auto;margin-right: auto;display: block;">

### 6.

Sometimes employees also receive a commission for the sales they make. An
employee works in one branch at one time, but can also be employed by different
branches over time. This temporal development is to be stored in the DB. At
least one, but possibly several employees work in a branch. Employees can have
superiors. Supervisors may have no employees or several employees. The bakery
has company cell phones, from which the model and phone number must be stored.
Some employees are provided with a company cell phone, but not all are. This
should be managed with the help of the database.

<img src="/databases/exercise03/6.svg" alt="" width="100%" style="margin-left: auto;margin-right: auto;display: block;">

### 7.

Provide 5 queries of interest to the bakery's marketing that can be answered
based on their semantic data model of the bakery (e.g., which products of the
category 'cake' were sold in store F in March 2022 in a quantity above 5
pieces?).

- Total invoice amount of all sales with customers who want to get the
  newsletter.
- All branches in which the employee 'John Doe' has ever worked in and sold a
  product for which he got a commission.
- The names of all the supervisors who supervise employees which have an expired
  card.
- The average gross salary of employees with a company cellphone who have worked
  in at least 2 other branches before.
- The total quantity of products sold by all employees supervised by 'John Doe'.
