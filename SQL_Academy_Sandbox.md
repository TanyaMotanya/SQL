# SQL
____
## Задание 1
Вывести имена всех людей, которые есть в базе данных авиакомпаний
```SQL
SELECT name
FROM Passenger
```
## Задание 2
Вывести названия всеx авиакомпаний
```SQL
SELECT name
FROM Company
```
## Задание 3
Вывести все рейсы, совершенные из Москвы
```SQL
SELECT *
FROM Trip
WHERE town_from = 'Moscow'
```
## Задание 4
Вывести имена людей, которые заканчиваются на "man"
```SQL
SELECT name
FROM Passenger
WHERE name LIKE '%man'
```
## Задание 5
Вывести количество рейсов, совершенных на TU-134
```SQL
SELECT COUNT(plane) as count
FROM Trip
WHERE plane = 'TU-134'
```
## Задание 6
Какие компании совершали перелеты на Boeing
```SQL
SELECT DISTINCT name
FROM Company
  JOIN Trip ON Company.id = Trip.company
WHERE plane = 'Boeing'
```
## Задание 7
Вывести все названия самолётов, на которых можно улететь в Москву (Moscow)
```SQL
SELECT DISTINCT plane
FROM Trip
WHERE town_to = 'Moscow'
```
## Задание 8
В какие города можно улететь из Парижа (Paris) и сколько времени это займёт?
```SQL
SELECT town_to,
  TIMEDIFF(time_in, time_out) AS flight_time
FROM Trip
WHERE town_from = 'Paris'
```
