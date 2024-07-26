CREATE TABLE users (
    id BIGINT NOT NULL PRIMARY KEY,
    first_name VARCHAR(64) NOT NULL,
    last_name VARCHAR(64) NOT NULL,
    email VARCHAR(128) NOT NULL
);

INSERT INTO users (id, first_name, last_name, email)
VALUES (1, 'Kost', 'Kuzm', 'kost_kuzm@mail.com');

UPDATE users SET
email = 'updated_mail@email.com'
WHERE id = 1;

SELECT * FROM users
WHERE first_name = 'Kost' AND last_name = Kuzm;

SELECT * FROM users
WHERE id = 2 OR id = 3;

DELETE FROM users
WHERE id = 2 OR id = 3;

CREATE TABLE apendings (
    id BIGINT NOT NULL PRIMARY KEY,
    price INT NOT NULL,
    created_at TIMESTAMP DEFAULT now(),
    user_id BIGINT NOT NULL,

    CONSTRAINT user_id_fk FOREIGN KEY (user_id) REFERENCES users (id)
);

SELECT spendings.*, users.first_name FROM spendings 
JOIN users ON users.id = spendings.user_id AND first_name = 'Kost';

SELECT SUM(price) FROM spendings;

SELECT MAX(price) FROM spendings
GROUP BY user_id;

SELECT users.*, SUM(spendings.price) FROM users
INNER JOIN spendings ON users.id = spendings.user_id
GROUP BY users.id, spendings.user_id
HAVING SUM(spendings.price) > 1000000;

ALTER TABLE spendings ADD COLUMN category_id BIGINT;

ALTER TABLE spendings ADD CONSTRAINT category_fk FOREIGN KEY (category_id) REFERENCES categories (id);

Вывести имена людей, которые заканчиваются на "man":
SELECT name FROM Passenger WHERE name LIKE '%man';

Вывести имена всех людей, которые есть в базе данных авиакомпаний:
SELECT name FROM Passenger;

Вывести все рейсы, совершенные из Москвы:
SELECT * FROM Trip
WHERE town_from = 'Moscow';


Вывести названия всеx авиакомпаний:
SELECT name FROM Company;

Вывести количество рейсов, совершенных на TU-134:
SELECT COUNT(plane) AS count FROM Trip
WHERE plane = 'TU-134';

Какие компании совершали перелеты на Boeing:
SELECT DISTINCT Company.name FROM Trip
INNER JOIN Company ON Company.id = Trip.company
WHERE plane = 'Boeing';

Вывести все названия самолётов, на которых можно улететь в Москву (Moscow):
SELECT DISTINCT  plane FROM Trip
WHERE town_to = 'Moscow';

Какие компании организуют перелеты из Владивостока (Vladivostok)?:
SELECT Company.name FROM Company
INNER JOIN Trip ON Trip.company = Company.id
WHERE town_from = 'Vladivostok';





