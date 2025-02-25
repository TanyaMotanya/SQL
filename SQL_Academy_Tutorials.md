# SQL
SQL Academy Lessons
Практические задачки из интерактивного учебника по SQL
## Содержание
- [Общая структура запроса](#Общая_структура_запроса)
- [Условный оператор WHERE](#Условный_оператор_WHERE)
- [Сортировка, оператор ORDER BY](#Сортировка_оператор_ORDER_BY)
- [Группировка данных и агрегатные функции](#Группировка_данных_и_агрегатные_функции)
____
## <a name="Общая_структура_запроса">Общая структура запроса</a>

### 1. SELECT по одному столбцу
Выведите поле name из таблицы Passenger.
```SQL
SELECT name FROM Passenger
```
### 2. SELECT по нескольким столбцам
Выведите поля member_id, member_name и status из таблицы FamilyMembers.
```SQL
SELECT member_id, member_name, status FROM FamilyMembers
```
### 3. SELECT по всем столбцам
Выведите все столбцы из таблицы Payments.
```SQL
SELECT * FROM Payments
```
### 4. Получение уникальных записей
Выполните предложенный ниже запрос, чтобы увидеть список пассажиров. Если присмотреться, то можно увидеть, что пассажир с именем Bruce Willis присутствует здесь дважды (в начале и конце списка).
Ваша задача заключается в том, чтобы вывести только уникальные имена пассажиров, дополнив предложенный запрос.
```SQL
SELECT DISTINCT name FROM Passenger
```
____
#### <a name="Условный_оператор_WHERE">Условный оператор WHERE</a>

### 1. Простая фильтрация по числам
Выведите идентификаторы товаров (поле good) из таблицы Payments, стоимость которых больше 2000 единиц. Стоимость товара хранится в поле unit_price.
```SQL
SELECT good FROM Payments WHERE unit_price > 2000
```
### 2. Простая фильтрация по строкам
Выведите имена (поле member_name) членов семьи из таблицы FamilyMembers, чей статус (поле status) равен "father".
```SQL
SELECT member_name FROM FamilyMembers WHERE status  = 'father'
```
### 3. Логическое ИЛИ
Выведите имя (поле member_name) и дату рождения (поле birthday) членов семьи из таблицы FamilyMembers, чей статус (поле status) равен "father" или "mother".
```SQL
SELECT member_name, birthday FROM FamilyMembers
    WHERE status = 'father' OR status = 'mother'  
```
### 4. Логическое И
Необходимо получить все комнаты, в которых есть как кухня (поле has_kitchen), так и интернет (поле has_internet). Напишите запрос, удовлетворяющий вышеописанному условию, который выводит все поля из таблицы Rooms.
Наличие обозначается 1 или true, а отсутствие 0 или false.
```SQL
SELECT * FROM Rooms
    WHERE has_kitchen = true AND has_internet = true
```
### 5. WHERE BETWEEN
Выведите резервации комнат (поля room_id, start_date, end_date) из таблицы Reservations, у которых итоговая стоимость аренды (поле total) находится в промежутке от 500 до 1200 включительно.
```SQL
SELECT room_id ,start_date ,end_date FROM Reservations
    WHERE total BETWEEN 500 AND 1200 
```
### 6. Поиск по строковому шаблону
Выведите всех членов семьи с фамилией "Quincey".
```SQL
SELECT member_name FROM FamilyMembers
    WHERE member_name LIKE '% Quincey'
```
____
## <a name="Сортировка_оператор_ORDER_BY">Сортировка, оператор ORDER BY</a>

### 1. Сортировка по убыванию
Для каждого отдельного платежа выведите идентификатор товара и сумму, потраченную на него, в отсортированном по убыванию этой суммы виде. Список платежей находится в таблице Payments.
Для вывода суммы используйте псевдоним sum.
```SQL
SELECT good, unit_price * amount as sum
    FROM Payments ORDER BY sum DESC
```
### 2. Сортировка по нескольким столбцам
Выведите список членов семьи с фамилией Quincey, в отсортированном по возрастанию столбцам status и member_name виде.
```SQL
SELECT * FROM FamilyMembers
    WHERE member_name LIKE '% Quincey'
        ORDER BY status, member_name
```
____
## <a name="Группировка_данных_и_агрегатные_функции">Группировка данных и агрегатные функции</a>

### 1. Группировка и сортировка
Подсчитайте количество учеников в каждом классе, а также отсортируйте их по убыванию количества учеников. Принадлежность ученика к конкретному классу вы можете получить из таблицы Student_in_class. В качестве результата необходимо вывести идентификатор класса (поле class) и количество учеников в этом классе.
Для вывода количества учеников используйте псевдоним count.
```SQL
SELECT class, COUNT(student ) AS count
    FROM Student_in_class
        GROUP BY class
        ORDER BY count DESC
```
### 2. Агрегатные функции MIN и MAX
Найдите самых старших членов семьи (используйте поле birthday) среди всех существующих семей на основании их статуса (поле status). Выведите статус и дату рождения.
Для вывода даты рождения используйте псевдоним birthday.
```SQL
SELECT status ,MIN(birthday) AS birthday FROM FamilyMembers
    GROUP BY status 
```
### 3. Агрегатная функция AVG
Получите среднее время полётов, совершённых на каждой из моделей самолёта. Выведите поле plane и среднее время полёта в секундах.
Для вывода времени используйте псевдоним time.
Используйте функцию TIMESTAMPDIFF(second, time_out, time_in), чтобы получить разницу во времени в секундах между двумя датами.
```SQL
SELECT plane ,AVG(TIMESTAMPDIFF(second, time_out, time_in)) AS time
    FROM Trip
        GROUP BY plane
```
### 4. Выборка с использованием нескольких агрегатных функций
Выведите идентификатор комнаты (поле room_id), среднюю стоимость за один день аренды (поле price, для вывода используйте псевдоним avg_price), а также количество резерваций этой комнаты (используйте псевдоним count). Полученный результат отсортируйте в порядке убывания сначала по количеству резерваций, а потом по средней стоимости.
```SQL
SELECT room_id, AVG(price) AS avg_price, COUNT(total) AS count
    FROM Reservations GROUP BY room_id 
        ORDER BY count DESC, avg_price DESC
```
### 5. HAVING
Дополните запрос из предыдущего задания, оставив в выборке только те комнаты, чья средняя стоимость аренды превышает 150 ед.
```SQL
SELECT room_id, AVG(price) AS avg_price, COUNT(total) AS count
    FROM Reservations GROUP BY room_id 
        HAVING avg_price > 150
        ORDER BY count DESC, avg_price DESC
```
____
