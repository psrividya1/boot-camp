**List available databases:**

show databases;

**The general command for creating a database:**

CREATE DATABASE database\_name;

` `Eg., CREATE DATABASE employees;

**To drop a database:**

DROP DATABASE database\_name;

Eg.,DROP DATABASE hello\_world\_db;

**Tells the currently used database:**

SELECT database();

**Creating Tables:**

CREATE TABLE tablename

` `(

`  `column\_name data\_type,

`   `column\_name data\_type

` `);

Eg.,

CREATE TABLE cats

(

` `name VARCHAR(100),

` `age INT

` `);

**To show tables in database:**

SHOW TABLES;

**To show columns of a particular table:** 

SHOW COLUMNS FROM tablename;

` `DESC tablename;

**Dropping tables**:

DROP TABLE <tablename>;

Eg., DROP TABLE cats;
#### **Inserting Data:**

The "formula":

INSERT INTO table\_name(column\_name) VALUES (data);

For example:

INSERT INTO cats(name, age) VALUES ('Jetson', 7);

**SELECT:**

SELECT \* FROM <table name>;

**MULTIPLE INSERT:**

INSERT INTO table\_name 

`  		 `(column\_name, column\_name) 

VALUES	 (value, value), 

` `(value, value), 

` `(value, value);

**Inserting a cat with incorrect data types**:

INSERT INTO cats(name, age) VALUES('Lima', 'dsfasdfdas'); 

Try Inserting a cat with a super long name:

Then view the warning:

**SHOW WARNINGS;**
#### *NULL and NOT NULL Code*
Try inserting a cat without an age:

INSERT INTO cats(name) VALUES('Alabama'); 

SELECT \* FROM cats; 

Try inserting a nameless and ageless cat:

INSERT INTO cats() VALUES(); 

Define a new cats2 table with NOT NULL constraints:




- CREATE TABLE cats2
- ` `(
- `   `name VARCHAR(100) NOT NULL,
- `   `age INT NOT NULL
- ` `);

DESC cats2; 

Now try inserting an ageless cat:

INSERT INTO cats2(name) VALUES('Texas'); 

**View the new warnings:**

SHOW WARNINGS; 

SELECT \* FROM cats2; 

Do the same for a nameless cat:

INSERT INTO cats2(age) VALUES(7); 

SHOW WARNINGS; 
#### Setting Default Values 
Define a table with a DEFAULT name specified:

- CREATE TABLE cats3
- ` `(
- `   `name VARCHAR(20) DEFAULT 'no name provided',
- `   `age INT DEFAULT 99
- ` `);

Notice the change when you describe the table:

DESC cats3; 

Insert a cat without a name:

INSERT INTO cats3(age) VALUES(13); 

Or a nameless, ageless cat:

INSERT INTO cats3() VALUES(); 

Combine NOT NULL and DEFAULT:

- CREATE TABLE cats4
- ` `(
- `   `name VARCHAR(20) NOT NULL DEFAULT 'unnamed',
- `   `age INT NOT NULL DEFAULT 99
- ` `);


Notice The Difference:

- INSERT INTO cats() VALUES();
 
- SELECT \* FROM cats;
 
- INSERT INTO cats3() VALUES();
 
- SELECT \* FROM cats3;
 
- INSERT INTO cats3(name, age) VALUES('Montana', NULL);
 
- SELECT \* FROM cats3;
 
- INSERT INTO cats4(name, age) VALUES('Cali', NULL);

**A Primer on Primary Keys**
####
Define a table with a PRIMARY KEY constraint:

- CREATE TABLE unique\_cats
- ` `(
- `   `cat\_id INT NOT NULL,
- `   `name VARCHAR(100),
- `   `age INT,
- `   `PRIMARY KEY (cat\_id)
- ` `);

DESC unique\_cats; 

Insert some new cats:

- INSERT INTO unique\_cats(cat\_id, name, age) VALUES(1, 'Fred', 23);
 
- INSERT INTO unique\_cats(cat\_id, name, age) VALUES(2, 'Louise', 3);
 
- INSERT INTO unique\_cats(cat\_id, name, age) VALUES(1, 'James', 3);

Notice what happens:

SELECT \* FROM unique\_cats; 

Adding in AUTO\_INCREMENT:

- CREATE TABLE unique\_cats2 (
- `   `cat\_id INT NOT NULL AUTO\_INCREMENT,
- `   `name VARCHAR(100),
- `   `age INT,
- `   `PRIMARY KEY (cat\_id)
- );

INSERT a couple new cats:

- INSERT INTO unique\_cats2(name, age) VALUES('Skippy', 4);
- INSERT INTO unique\_cats2(name, age) VALUES('Jiff', 3);
- INSERT INTO unique\_cats2(name, age) VALUES('Jiff', 3);
- INSERT INTO unique\_cats2(name, age) VALUES('Jiff', 3);
- INSERT INTO unique\_cats2(name, age) VALUES('Skippy', 4);

Notice the difference:

SELECT \* FROM unique\_cats2;

**Introduction to CRUD**

INSERT INTO cats(name, age) VALUES(‘Taco’, 14);

**Preparing Our Data**

Let's drop the existing cats table:

DROP TABLE cats; 

Recreate a new cats table:

- CREATE TABLE cats 
- ` `( 
- `    `cat\_id INT NOT NULL AUTO\_INCREMENT, 
- `    `name   VARCHAR(100), 
- `    `breed  VARCHAR(100), 
- `    `age    INT, 
- `    `PRIMARY KEY (cat\_id) 
- ` `); 

DESC cats; 

And finally insert some new cats:

- INSERT INTO cats(name, breed, age) 
- VALUES ('Ringo', 'Tabby', 4),
- `      `('Cindy', 'Maine Coon', 10),
- `      `('Dumbledore', 'Maine Coon', 11),
- `      `('Egg', 'Persian', 4),
- `      `('Misty', 'Tabby', 13),
- `      `('George Michael', 'Ragdoll', 9),
- `      `('Jackson', 'Sphynx', 7);

#### ***Various Simple SELECT statements:***
SELECT \* FROM cats; 

SELECT name FROM cats; 

SELECT age FROM cats; 

SELECT cat\_id FROM cats; 

SELECT name, age FROM cats; 

SELECT cat\_id, name, age FROM cats; 

SELECT age, breed, name, cat\_id FROM cats; 

