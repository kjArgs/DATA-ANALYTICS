## EXERCISE NO 2

    CREATE TABLE friends(
    id INTEGER,
    name TEXT,
    birthday DATE
    );

    INSERT INTO friends (id, name, birthday)
    VALUES(1, 'Ororo Munroe', '1940-05-30');

    INSERT INTO friends (id, name, birthday)
    VALUES(2, 'Juan Dela Cruz', '1942-09-27');

    INSERT INTO friends (id, name, birthday)
    VALUES(3, 'Ehh Cruz', '2003-09-27');

    UPDATE friends
    SET name = 'Storm'
    WHERE name = 'Ororo Munroe';

    ALTER TABLE friends
    ADD COLUMN email TEXT;

    UPDATE friends 
    SET email CASE 
    WHEN name = 'Storm' THEN 'storm@codeacademy.com'
    ELSE NULL
    END;

    DELETE FROM friends
    WHERE name = 'Storm';

    SELECT * FROM friends;