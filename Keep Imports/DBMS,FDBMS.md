[[Keep/Colour/DEFAULT]] [[Keep/Attachments]] [[Keep/Archived]] 

tuple is a one row(one record)
attributes-property or characteristics
relation-the way two or more databases are linked

ACID-Atomicity,Consistency,Isolation,Durability

cursor -as pointer to context area(responsible for holding the rows that have been returned by sql)
trigger -a program which gets automatically executed in response to some events such as modification in db.


The federated database management system is useful while working with multiple applications that uses federation of databases.

There are some issues with the federated database management system. They are −

Managing the difference in data models, while working with federated databases multiple applications can have different type of data models and dealing with these data models using is single language is difficult.

Working with different constraints in data, Databases have multiple constraints on data. Creating a single global schema to work with all constraints is quite difficult.

Difference in Query languages is a big issue while working with federated databases


META DATA-  is a data about the data.Self describing nature of database.



Disadvantages of DBMS
High initial investment in hardware, software, and training


 The generality that a DBMS provides for defining and processing data

 Overhead for providing security, concurrency control, recovery, and integrity functions

Therefore, it may be more desirable to use regular files under the following circum-stances:


 Simple, well-defined database applications that are not expected to change at all



Data abstraction generally refers to the suppression
of details of data organization and storage



Nested queries 
Outer qwery -main qwery
Inner query - subqurry
Independent nested queries(innermost to outermost qwery IN,NULL,ALL) 
correlated nested qwery- when a subquery must return a different results for each main query

The EXISTS condition in SQL is
 used to check whether the result of a correlated nested query is empty (contains no tuples) or not. The result of EXISTS is a boolean value True or False.


EXISTS is used to determine if any values are returned or not. Whereas, IN can be used as a multiple OR operator. If the sub-query result is large, then EXISTS is faster than IN. Once the single positive condition is met in the EXISTS condition then the SQL Engine will stop the process


Partial dependency means that a nonprime attribute is functionally dependent on part of a candidate key. (A nonprime attribute is an attribute that's not part of any candidate key

In Non-trivial functional dependency, the dependent is strictly not a subset of the determinant. i.e. If X → Y and Y is not a subset of X, then it is called Non-trivial functional dependency



1nf -domain should be unique there's should not multi values attributes.

2nf- every nonprime attributes is fully function depend on Prime attributes.

3nf- it is in 2nf and no non prime attributes of r is  transitively dependent on primary key.

BCNF(BOYCE CODD NORMAL FORM)
if it is in 3NF
For every functional dependency X->Y
X should be the super key of the table.(Non trivial fD)

4NF- if it is in Boyce Codd normal form and has no multi-valued dependency.
For a dependency A → B, if for a single value of A, multiple values of B exists, then the relation will be a multi-valued dependency(undesirable MVD )X->>Y ,X IS SUPER KEY

5NF-A relation is in 5NF if it is in 4NF and not contains any join dependency and joining should be lossless.
5NF is satisfied when all the tables are broken into as many tables as possible in order to avoid redundancy.
5NF is also known as Project-join normal form (PJ/NF)




A cursor is a temporary work area created in the system memory when a SQL statement is executed. A cursor contains information on a select statement and the rows of data accessed by it. This temporary work area is used to store the data retrieved from the database, and manipulate this data



n a database, a deadlock is an unwanted situation in which two or more transactions are waiting indefinitely for one another to give up locks. Deadlock is said to be one of the most feared complications in DBMS as it brings the whole system to a Halt.


![[181c5104284.bb7132b5120ba708.jpg]]