SELECT cat\_id, name, age, breed FROM cats;

**Introduction to WHERE**

Select by age:

SELECT \* FROM cats WHERE age=4; 

Select by name:

SELECT \* FROM cats WHERE name='Egg'; 

Notice how it deals with case:

SELECT \* FROM cats WHERE name='egG';

**Introduction to Aliases**

SELECT cat\_id AS id, name FROM cats;

SELECT name AS 'cat name', breed AS 'kitty breed' FROM cats;

DESC cats;

**The UPDATE Command**

Change tabby cats to shorthair:

UPDATE cats SET breed='Shorthair' WHERE breed='Tabby'; 

Another update:

UPDATE cats SET age=14 WHERE name='Misty';

**Introduction to DELETE**

DELETE FROM cats WHERE name='Egg';

SELECT \* FROM cats;

SELECT \* FROM cats WHERE name='egg';

DELETE FROM cats WHERE name='egg';

SELECT \* FROM cats;

DELETE FROM cats;

**Running SQL Files**

CREATE TABLE cats

`   `(

`       `cat\_id INT NOT NULL AUTO\_INCREMENT,

`       `name VARCHAR(100),

`       `age INT,

`       `PRIMARY KEY(cat\_id)

`   `);



mysql-ctl cli

use cat\_app;

source first\_file.sql

DESC cats;



INSERT INTO cats(name, age)

VALUES('Charlie', 17);

INSERT INTO cats(name, age)

VALUES('Connie', 10);

SELECT \* FROM cats; 

source testing/insert.sql

**Loading Our Book Data**

\1. First create your book\_data.sql file with the following code:

- DROP DATABASE IF EXISTS book\_shop;
- CREATE DATABASE book\_shop;
- USE book\_shop; 

- CREATE TABLE books 
- (
- book\_id INT NOT NULL AUTO\_INCREMENT,
- title VARCHAR(100),
- author\_fname VARCHAR(100),
- author\_lname VARCHAR(100),
- released\_year INT,
- stock\_quantity INT,
- pages INT,
- PRIMARY KEY(book\_id)
- );

- INSERT INTO books (title, author\_fname, author\_lname, released\_year, stock\_quantity, pages)
- VALUES
- ('The Namesake', 'Jhumpa', 'Lahiri', 2003, 32, 291),
- ('Norse Mythology', 'Neil', 'Gaiman',2016, 43, 304),
- ('American Gods', 'Neil', 'Gaiman', 2001, 12, 465),
- ('Interpreter of Maladies', 'Jhumpa', 'Lahiri', 1996, 97, 198),
- ('A Hologram for the King: A Novel', 'Dave', 'Eggers', 2012, 154, 352),
- ('The Circle', 'Dave', 'Eggers', 2013, 26, 504),
- ('The Amazing Adventures of Kavalier & Clay', 'Michael', 'Chabon', 2000, 68, 634),
- ('Just Kids', 'Patti', 'Smith', 2010, 55, 304),
- ('A Heartbreaking Work of Staggering Genius', 'Dave', 'Eggers', 2001, 104, 437),
- ('Coraline', 'Neil', 'Gaiman', 2003, 100, 208),
- ('What We Talk About When We Talk About Love: Stories', 'Raymond', 'Carver', 1981, 23, 176),
- ("Where I'm Calling From: Selected Stories", 'Raymond', 'Carver', 1989, 12, 526),
- ('White Noise', 'Don', 'DeLillo', 1985, 49, 320),
- ('Cannery Row', 'John', 'Steinbeck', 1945, 95, 181),
- ('Oblivion: Stories', 'David', 'Foster Wallace', 2004, 172, 329),
- ('Consider the Lobster', 'David', 'Foster Wallace', 2005, 92, 343);

\2. Then source that file
source book\_data.sql 

\3. Now check your work:

- DESC books;
- SELECT \* FROM books;

**Working With CONCAT**

- SELECT author\_fname, author\_lname FROM books;
 
- CONCAT(x,y,z) // from slides
 
- CONCAT(column, anotherColumn) // from slides
 
- CONCAT(author\_fname, author\_lname)
 
- CONCAT(column, 'text', anotherColumn, 'more text')
 
- CONCAT(author\_fname, ' ', author\_lname)
 
- CONCAT(author\_fname, author\_lname); // invalid syntax
 
- SELECT CONCAT('Hello', 'World');
 
- SELECT CONCAT('Hello', '...', 'World');
 
- SELECT
- ` `CONCAT(author\_fname, ' ', author\_lname)
- FROM books;
 
- SELECT
- ` `CONCAT(author\_fname, ' ', author\_lname)
- ` `AS 'full name'
- FROM books;
 
- SELECT author\_fname AS first, author\_lname AS last, 
- ` `CONCAT(author\_fname, ' ', author\_lname) AS full
- FROM books;
 
- SELECT author\_fname AS first, author\_lname AS last, 
- ` `CONCAT(author\_fname, ', ', author\_lname) AS full
- FROM books;
 
- SELECT CONCAT(title, '-', author\_fname, '-', author\_lname) FROM books;
 
- SELECT 
- `   `CONCAT\_WS(' - ', title, author\_fname, author\_lname) 
- FROM books;

**Introducing SUBSTRING**

- SELECT SUBSTRING('Hello World', 1, 4);
 
- SELECT SUBSTRING('Hello World', 7);
 
- SELECT SUBSTRING('Hello World', 3, 8);
 
- SELECT SUBSTRING('Hello World', 3);
 
- SELECT SUBSTRING('Hello World', -3);
 
- SELECT SUBSTRING('Hello World', -7);
 
- SELECT title FROM books;
 
- SELECT SUBSTRING("Where I'm Calling From: Selected Stories", 1, 10);
 
- SELECT SUBSTRING(title, 1, 10) FROM books;
 
- SELECT SUBSTRING(title, 1, 10) AS 'short title' FROM books;
 
- SELECT SUBSTR(title, 1, 10) AS 'short title' FROM books;
 
- SELECT CONCAT
- `    `(
- `        `SUBSTRING(title, 1, 10),
- `        `'...'
- `    `)
- FROM books;
 
- source book\_code.sql
 
- SELECT CONCAT
- `    `(
- `        `SUBSTRING(title, 1, 10),
- `        `'...'
- `    `) AS 'short title'
- FROM books;
 
- source book\_code.sql

