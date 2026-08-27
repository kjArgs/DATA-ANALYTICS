## WHAT IS QUERY?

    is a process of requesting information to retrieve data from the database.

### AS CLAUSE

    is a keyword that allows you to rename the table or column with an alias.

        SELECT name AS '______'
        FROM movies;
    NOTE: When using AS, the columns are not being renamed in the table. The aliases only appear in the result.

### DISTINCT

    DISTINCT is used to return unique values in the output. It filters out all duplicate values in the specified column(s).

    For example,
        SELECT tools
        FROM inventory;

    might return,

        tools
        Hammer
        Nails
        Nails
        Nails


    this will return redundant result as long as it is from tools category

    if we add distinct

        SELECT DISTINCT tools
        FROM inventory;

    it will return
        tools
        Hammer
        Nails

## WHERE CLAUSE

    We can restrict our query results using thE WHERE clause in order to obtain only the information we want.

        SELECT *
        FROM movies
        WHERE imdb_rating > 8;

    How does it work?
        1. The WHERE clause filters the result set to only include rows where the following condition is true.

        2. imdb_rating > 8 is the condition. Here, only rows with a value greater than 8 in the imdb_rating column will be returned.

        //put here just for the meantime
        Comparison operators used with the WHERE clause are:

                = equal to
                != not equal to
                > greater than
                < less than
                >= greater than or equal to
                <= less than or equal to

## LIKE OPERATOR

    LIKE can be a useful operator when you want to compare patterns or similar values.

    WILDCARD CHARACTERS:

    1. % (Percent Sign): Represents zero, one, or multiple characters.
    2. _ (Underscore): Represents exactly one single character.

        PATTERN            MEANING
        'A%'               Starts with A
        '%A'               Ends with A
        '%A%'              Contains before and after
        '%or%'             Contains "or" anywhere
        '_r%'              Has "r" in the second position
        'A__%'             Starts with "A" and is at least 3 characters long
        'A_z'              Starts with "A", ends with "z", exactly 3 characters long

        example query,
            SELECT *
            FROM movies
            WHERE name LIKE 'A%';

## Is Null

    Unknown values are indicated by NULL.

    It is not possible to test for NULL values with comparison operators, such as = and !=.

    Instead, we will have to use these operators:
       1. IS NULL
       2. IS NOT NULL

        example,
            SELECT name
            FROM movies
            WHERE imdb_rating IS NOT NULL;

## BETWEEN

    The BETWEEN operator is used in a WHERE clause to filter the result set within a certain range. It accepts two values that are either numbers, text, or dates.

    When the values are text, BETWEEN filters the result set for within the alphabetical range.

    In this statement, BETWEEN filters the result set to only include movies with names that begin with the letter ‘A’ up to, but not including ones that begin with ‘J’.

        SELECT *
        FROM movies
        WHERE name BETWEEN 'A' AND 'J';

    However, if a movie has a name of simply ‘J’, it would actually match. This is because BETWEEN goes up to the second value — up to ‘J’. So the movie named ‘J’ would be included in the result set but not ‘Jaws’.

## AND

    Sometimes we want to combine multiple conditions in a
    WHERE clause to make the result set more specific and useful.

    example query,
        SELECT *
        FROM movies;

    - year BETWEEN 1990 AND 1999 is the 1st condition.
    - genre = 'romance' is the 2nd condition.=
    - AND combines the two conditions.

## OR

    Similar to AND, the OR operator can also be used to combine multiple conditions in WHERE, but there is a fundamental difference:
        - AND operator displays a row if all the conditions are true.
        - OR operator displays a row if any condition is true.

            SELECT *
            FROM movies
            WHERE year > 2014
            OR genre = 'action';

        With OR, if any of the conditions are true, then the row is added to the result.

## ORDER BY

    It is often useful to list the data in our result set in a particular order.

    We can sort the results using
    ORDER BY , either alphabetically or numerically. Sorting the results often makes the data more useful and easier to analyze.

    For example, if we want to sort everything by the movie’s title from A through Z:

        SELECT *
        FROM movies
        ORDER BY name;

    - ORDER BY is a clause that indicates you want to sort the result set by a particular column.

    - name is the specified column.

    Sometimes we want to sort things in a decreasing order. For example, if we want to select all of the well-received movies, sorted from highest to lowest by their year:

        SELECT *
        FROM movies
        WHERE imdb_rating > 8
        ORDER BY year DESC;

    - DESC is a keyword used in ORDER BY to sort the results in descending order (high to low or Z-A).

    - ASC is a keyword used in ORDER BY to sort the results in ascending order (low to high or A-Z).

## LIMIT

    LIMIT is a clause that lets you specify the maximum number of rows the result set will have. This saves space on our screen and makes our queries run faster.

    NOTE: LIMIT always goes at the very end of the query. Also, it is not supported in all SQL databases.

## CASE

    CASE statement allows us to create different outputs (usually in the SELECT statement). It is SQL’s way of handling if-then logic.

    Suppose we want to condense the ratings in movies to    three levels:

        - If the rating is above 8, then it is Fantastic.
        - If the rating is above 6, then it is Poorly Received.
        - Else, Avoid at All Costs.

            SELECT name,
            CASE
            WHEN imdb_rating > 8 THEN 'Fantastic'
            WHEN imdb_rating > 6 THEN 'Poorly Received'
            ELSE 'Avoid at All Costs'
            END
            FROM movies;


