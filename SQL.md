
# SQL

## Основы SQL

SQL - язык позволяющий осуществлять запрсосы к БД посредством СУБД. В различных СУБД язык SQL может иметь свою специфичную реализацию (свой диалект).

Подмножество языка SQL:

- DDL (Data Definition Language) - язык для создания и модификации структуры БД с помощью операторов CREATE, ALTER, DROP, TRUNCATE, RENAME.

- DML (Data Manipulation Language) - язык для манипуляции данными в БД с помощью операторов SELECT, INSERT, UPDATE, DELETE.
 
- DCL (Data Control Language) - язык для предоставления и отзыва привилегий пользователя БД с помощью операторов GRANT, DENY, REVOKE. 

- TCL (Transaction Control Language) - язык для контроля и управления транзакциями БД с помощью операторов BEGIN TRANSACTION, COMMIT, ROLLBACK. 

## Основы выборки #1

### Базовый синтаксис

Одна из основных функций SQL - это получение выборок данных из СУБД. Для этого в SQL используется оператор SELECT.

Вывод произвольных значений

    SELECT "Hello world";

Вывод всех данных из таблицы

Для вывода всех данных из таблицы используется символ *

    SELECT * 
    FROM {table_name};

Вывод данных из определенных колонок таблицы 

    SELECT {column_name #1}, {column_name #2} 
    FROM {table_name};

Псевдонимы (алиасы)

Используется оператор AS для присвоения сокращенных имен столбцам или таблицам, улучшает читаемость кода.

    SELECT {column_name #1}, {column_name #2} AS {alias_name} 
    FROM {table_name};

### Литералы в SQL #1.1

Литерал - эот указанное явным образом фиксировоанное значение, например, число 12 или строка "SQL".

Основными типами литералов в MySQL являются:

- строковый;
- числовой;
- логический;
- NULL;
- литерал длаты и времемни.

Строковые литералы 

Строка - это последовательность символов, заключенных в одинарные ('') или двойные ("") кавычки.
Строки могут содержать специальные последовательноти символов, начинающиеся с '\' (экранирующий символ).
Они нужны для того, чтобы СУБД придала обычным символам (буквам и другим знакам) новое особое  значение.
Например, последовательность '\n' буквально означает 'перево строки'.