**Introducing REPLACE**

- SELECT REPLACE('Hello World', 'Hell', '%$#@');
 
- SELECT REPLACE('Hello World', 'l', '7');
 
- SELECT REPLACE('Hello World', 'o', '0');
 
- SELECT REPLACE('HellO World', 'o', '\*');
 
- SELECT
- ` `REPLACE('cheese bread coffee milk', ' ', ' and ');
 
- SELECT REPLACE(title, 'e ', '3') FROM books;
 
- -- SELECT
- --    CONCAT
- --    (
- --        SUBSTRING(title, 1, 10),
- --        '...'
- --    ) AS 'short title'
- -- FROM books;
 
- SELECT
- `   `SUBSTRING(REPLACE(title, 'e', '3'), 1, 10)
- FROM books;
 
- SELECT
- `   `SUBSTRING(REPLACE(title, 'e', '3'), 1, 10) AS 'weird string'
- FROM books;

**Using REVERSE**

- SELECT REVERSE('Hello World');
 
- SELECT REVERSE('meow meow');
 
- SELECT REVERSE(author\_fname) FROM books;
 
- SELECT CONCAT('woof', REVERSE('woof'));
 
- SELECT CONCAT(author\_fname, REVERSE(author\_fname)) FROM books;

**Working with CHAR LENGTH**

- SELECT CHAR\_LENGTH('Hello World');
 
- SELECT author\_lname, CHAR\_LENGTH(author\_lname) AS 'length' FROM books;
 
- SELECT CONCAT(author\_lname, ' is ', CHAR\_LENGTH(author\_lname), ' characters long') FROM boo

**Changing Case with UPPER and LOWER**

- SELECT UPPER('Hello World');
 
- SELECT LOWER('Hello World');
 
- SELECT UPPER(title) FROM books;
 
- SELECT CONCAT('MY FAVORITE BOOK IS ', UPPER(title)) FROM books;
 
- SELECT CONCAT('MY FAVORITE BOOK IS ', LOWER(title)) FROM books;

**Note about string functions**

This works:

- SELECT UPPER(CONCAT(author\_fname, ' ', author\_lname)) AS "full name in caps"
- FROM books;

While this does not:

- SELECT CONCAT(UPPER(author\_fname, ' ', author\_lname)) AS "full name in caps" 
- FROM books;

UPPER only takes one argument and CONCAT takes two or more arguments, so they can't be switched in that way.

You could do it this way, however:

- SELECT CONCAT(UPPER(author\_fname), ' ', UPPER(author\_lname)) AS "full name in caps" 
- FROM books;

**Seed Data: Adding A Couple New Books**

- INSERT INTO books
- `   `(title, author\_fname, author\_lname, released\_year, stock\_quantity, pages)
- `   `VALUES ('10% Happier', 'Dan', 'Harris', 2014, 29, 256), 
- `          `('fake\_book', 'Freida', 'Harris', 2001, 287, 428),
- `          `('Lincoln In The Bardo', 'George', 'Saunders', 2017, 1000, 367);
 
 
- SELECT title FROM books;

**Using DISTINCT**

- SELECT author\_lname FROM books;
 
- SELECT DISTINCT author\_lname FROM books;
 
- SELECT author\_fname, author\_lname FROM books;
 
- SELECT DISTINCT CONCAT(author\_fname,' ', author\_lname) FROM books;
 
- SELECT DISTINCT author\_fname, author\_lname FROM books;

**Sorting Data with ORDER BY**

- SELECT author\_lname FROM books;
 
- SELECT author\_lname FROM books ORDER BY author\_lname;
 
- SELECT title FROM books;
 
- SELECT title FROM books ORDER BY title;
- SELECT author\_lname FROM books ORDER BY author\_lname DESC;
 
- SELECT released\_year FROM books;
 
- SELECT released\_year FROM books ORDER BY released\_year;
 
- SELECT released\_year FROM books ORDER BY released\_year DESC;
 
- SELECT released\_year FROM books ORDER BY released\_year ASC;
 
- SELECT title, released\_year, pages FROM books ORDER BY released\_year;
 
- SELECT title, pages FROM books ORDER BY released\_year;
 
- SELECT title, author\_fname, author\_lname 
- FROM books ORDER BY 2;
 
- SELECT title, author\_fname, author\_lname 
- FROM books ORDER BY 3;
 
- SELECT title, author\_fname, author\_lname 
- FROM books ORDER BY 1;
 
- SELECT title, author\_fname, author\_lname 
- FROM books ORDER BY 1 DESC;
 
- SELECT author\_lname, title
- FROM books ORDER BY 2;
 
- SELECT author\_fname, author\_lname FROM books 
- ORDER BY author\_lname, author\_fname;

**Using LIMIT**

- SELECT title FROM books LIMIT 3;
 
- SELECT title FROM books LIMIT 1;
 
- SELECT title FROM books LIMIT 10;
 
- SELECT \* FROM books LIMIT 1;
 
- SELECT title, released\_year FROM books 
- ORDER BY released\_year DESC LIMIT 5;
 
- SELECT title, released\_year FROM books 
- ORDER BY released\_year DESC LIMIT 1;
 
- SELECT title, released\_year FROM books 
- ORDER BY released\_year DESC LIMIT 14;
 
- SELECT title, released\_year FROM books 
- ORDER BY released\_year DESC LIMIT 0,5;
 
- SELECT title, released\_year FROM books 
- ORDER BY released\_year DESC LIMIT 0,3;
 
- SELECT title, released\_year FROM books 
- ORDER BY released\_year DESC LIMIT 1,3;
 
- SELECT title, released\_year FROM books 
- ORDER BY released\_year DESC LIMIT 10,1;
 
- SELECT \* FROM tbl LIMIT 95,18446744073709551615;
 
- SELECT title FROM books LIMIT 5;
 
- SELECT title FROM books LIMIT 5, 123219476457;

- SELECT title FROM books LIMIT 5, 50;

**Better Searches with LIKE**

- SELECT title, author\_fname FROM books WHERE author\_fname LIKE '%da%';



- SELECT title, author\_fname FROM books WHERE author\_fname LIKE 'da%';



- SELECT title FROM books WHERE  title LIKE 'the';



- SELECT title FROM books WHERE  title LIKE '%the';



- SELECT title FROM books WHERE title LIKE '%the%';

**More Wildcards**

