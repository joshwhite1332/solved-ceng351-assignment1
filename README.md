Download Link: https://assignmentchef.com/product/solved-ceng351-assignment1
<br>
In the scope of this assignment, you are asked to create a system by designing queries and implementing pre-defined functions to administer a database for a book store. For this, you have certain tasks and well-defined interfaces. What you will do is to implement the provided interfaces to accomplish the given tasks. All necessary data files, classes and the interface you will implement are provided as source files. Do not confuse interface with graphical user interface (GUI). You will not design any GUI in the scope of this assignment. You will be familiar with interface which is a data type like class and enum. The first thing you should do is implementing functions which create the necessary tables corresponding to the schema given in Section 3. Then, you should design queries to accomplish the given tasks. Lastly, you should implement the interface using the queries you have designed as they give the desired results when defined parameters are given. You will not implement Evaluation class. It will be implemented by me to manipulate the database through the pre-defined interface and evaluate your implementations. Your task is to build up classes which implement the provided interfaces.

<h1>1           Objectives</h1>

This assignment aims to help you get familiar with

<ul>

 <li>Java programming language basics,</li>

 <li>Object oriented programming concepts,</li>

 <li>Connecting and querying to MySQL Server using JDBC.</li>

</ul>

<h1>2           Schema</h1>

You will use (strictly) the schema given below in the scope of this assignment.

<strong>author</strong>(<u>author id</u>:int, author name:varchar(60)) <strong>publisher</strong>(publisher id:int, publisher name:varchar(50))

<strong>book</strong>(<u>isbn</u>:char(13), book name:varchar(120), publisher id:int, first publish year:char(4), page count:int, category:varchar(25),

rating:float) <strong>REFERENCES </strong>publisher(publisher id) <strong>author of</strong>(<u>isbn</u>:char(13),<u>author id</u>:int) <strong>REFERENCES </strong>book(isbn) author(author id) <strong>phw1</strong>(<u>isbn</u>:char(13), book name:varchar(120), rating:float)

Your task is to generate a class named BOOKDB (should belong to package ceng.ceng351.bookdb) which implements IBOOKDB interface. You can create any additional classes if necessary. BOOKDB class should be able to accomplish the following tasks:

<ul>

 <li>Creating the database tables</li>

 <li>Inserting data into tables</li>

 <li>Retrieving the required SQL queries for the given questions.</li>

 <li>Performing the required DML operations.</li>

 <li>Dropping the database tables</li>

</ul>

Tasks are explained in more detail below. For each task, there is a corresponding method in IBOOKDB interface. You need to implement them in BOOKDB class. Necessary data files (for populating the tables) to accomplish these tasks will be provided. In <strong>data </strong>folder there are 4 txt files corresponding to each table. You will use these tables when you are inserting data. Data files, interfaces and classes for fulfilling these tasks will be provided as source files. You can assume all information will be complete and consistent, i.e. all necessary data will be inserted before executing a query. You can find detailed description about the usage of the functions in provided source files. Do not forget to define <strong>foreign keys </strong>when you are creating tables. Please do not forget to use DISTINCT keyword when appropriate in your MySQL queries.

<h2>2.1         Creating the database tables</h2>

public int createTables();

You will create all the tables according to the schema described above.

You can assume that tables will be created before executing any other database operation. Returns the number of tables that are created successfully.

<h2>2.2         Inserting data into tables</h2>

public int insertAuthor(Author[] authors); public int insertBook(Book[] books); public int insertPublisher(Publisher[] publishers); public int insertAuthor_of(Author_of[] author_ofs);

You will insert data into appropriate tables.

Returns the number of rows inserted successfully. In this task, please do <strong>not </strong>insert any data inside <strong>phw1 </strong>table.

<h2>2.3         Query 1</h2>

public QueryResult.ResultQ1[] functionQ1();

List isbn, first publish year, page count and publisher name of the book(s) which have the maximum number of pages. Order the results by isbn in ascending order.

<h2>2.4         Query 2</h2>

public QueryResult.ResultQ2[] functionQ2(int author_id1,int author_id2);

For the publishers who have published books that were co-authored by both of the given authors(author1 and author2); list publisher id(s) and average page count(s) of all the books these publishers have published. Order the results by publisher id in ascending order.

<h2>2.5         Query 3</h2>

public QueryResult.ResultQ3[] functionQ3(String author_name);

List book name, category and first publish year of the earliest published book(s) of the author(s) whose author name is given.

Order the results by book name, category and first publish year in ascending order.

<h2>2.6         Query 4</h2>

public QueryResult.ResultQ4[] functionQ4();

For publishers whose name contains at least 3 words (i.e., ”Koc Universitesi Yayinlari”), have published at least 3 books and average rating of all their books are greater than(<em>&gt;</em>) 3; list their publisher id(s) and distinct category(ies) they have published.

PS: You may assume that each word in publisher name is seperated by a space. Order the results by publisher id and category in ascending order.

<h2>2.7         Query 5</h2>

public QueryResult.ResultQ5[] functionQ5(int author_id);

List author id and author name of the authors who have worked with all the publishers that the given author id has worked. Order the results by author id in ascending order.

<h2>2.8         Query 6</h2>

public QueryResult.ResultQ6[] functionQ6();

List author id(s) and isbn(s) of the book(s) written by ”Selective” authors. ”Selective” authors are those who have <strong>only </strong>worked with publishers that have published their books only.(i.e., they haven’t published books of different authors) Order the results by author id and isbn in ascending order.

<h2>2.9         Query 7</h2>

public QueryResult.ResultQ7[] functionQ7(double rating);

List publisher id and publisher name of the publishers who have published at least 2 books in ’Roman’ category and average rating of their books are more than (<em>&gt;</em>) the given value. Order the results by publisher id in ascending order.

<h2>2.10         Query 8 (Bulk insert)</h2>

public QueryResult.ResultQ8[] functionQ8();

<ol>

 <li>Some of the books in the store have been published more than once: although they have same names(book name), they are published with different isbns. For each multiple copy of these books, find the book name(s) with the lowest rating for each book name and store their isbn, book name and rating into <strong>phw1 </strong>table using a single BULK insertion query. If there exists more than 1 with the lowest rating, then store them all.</li>

 <li>After the bulk insertion operation, list isbn, book name and rating of all rows in <strong>phw1 </strong></li>

</ol>

Order the results by isbn in ascending order.

<h2>2.11         Query 9 (Update)</h2>

public double functionQ9(String keyword);

<ol>

 <li>For the books that contain the given <strong>keyword </strong>anywhere in their names, increase their ratings by one. Please note that, the maximum rating cannot be more than 5, therefore if the previous rating is greater than 4, do not update the rating of that book.</li>

 <li>After the update operation, return sum of the ratings of all books.</li>

</ol>

<h2>2.12         Query 10 (Delete)</h2>

public int function10();

<ol>

 <li>Delete publishers in publisher table who haven’t published a book yet.</li>

 <li>After the delete operation, return count of all rows of the publisher table.</li>

</ol>

<h2>2.13         Dropping the database tables</h2>

You will drop all the tables (if they exist).

Returns the number of tables that are dropped successfully.