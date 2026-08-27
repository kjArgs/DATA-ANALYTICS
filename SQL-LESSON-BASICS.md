## INTRODUCTION TO SQL

    SQL or Structured Query Language is a programming language used to manage data stored on the relational databases.

## RELATIONAL DATABASE

    is a database that organizes information in one or more tables.

## WHAT IS A TABLE?

    is a collection of data organized into rows and columns. Tables are sometimes referred as 'relations'.

## WHAT IS A ROW AND COLUMN?

    - a column is a set of data values of a particular type examples are id, name, and age are  the      columns.
    - row is a single record in a table.

## DATA TYPE IN A DATABASE

    - INTEGER, a positive or negative whole number
    - TEXT, a text  string
    - DATE, the date format YYYY-MM-DD
    - REAL, a decimal value

## STATEMENT IN A DATABASE

    a statement is a set of queries that the database recognized as a command.

    CREATE TABLE table_name (
        column_1 data_type,
        column_2 data_type,
        column_3 data_type
    );

    BREAKDOWN OF THE COMPONENT ON THE GIVEN DATABASE STATEMENT
    1). CREATE TABLE is a clause . A 'CLAUSE' performs specific task in SQL. By convention clause are written in capital letters. Clause can also be referred as commands.

    2. table_name is a given name to the table that the command is referred to.

    3. (column_1 data_type, column_2 data_type, column_3 data_type) is a parameter. A parameter is a set of columns, data types, or values that are passed to the clause and arguments.

# MANIPULATION

### CREATE STATEMENT

    statements allow us to create a new table in the database.

    CREATE TABLE celebs (
        id INTEGER,
        name TEXT,
        age INTEGER
    );

### INSERT STATEMENT

    insert statement allows user to insert rows in the tables.

    INSERT INTO celebs (id, name, age)
    VALUES (1, 'Justin Bieber', 29);

    BREAKDOWN OF THE STATEMENT
        1. INSERT INTO is the clause that adds the specific row or rows.

        2. celebs is the table row is added to.

        3. (id, name, age) is a parameter identifying the columns that data will be inserted into.

        4. VALUES is a clause that indicates the data being inserted.

        5. (1, 'Justin Bieber', 29) is a parameter identifying the values being inserted.

            1: an integer that will be added to id column
            'Justin Bieber': text that will be added to name column
            29: an integer that will be added to age column

### SELECT STATEMENT

    SELECT statements are used to fetch data from a database.

    SELECT name FROM celebs;

    BREAKDOWN OF THE STATEMENT:

        1. Every SQL query will begin with the SELECT command to fetch data from one or more tables.

        2. SELECT is a clause that indicates that the statement is a query. You will use SELECT every time you query data from a database.

        3. name specifies the column to query data from.

        4. FROM celebs specifies the name of the table to query data from. In this statement, data is queried from the celebs table.

        NOTE: * is a special wildcard character that we have been using. It allows you to select every column in a table without having to name each one individually.

### ALTER STATEMENT

    The ALTER TABLE statement adds a new column to a table. You can use this command when you want to add columns to a table.

        ALTER TABLE celebs
        ADD COLUMN twitter_handle TEXT;

    BREAKDOWN OF THE STATEMENT
        1. ALTER TABLE is a clause that lets you make the specified changes.

        2. celebs is the name of the table that is being changed.

        3. ADD COLUMN is a clause that lets you add a new column to a table:

### UPDATE STATEMENT

    The UPDATE statement edits a row in a table. You can use the UPDATE statement when you want to change existing records.

    UPDATE celebs
    SET twitter_handle = '@taylorswift13'
    WHERE id = 4;
    BREAKDOWN OF THE STATEMENT:
        1. UPDATE is a clause that edits a row in the table.

        2. celebs is the name of the table.

        3. SET is a clause that indicates the column to

### DELETE STATEMENT

    The DELETE FROM statement deletes one or more rows from a table. You can use the statement when you want to delete existing records.

    DELETE FROM celebs
    WHERE twitter_handle IS NULL;

    BREAKDOWN OF THE STATEMENT:

        1. DELETE FROM is a clause that lets you delete rows from a table.

        2. celebs is the name of the table we want to delete rows from.

        3. WHERE is a clause that lets you select which rows you want to delete. Here we want to delete all of the rows where the twitter_handle column IS NULL.

        4. IS NULL is a condition in SQL that returns true when the value is NULL and false otherwise.

### CONSTRAINTS STATEMENT

    that add information about how a column can be used are invoked after specifying the data type for a column. They can be used to tell the database to reject inserted data that does not adhere to a certain restriction.

    CREATE TABLE celebs (
        id INTEGER PRIMARY KEY,
        name TEXT UNIQUE,
        date_of_birth TEXT NOT NULL,
        date_of_death TEXT DEFAULT 'Not Applicable'
    );
    BREAKDOWN OF THE STATEMENT: 
        
        1. PRIMARY KEY columns can be used to uniquely identify the row. Attempts to insert a row with an identical value to a row already in the table will result in a constraint violation which will not allow you to insert the new row.

        2. UNIQUE columns have a different value for every row. This is similar to PRIMARY KEY except a table can have many different UNIQUE columns.

        3. NOT NULL columns must have a value. Attempts to insert a row without a value for a NOT NULL column will result in a constraint violation and the new row will not be inserted.

        4. DEFAULT columns take an additional argument that will be the assumed value for an inserted row if the new row does not specify a value for that column.