- SELECT title, stock\_quantity FROM books;

- SELECT title, stock\_quantity FROM books WHERE stock\_quantity LIKE '\_\_\_\_';

- SELECT title, stock\_quantity FROM books WHERE stock\_quantity LIKE '\_\_';

- (235)234-0987 LIKE '(\_\_\_)\_\_\_-\_\_\_\_'



- SELECT title FROM books;



- SELECT title FROM books WHERE title LIKE '%\%%'



- SELECT title FROM books WHERE title LIKE '%\\_%'

**The Count Function**

- SELECT COUNT(\*) FROM books;



- SELECT COUNT(author\_fname) FROM books;



- SELECT COUNT(DISTINCT author\_fname) FROM books;



- SELECT COUNT(DISTINCT author\_lname) FROM books;



- SELECT COUNT(DISTINCT author\_lname, author\_fname) FROM books;



- SELECT title FROM books WHERE title LIKE '%the%';



- SELECT COUNT(\*) FROM books WHERE title LIKE '%the%';

**The Joys of Group By**

- SELECT title, author\_lname FROM books;

- SELECT title, author\_lname FROM books
- GROUP BY author\_lname;



- SELECT author\_lname, COUNT(\*) 
- FROM books GROUP BY author\_lname;





- SELECT title, author\_fname, author\_lname FROM books;

- SELECT title, author\_fname, author\_lname FROM books GROUP BY author\_lname;



- SELECT author\_fname, author\_lname, COUNT(\*) FROM books GROUP BY author\_lname;



- SELECT author\_fname, author\_lname, COUNT(\*) FROM books GROUP BY author\_lname, author\_fname;

- SELECT released\_year FROM books;

- SELECT released\_year, COUNT(\*) FROM books GROUP BY released\_year;



- SELECT CONCAT('In ', released\_year, ' ', COUNT(\*), ' book(s) released') AS year FROM books GROUP BY released\_year;




**MIN and MAX Basics**

- SELECT MIN(released\_year) 
- FROM books;
 
- SELECT MIN(released\_year) FROM books;
 
- SELECT MIN(pages) FROM books;
 
- SELECT MAX(pages) 
- FROM books;



- SELECT MAX(released\_year) 
- FROM books;
 
- SELECT MAX(pages), title
- FROM books;




**A Problem with Min and Max**

- SELECT \* FROM books 
- WHERE pages = (SELECT Min(pages) 
- `               `FROM books); 



- SELECT title, pages FROM books 
- WHERE pages = (SELECT Max(pages) 
- `               `FROM books); 



- SELECT title, pages FROM books 
- WHERE pages = (SELECT Min(pages) 
- `               `FROM books); 



- SELECT \* FROM books 
- ORDER BY pages ASC LIMIT 1;

- SELECT title, pages FROM books 
- ORDER BY pages ASC LIMIT 1;

- SELECT \* FROM books 
- ORDER BY pages DESC LIMIT 1;

**Using Min and Max with Group By**

- SELECT author\_fname, 
- `      `author\_lname, 
- `      `Min(released\_year) 
- FROM   books 
- GROUP  BY author\_lname, 
- `         `author\_fname;



- SELECT
- ` `author\_fname,
- ` `author\_lname,
- ` `Max(pages)
- FROM books
- GROUP BY author\_lname,
- `        `author\_fname;



- SELECT
- ` `CONCAT(author\_fname, ' ', author\_lname) AS author,
- ` `MAX(pages) AS 'longest book'
- FROM books
- GROUP BY author\_lname,
- `        `author\_fname;

**The Sum Function**

- SELECT SUM(pages)
- FROM books;



- SELECT SUM(released\_year) FROM books;



- SELECT author\_fname,
- `      `author\_lname,
- `      `Sum(pages)
- FROM books
- GROUP BY
- `   `author\_lname,
- `   `author\_fname;



- SELECT author\_fname,
- `      `author\_lname,
- `      `Sum(released\_year)
- FROM books
- GROUP BY
- `   `author\_lname,
- `   `author\_fname;

**The Avg Function**

- SELECT AVG(released\_year) 
- FROM books;



- SELECT AVG(pages) 
- FROM books;



- SELECT AVG(stock\_quantity) 
- FROM books 
- GROUP BY released\_year;



- SELECT released\_year, AVG(stock\_quantity) 
- FROM books 
- GROUP BY released\_year;



- SELECT author\_fname, author\_lname, AVG(pages) FROM books
- GROUP BY author\_lname, author\_fname;

**CHAR and VARCHAR**

- CREATE TABLE dogs (name CHAR(5), breed VARCHAR(10));



- INSERT INTO dogs (name, breed) VALUES ('bob', 'beagle');



- INSERT INTO dogs (name, breed) VALUES ('robby', 'corgi');



- INSERT INTO dogs (name, breed) VALUES ('Princess Jane', 'Retriever');



- SELECT \* FROM dogs;



- INSERT INTO dogs (name, breed) VALUES ('Princess Jane', 'Retrievesadfdsafdasfsafr');



- SELECT \* FROM dogs;

**DECIMAL**

- CREATE TABLE items(price DECIMAL(5,2));



- INSERT INTO items(price) VALUES(7);



- INSERT INTO items(price) VALUES(7987654);



- INSERT INTO items(price) VALUES(34.88);



- INSERT INTO items(price) VALUES(298.9999);



- INSERT INTO items(price) VALUES(1.9999);

- SELECT \* FROM items;

**FLOAT and DOUBLE**

- CREATE TABLE thingies (price FLOAT);



- INSERT INTO thingies(price) VALUES (88.45);



- SELECT \* FROM thingies;



- INSERT INTO thingies(price) VALUES (8877.45);



- SELECT \* FROM thingies;



- INSERT INTO thingies(price) VALUES (8877665544.45);



- SELECT \* FROM thingies;

**Creating Our DATE data**

- CREATE TABLE people (name VARCHAR(100), birthdate DATE, birthtime TIME, birthdt DATETIME);



- INSERT INTO people (name, birthdate, birthtime, birthdt)
- VALUES('Padma', '1983-11-11', '10:07:35', '1983-11-11 10:07:35');



- INSERT INTO people (name, birthdate, birthtime, birthdt)
- VALUES('Larry', '1943-12-25', '04:10:42', '1943-12-25 04:10:42');

- SELECT \* FROM people;

**Formatting Dates**

