---
layout: default
title: "Lab 4: SQL, Queries, Joins"
---

Getting Started
===============

Download [CS320\_Derby.zip](../resources/CS320_Derby.zip) and [CS320\_Lab04.zip](CS320_Lab04.zip). Import them into your Eclipse workspace<br> (**File-\>Import...-\>General-\>Existing projects into workspace-\>Archive File**). You will see a projects called **CS320\_Derby** and **CS320\_Lab04** in the Package Explorer.  You will be running the **SQLDemo** class in the **CS320_Lab04** project.

Setting up the database
=======================

Execute the **SQLDemo** class as a Java application.

Use **create table** commands to create **books** and **authors** tables. From the **SQL\>** prompt, enter the following commands.  Rather than typing them, you can actually copy each command from this page and paste it into the SQL prompt - then press "Enter" to execute the command.

    create table books (
        book_id int
            primary key generated always as identity (start with 1, increment by 1),
        author_id int,
        title varchar(70),
        isbn varchar(15),
        published int
    );

    create table authors (
        author_id int
            primary key generated always as identity (start with 1, increment by 1),
        lastname varchar(40),
        firstname varchar(40)
    );

Next, use **import** commands to load data into these tables:

    import books books.csv;

    import authors authors.csv;

Your database is now populated with data.

Now, use the **alter table** command to establish **author_id** as a foreign key in the **books** table.  Enter the following command:

    alter table books
        add foreign key (author_id)
        references authors (author_id);
    
The schemas of the database tables are described in the notes for [Lecture 13](../lectures/lecture13.html).

**NOTE:** You must work individually on this lab.  It is imperative that everyone on your team be able to construct SQL queries, to establish a connection between a Java program and a SQL database, and to write SQL queries embedded in Java code.  This **WILL** come up on the exam.

Task
====

Compose and execute SQL queries that retrieve the following information.  For the later queries, you will have to do some research at **[w3schools](http://www.w3schools.com/sql/default.asp)** in order to learn the proper SQL commands to complete the query.  This is intended as an exercise to familiarize you with the w3schools website, as well as reinforce researching for new information on your own.

Each query should be terminated with a semicolon (**;**). For example, here is asession showing a query to select all of the tuples in the **authors** table (user input in **bold**):

<pre>
SQL> <b>select * from authors;</b>
AUTHOR_ID    LASTNAME FIRSTNAME
--------- ----------- ---------
        1       Adams   Douglas
        2       Adams     Scott
        3    Breathed  Berkeley
        4     Chapman    Graham
        5      Cleese      John
        6     Gilliam     Terry
        7     Hawking   Stephen
        8        Idle      Eric
        9       Jones     Terry
       10    Kahneman    Daniel
       11    Mlodinow   Leonard
       12      Newton     Isaac
       13       Palin   Michael
       14   Watterson      Bill
OK (14 rows(s))
</pre>

Make sure to verify that the results of each query are correct by comparing against the  database tables themselves.

1) The title for each book written by Stephen Hawking

2) The title and year of publishing for each book written by Douglas Adams

3) The author's name (first and last), the ISBN, and the year published for the book with the title "Something Under the Bed is Drooling"

4) All of the authors for "The Complete Monty Python's Flying Circus; All the Words, Volume 1"

5) The title and author for each of Berkeley Breathed's and Bill Watterson's books, sorted in ascending order by title

6) The author(s) and title for each book with the word "Time" or "Universe" in the title, sorted in ascending order by lastname, and then ascending by title.

7) Attempt to insert a new book into the **books** table, with an **author_id** that does not appear in the **authors** table (this attempt should fail, due to specifying an invalid **foreign key** for **author_id**)

8) Insert yourself as a new author in the **authors** table (do not specify an author_id, Derby will do that for you, since **author_id** is the auto-generated primary key for the **authors** table)

9) Retrieve the **author_id** from the **authors** table for your entry and insert a new book into the **books** table, using your **author_id**

10) Now retrieve all of the information for your book (title, ISBN, published, lastname, firstname)

# What to submit

Download the [template text file](lab04-template.txt) and rename it **lab04-username.txt** (replace "username" with your YCP username).  For each query listed above, copy and paste the following information into your text file:

* The exact query you came up with (including the "SQL>" prompt
* The exact result of the query (including the last line that starts with "OK").

Copy and paste the final working query and the results of the query from the Eclipse console underneath its respective question in the supplied template file.  I recommend that you develop each query in the template file, and then copy and paste it to the "SQL>" prompt in the Eclipse console, and then execute it.  That way, you can easily iterate editing and executing the SQL queries.

**NOTE:** You may NOT use specific **author_id**'s or **book_id**'s directly in your queries (except for problems 7 and 9, which specifically state to enter an **author_id**).  You **must** join the tables using the method given in the lecture and lab, and demonstrated in class.

**NOTE:** Look out for the "traps" of not specifying a semi-colon at the end of your SQL statement in SQLDemo, and for having an odd number of single quotes in a query.  Also, you will have to figure out how to specify a single quote as part of a text string, and you will also have to figure out how to insert a new row into a table (hint: w3schools).

Upload your solution text file to the **Lab04** project on the Marmoset server. The server URL is

> [https://cs.ycp.edu/marmoset/](https://cs.ycp.edu/marmoset/)