- SELECT name, birthdate FROM people;



- SELECT name, DAY(birthdate) FROM people;



- SELECT name, birthdate, DAY(birthdate) FROM people;



- SELECT name, birthdate, DAYNAME(birthdate) FROM people;



- SELECT name, birthdate, DAYOFWEEK(birthdate) FROM people;



- SELECT name, birthdate, DAYOFYEAR(birthdate) FROM people;



- SELECT name, birthtime, DAYOFYEAR(birthtime) FROM people;



- SELECT name, birthdt, DAYOFYEAR(birthdt) FROM people;



- SELECT name, birthdt, MONTH(birthdt) FROM people;



- SELECT name, birthdt, MONTHNAME(birthdt) FROM people;



- SELECT name, birthtime, HOUR(birthtime) FROM people;



- SELECT name, birthtime, MINUTE(birthtime) FROM people;



- SELECT CONCAT(MONTHNAME(birthdate), ' ', DAY(birthdate), ' ', YEAR(birthdate)) FROM people;



- SELECT DATE\_FORMAT(birthdt, 'Was born on a %W') FROM people;



- SELECT DATE\_FORMAT(birthdt, '%m/%d/%Y') FROM people;



- SELECT DATE\_FORMAT(birthdt, '%m/%d/%Y at %h:%i') FROM people;

**Date Math**

- SELECT \* FROM people;



- SELECT DATEDIFF(NOW(), birthdate) FROM people;



- SELECT name, birthdate, DATEDIFF(NOW(), birthdate) FROM people;



- SELECT birthdt FROM people;



- SELECT birthdt, DATE\_ADD(birthdt, INTERVAL 1 MONTH) FROM people;



- SELECT birthdt, DATE\_ADD(birthdt, INTERVAL 10 SECOND) FROM people;



- SELECT birthdt, DATE\_ADD(birthdt, INTERVAL 3 QUARTER) FROM people;



- SELECT birthdt, birthdt + INTERVAL 1 MONTH FROM people;



- SELECT birthdt, birthdt - INTERVAL 5 MONTH FROM people;

- SELECT birthdt, birthdt + INTERVAL 15 MONTH + INTERVAL 10 HOUR FROM people;

**Working with TIMESTAMPS**

- CREATE TABLE comments (
- `   `content VARCHAR(100),
- `   `created\_at TIMESTAMP DEFAULT NOW()
- );

- INSERT INTO comments (content) VALUES('lol what a funny article');



- INSERT INTO comments (content) VALUES('I found this offensive');



- INSERT INTO comments (content) VALUES('Ifasfsadfsadfsad');



- SELECT \* FROM comments ORDER BY created\_at DESC;



- CREATE TABLE comments2 (
- `   `content VARCHAR(100),
- `   `changed\_at TIMESTAMP DEFAULT NOW() ON UPDATE CURRENT\_TIMESTAMP
- );



- INSERT INTO comments2 (content) VALUES('dasdasdasd');



- INSERT INTO comments2 (content) VALUES('lololololo');



- INSERT INTO comments2 (content) VALUES('I LIKE CATS AND DOGS');



- UPDATE comments2 SET content='THIS IS NOT GIBBERISH' WHERE content='dasdasdasd';



- SELECT \* FROM comments2;



- SELECT \* FROM comments2 ORDER BY changed\_at;

- CREATE TABLE comments2 (
- `   `content VARCHAR(100),
- `   `changed\_at TIMESTAMP DEFAULT NOW() ON UPDATE NOW()
- );

**Not Equal**

- SELECT title FROM books WHERE released\_year = 2017;

- SELECT title FROM books WHERE released\_year != 2017;



- SELECT title, author\_lname FROM books;



- SELECT title, author\_lname FROM books WHERE author\_lname = 'Harris';



- SELECT title, author\_lname FROM books WHERE author\_lname != 'Harris';

**Not Like**

- SELECT title FROM books WHERE title LIKE 'W';

- SELECT title FROM books WHERE title LIKE 'W%';



- SELECT title FROM books WHERE title LIKE '%W%';



- SELECT title FROM books WHERE title LIKE 'W%';



- SELECT title FROM books WHERE title NOT LIKE 'W%';

**Greater Than**

- SELECT title, released\_year FROM books ORDER BY released\_year;

- SELECT title, released\_year FROM books 
- WHERE released\_year > 2000 ORDER BY released\_year;



- SELECT title, released\_year FROM books 
- WHERE released\_year >= 2000 ORDER BY released\_year;

- SELECT title, stock\_quantity FROM books;

- SELECT title, stock\_quantity FROM books WHERE stock\_quantity >= 100;

- SELECT 99 > 1;

- SELECT 99 > 567;



- SELECT title, author\_lname FROM books WHERE author\_lname = 'Eggers';

- SELECT title, author\_lname FROM books WHERE author\_lname = 'eggers';

- SELECT title, author\_lname FROM books WHERE author\_lname = 'eGGers';

**Less Than**

- SELECT title, released\_year FROM books;

- SELECT title, released\_year FROM books
- WHERE released\_year < 2000;

- SELECT title, released\_year FROM books
- WHERE released\_year <= 2000;

**Logical AND**

- SELECT title, author\_lname, released\_year FROM books
- WHERE author\_lname='Eggers';



- SELECT title, author\_lname, released\_year FROM books
- WHERE released\_year > 2010;

- SELECT  
- `   `title, 
- `   `author\_lname, 
- `   `released\_year FROM books
- WHERE author\_lname='Eggers' 
- `   `AND released\_year > 2010;

- SELECT 1 < 5 && 7 = 9;
- -- false

- SELECT -10 > -20 && 0 <= 0;
- -- true

- SELECT -40 <= 0 AND 10 > 40;
- --false

- SELECT 54 <= 54 && 'a' = 'A';
- -- true

- SELECT \* 
- FROM books
- WHERE author\_lname='Eggers' 
- `   `AND released\_year > 2010 
- `   `AND title LIKE '%novel%';

**Logical OR**

- SELECT 
- `   `title, 
- `   `author\_lname, 
- `   `released\_year 
- FROM books
- WHERE author\_lname='Eggers' || released\_year > 2010;


- SELECT 40 <= 100 || -2 > 0;
- -- true

- SELECT 10 > 5 || 5 = 5;
- -- true

- SELECT 'a' = 5 || 3000 > 2000;
- -- true

- SELECT title, 
- `      `author\_lname, 
- `      `released\_year, 
- `      `stock\_quantity 
- FROM   books 
- WHERE  author\_lname = 'Eggers' 
- `             `|| released\_year > 2010 
- OR     stock\_quantity > 100;

**Between**

- SELECT title, released\_year FROM books WHERE released\_year >= 2004 && released\_year <= 2015;

- SELECT title, released\_year FROM books 
- WHERE released\_year BETWEEN 2004 AND 2015;

- SELECT title, released\_year FROM books 
- WHERE released\_year NOT BETWEEN 2004 AND 2015;

- SELECT CAST('2017-05-02' AS DATETIME);

- show databases;

- use new\_testing\_db;

- SELECT name, birthdt FROM people WHERE birthdt BETWEEN '1980-01-01' AND '2000-01-01';

- SELECT 
- `   `name, 
- `   `birthdt 
- FROM people
- WHERE 
- `   `birthdt BETWEEN CAST('1980-01-01' AS DATETIME)
- `   `AND CAST('2000-01-01' AS DATETIME);

**In And Not In**

- show databases();
- use book\_shop;

- SELECT 
- `   `title, 
- `   `author\_lname 
- FROM books
- WHERE author\_lname='Carver' OR
- `     `author\_lname='Lahiri' OR
- `     `author\_lname='Smith';

- SELECT title, author\_lname FROM books
- WHERE author\_lname IN ('Carver', 'Lahiri', 'Smith');

- SELECT title, released\_year FROM books
- WHERE released\_year IN (2017, 1985);

- SELECT title, released\_year FROM books
- WHERE released\_year != 2000 AND
- `     `released\_year != 2002 AND
- `     `released\_year != 2004 AND
- `     `released\_year != 2006 AND
- `     `released\_year != 2008 AND
- `     `released\_year != 2010 AND
- `     `released\_year != 2012 AND
- `     `released\_year != 2014 AND
- `     `released\_year != 2016;

- SELECT title, released\_year FROM books
- WHERE released\_year NOT IN 
- (2000,2002,2004,2006,2008,2010,2012,2014,2016);

- SELECT title, released\_year FROM books
- WHERE released\_year >= 2000
- AND released\_year NOT IN 
- (2000,2002,2004,2006,2008,2010,2012,2014,2016);

- SELECT title, released\_year FROM books
- WHERE released\_year >= 2000 AND
- released\_year % 2 != 0;

- SELECT title, released\_year FROM books
- WHERE released\_year >= 2000 AND
- released\_year % 2 != 0 ORDER BY released\_year;

**Case Statements**

- SELECT title, released\_year,
- `      `CASE 
- `        `WHEN released\_year >= 2000 THEN 'Modern Lit'
- `        `ELSE '20th Century Lit'
- `      `END AS GENRE
- FROM books;

- SELECT title, stock\_quantity,
- `   `CASE 
- `       `WHEN stock\_quantity BETWEEN 0 AND 50 THEN '\*'
- `       `WHEN stock\_quantity BETWEEN 51 AND 100 THEN '\*\*'
- `       `ELSE '\*\*\*'
- `   `END AS STOCK
- FROM books;

- SELECT title,
- `   `CASE 
- `       `WHEN stock\_quantity BETWEEN 0 AND 50 THEN '\*'
- `       `WHEN stock\_quantity BETWEEN 51 AND 100 THEN '\*\*'
- `       `ELSE '\*\*\*'
- `   `END AS STOCK
- FROM books;

- SELECT title, stock\_quantity,
- `   `CASE 
- `       `WHEN stock\_quantity BETWEEN 0 AND 50 THEN '\*'
- `       `WHEN stock\_quantity BETWEEN 51 AND 100 THEN '\*\*'
- `       `WHEN stock\_quantity BETWEEN 101 AND 150 THEN '\*\*\*'
- `       `ELSE '\*\*\*\*'
- `   `END AS STOCK
- FROM books;

- SELECT title, stock\_quantity,
- `   `CASE 
- `       `WHEN stock\_quantity <= 50 THEN '\*'
- `       `WHEN stock\_quantity <= 100 THEN '\*\*'
- `       `ELSE '\*\*\*'
- `   `END AS STOCK
- FROM books;

**Working With Foreign Keys**

**-- Creating the customers and orders tables**

- CREATE TABLE customers(
- `   `id INT AUTO\_INCREMENT PRIMARY KEY,
- `   `first\_name VARCHAR(100),
- `   `last\_name VARCHAR(100),
- `   `email VARCHAR(100)
- );

- CREATE TABLE orders(
- `   `id INT AUTO\_INCREMENT PRIMARY KEY,
- `   `order\_date DATE,
- `   `amount DECIMAL(8,2),
- `   `customer\_id INT,
- `   `FOREIGN KEY(customer\_id) REFERENCES customers(id)
- );

**-- Inserting some customers and orders**

- INSERT INTO customers (first\_name, last\_name, email) 
- VALUES ('Boy', 'George', '<george@gmail.com>'),
- `      `('George', 'Michael', '<gm@gmail.com>'),
- `      `('David', 'Bowie', '<david@gmail.com>'),
- `      `('Blue', 'Steele', '<blue@gmail.com>'),
- `      `('Bette', 'Davis', '<bette@aol.com>');

- INSERT INTO orders (order\_date, amount, customer\_id)
- VALUES ('2016/02/10', 99.99, 1),
- `      `('2017/11/11', 35.50, 1),
- `      `('2014/12/12', 800.67, 2),
- `      `('2015/01/03', 12.50, 2),
- `      `('1999/04/11', 450.25, 5);


-- This INSERT fails because of our fk constraint.  No user with id: 98




- INSERT INTO orders (order\_date, amount, customer\_id)
- VALUES ('2016/06/06', 33.67, 98);

**Cross Joins**

**-- Finding Orders Placed By George: 2 Step Process**

- SELECT id FROM customers WHERE last\_name='George';
- SELECT \* FROM orders WHERE customer\_id = 1;

**-- Finding Orders Placed By George: Using a subquery**

- SELECT \* FROM orders WHERE customer\_id =
- `   `(
- `       `SELECT id FROM customers
- `       `WHERE last\_name='George'
- `   `);

**-- Cross Join Craziness**

SELECT \* FROM customers, orders;

**Inner Joins**

**IMPLICIT INNER JOIN**

- SELECT \* FROM customers, orders 
- WHERE customers.id = orders.customer\_id;

**-- IMPLICIT INNER JOIN**

- SELECT first\_name, last\_name, order\_date, amount
- FROM customers, orders 
- `   `WHERE customers.id = orders.customer\_id;


-- EXPLICIT INNER JOINS

- SELECT \* FROM customers
- JOIN orders
- `   `ON customers.id = orders.customer\_id;

- SELECT first\_name, last\_name, order\_date, amount 
- FROM customers
- JOIN orders
- `   `ON customers.id = orders.customer\_id;

- SELECT \*
- FROM orders
- JOIN customers
- `   `ON customers.id = orders.customer\_id;

**-- ARBITRARY JOIN - meaningless, but still possible** 

- SELECT \* FROM customers
- JOIN orders ON customers.id = orders.id;

**Left Joins**

-- Getting Fancier (Inner Joins Still)

- SELECT first\_name, last\_name, order\_date, amount 
- FROM customers
- JOIN orders
- `   `ON customers.id = orders.customer\_id
- ORDER BY order\_date;
- SELECT 
- `   `first\_name, 
- `   `last\_name, 
- `   `SUM(amount) AS total\_spent
- FROM customers
- JOIN orders
- `   `ON customers.id = orders.customer\_id
- GROUP BY orders.customer\_id
- ORDER BY total\_spent DESC;

**-- LEFT JOINS**

- SELECT \* FROM customers
- LEFT JOIN orders
- `   `ON customers.id = orders.customer\_id;
- SELECT first\_name, last\_name, order\_date, amount
- FROM customers
- LEFT JOIN orders
- `   `ON customers.id = orders.customer\_id; 
- SELECT 
- `   `first\_name, 
- `   `last\_name,
- `   `IFNULL(SUM(amount), 0) AS total\_spent
- FROM customers
- LEFT JOIN orders
- `   `ON customers.id = orders.customer\_id
- GROUP BY customers.id
- ORDER BY total\_spent;

**ALTERING OUR SCHEMA to allow for a better example (optional)**

- CREATE TABLE customers(
- `   `id INT AUTO\_INCREMENT PRIMARY KEY,
- `   `first\_name VARCHAR(100),
- `   `last\_name VARCHAR(100),
- `   `email VARCHAR(100)
- );
- CREATE TABLE orders(
- `   `id INT AUTO\_INCREMENT PRIMARY KEY,
- `   `order\_date DATE,
- `   `amount DECIMAL(8,2),
- `   `customer\_id INT
- );

**-- INSERTING NEW DATA (no longer bound by foreign key constraint)**

- INSERT INTO customers (first\_name, last\_name, email) 
- VALUES ('Boy', 'George', '<george@gmail.com>'),
- `      `('George', 'Michael', '<gm@gmail.com>'),
- `      `('David', 'Bowie', '<david@gmail.com>'),
- `      `('Blue', 'Steele', '<blue@gmail.com>'),
- `      `('Bette', 'Davis', '<bette@aol.com>');

- INSERT INTO orders (order\_date, amount, customer\_id)
- VALUES ('2016/02/10', 99.99, 1),
- `      `('2017/11/11', 35.50, 1),
- `      `('2014/12/12', 800.67, 2),
- `      `('2015/01/03', 12.50, 2),
- `      `('1999/04/11', 450.25, 5);

- INSERT INTO orders (order\_date, amount, customer\_id) VALUES
- ('2017/11/05', 23.45, 45),
- (CURDATE(), 777.77, 109);

**A MORE COMPLEX RIGHT JOIN**

- SELECT 
- `   `IFNULL(first\_name,'MISSING') AS first, 
- `   `IFNULL(last\_name,'USER') as last, 
- `   `order\_date, 
- `   `amount, 
- `   `SUM(amount)
- FROM customers
- RIGHT JOIN orders
- `   `ON customers.id = orders.customer\_id
- GROUP BY first\_name, last\_name;

**-- WORKING WITH ON DELETE CASCADE**

- CREATE TABLE customers(
- `   `id INT AUTO\_INCREMENT PRIMARY KEY,
- `   `first\_name VARCHAR(100),
- `   `last\_name VARCHAR(100),
- `   `email VARCHAR(100)
- );

- CREATE TABLE orders(
- `   `id INT AUTO\_INCREMENT PRIMARY KEY,
- `   `order\_date DATE,
- `   `amount DECIMAL(8,2),
- `   `customer\_id INT,
- `   `FOREIGN KEY(customer\_id) 
- `       `REFERENCES customers(id)
- `       `ON DELETE CASCADE
- );



- INSERT INTO customers (first\_name, last\_name, email) 
- VALUES ('Boy', 'George', '<george@gmail.com>'),
- `      `('George', 'Michael', '<gm@gmail.com>'),
- `      `('David', 'Bowie', '<david@gmail.com>'),
- `      `('Blue', 'Steele', '<blue@gmail.com>'),
- `      `('Bette', 'Davis', '<bette@aol.com>');

- INSERT INTO orders (order\_date, amount, customer\_id)
- VALUES ('2016/02/10', 99.99, 1),
- `      `('2017/11/11', 35.50, 1),
- `      `('2014/12/12', 800.67, 2),
- `      `('2015/01/03', 12.50, 2),
- `      `('1999/04/11', 450.25, 5);

**Right and Left Joins**

- SELECT \* FROM customers
- LEFT JOIN orders
- `   `ON customers.id = orders.customer\_id;
- SELECT \* FROM orders
- RIGHT JOIN customers
- `   `ON customers.id = orders.customer\_id;    
- SELECT \* FROM orders
- LEFT JOIN customers
- `   `ON customers.id = orders.customer\_id;    
- SELECT \* FROM customers
- RIGHT JOIN orders
- `   `ON customers.id = orders.customer\_id;

**Creating Our Tables**

**-- CREATING THE REVIEWERS TABLE**




- CREATE TABLE reviewers (
- `   `id INT AUTO\_INCREMENT PRIMARY KEY,
- `   `first\_name VARCHAR(100),
- `   `last\_name VARCHAR(100)
- );

**-- CREATING THE SERIES TABLE**

- CREATE TABLE series(
- `   `id INT AUTO\_INCREMENT PRIMARY KEY,
- `   `title VARCHAR(100),
- `   `released\_year YEAR(4),
- `   `genre VARCHAR(100)
- );

**-- CREATING THE REVIEWS TABLE**

- CREATE TABLE reviews (
- `   `id INT AUTO\_INCREMENT PRIMARY KEY,
- `   `rating DECIMAL(2,1),
- `   `series\_id INT,
- `   `reviewer\_id INT,
- `   `FOREIGN KEY(series\_id) REFERENCES series(id),
- `   `FOREIGN KEY(reviewer\_id) REFERENCES reviewers(id)
- );

**-- INSERTING A BUNCH OF DATA**

- INSERT INTO series (title, released\_year, genre) VALUES
- `   `('Archer', 2009, 'Animation'),
- `   `('Arrested Development', 2003, 'Comedy'),
- `   `("Bob's Burgers", 2011, 'Animation'),
- `   `('Bojack Horseman', 2014, 'Animation'),
- `   `("Breaking Bad", 2008, 'Drama'),
- `   `('Curb Your Enthusiasm', 2000, 'Comedy'),
- `   `("Fargo", 2014, 'Drama'),
- `   `('Freaks and Geeks', 1999, 'Comedy'),
- `   `('General Hospital', 1963, 'Drama'),
- `   `('Halt and Catch Fire', 2014, 'Drama'),
- `   `('Malcolm In The Middle', 2000, 'Comedy'),
- `   `('Pushing Daisies', 2007, 'Comedy'),
- `   `('Seinfeld', 1989, 'Comedy'),
- `   `('Stranger Things', 2016, 'Drama');

- INSERT INTO reviewers (first\_name, last\_name) VALUES
- `   `('Thomas', 'Stoneman'),
- `   `('Wyatt', 'Skaggs'),
- `   `('Kimbra', 'Masters'),
- `   `('Domingo', 'Cortes'),
- `   `('Colt', 'Steele'),
- `   `('Pinkie', 'Petit'),
- `   `('Marlon', 'Crafford');

- INSERT INTO reviews(series\_id, reviewer\_id, rating) VALUES
- `   `(1,1,8.0),(1,2,7.5),(1,3,8.5),(1,4,7.7),(1,5,8.9),
- `   `(2,1,8.1),(2,4,6.0),(2,3,8.0),(2,6,8.4),(2,5,9.9),
- `   `(3,1,7.0),(3,6,7.5),(3,4,8.0),(3,3,7.1),(3,5,8.0),
- `   `(4,1,7.5),(4,3,7.8),(4,4,8.3),(4,2,7.6),(4,5,8.5),
- `   `(5,1,9.5),(5,3,9.0),(5,4,9.1),(5,2,9.3),(5,5,9.9),
- `   `(6,2,6.5),(6,3,7.8),(6,4,8.8),(6,2,8.4),(6,5,9.1),
- `   `(7,2,9.1),(7,5,9.7),
- `   `(8,4,8.5),(8,2,7.8),(8,6,8.8),(8,5,9.3),
- `   `(9,2,5.5),(9,3,6.8),(9,4,5.8),(9,6,4.3),(9,5,4.5),
- `   `(10,5,9.9),
- `   `(13,3,8.0),(13,4,7.2),
- `   `(14,2,8.5),(14,3,8.9),(14,4,8.9);

- SELECT 
- title, 
- rating 
- FROM series
- JOIN reviews
- ON series.id = reviews.series\_id;

**AVG rating**

- SELECT
- `   `title,
- `   `AVG(rating) as avg\_rating
- FROM series
- JOIN reviews
- `   `ON series.id = reviews.series\_id
- GROUP BY series.id
- ORDER BY avg\_rating;
- SELECT
- `   `first\_name,
- `   `last\_name,
- `   `rating
- FROM reviewers
- INNER JOIN reviews
- `   `ON reviewers.id = reviews.reviewer\_id;



- SELECT
- `   `first\_name,
- `   `last\_name,
- `   `rating
- FROM reviews
- INNER JOIN reviewers
- `   `ON reviewers.id = reviews.reviewer\_id;

**UNREVIEWED SERIES**

- SELECT title AS unreviewed\_series
- FROM series
- LEFT JOIN reviews
- `   `ON series.id = reviews.series\_id
- WHERE rating IS NULL;

**GENRE AVG RATINGS**

- SELECT genre, 
- `      `Round(Avg(rating), 2) AS avg\_rating 
- FROM   series 
- `      `INNER JOIN reviews 
- `              `ON series.id = reviews.series\_id 
- GROUP  BY genre;

***Reviewer Stats*** 

- SELECT first\_name, 
- `      `last\_name, 
- `      `Count(rating)                               AS COUNT, 
- `      `Ifnull(Min(rating), 0)                      AS MIN, 
- `      `Ifnull(Max(rating), 0)                      AS MAX, 
- `      `Round(Ifnull(Avg(rating), 0), 2)            AS AVG, 
- `      `IF(Count(rating) > 0, 'ACTIVE', 'INACTIVE') AS STATUS 
- FROM   reviewers 
- `      `LEFT JOIN reviews 
- `             `ON reviewers.id = reviews.reviewer\_id 
- GROUP  BY reviewers.id;

***Reviewer Stats With POWER USERS*** 

- SELECT first\_name, 
- `      `last\_name, 
- `      `Count(rating)                    AS COUNT, 
- `      `Ifnull(Min(rating), 0)           AS MIN, 
- `      `Ifnull(Max(rating), 0)           AS MAX, 
- `      `Round(Ifnull(Avg(rating), 0), 2) AS AVG, 
- `      `CASE 
- `        `WHEN Count(rating) >= 10 THEN 'POWER USER' 
- `        `WHEN Count(rating) > 0 THEN 'ACTIVE' 
- `        `ELSE 'INACTIVE' 
- `      `end                              AS STATUS 
- FROM   reviewers 
- `      `LEFT JOIN reviews 
- `             `ON reviewers.id = reviews.reviewer\_id 
- GROUP  BY reviewers.id;

**3 TABLES!**

- SELECT 
- `   `title,
- `   `rating,
- `   `CONCAT(first\_name,' ', last\_name) AS reviewer
- FROM reviewers
- INNER JOIN reviews 
- `   `ON reviewers.id = reviews.reviewer\_id
- INNER JOIN series
- `   `ON series.id = reviews.series\_id
- ORDER BY title;







