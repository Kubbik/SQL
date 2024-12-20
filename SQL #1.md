# SQL

## Основы SQL

SQL - язык позволяющий осуществлять запрсосы к БД посредством СУБД. В различных СУБД язык SQL может иметь свою специфичную реализацию (свой диалект).

Подмножество языка SQL:

- DDL (Data Definition Language) - язык для создания и модификации структуры БД с помощью операторов CREATE, ALTER, DROP, TRUNCATE, RENAME.

- DML (Data Manipulation Language) - язык для манипуляции данными в БД с помощью операторов SELECT, INSERT, UPDATE, DELETE.
 
- DCL (Data Control Language) - язык для предоставления и отзыва привилегий пользователя БД с помощью операторов GRANT, DENY, REVOKE. 

- TCL (Transaction Control Language) - язык для контроля и управления транзакциями БД с помощью операторов BEGIN TRANSACTION, COMMIT, ROLLBACK. 

## #1 Основы выборки #1

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

### #1.1 Литералы в SQL

Литерал - эот указанное явным образом фиксировоанное значение, например, число 12 или строка "SQL".

Основными типами литералов в MySQL являются:

- строковый;
- числовой;
- логический;
- NULL;
- литерал длаты и времемни.


**Строковые литералы** 

Строка - это последовательность символов, заключенных в одинарные ('') или двойные ("") кавычки.
Строки могут содержать специальные последовательноти символов, начинающиеся с '\' (экранирующий символ).
Они нужны для того, чтобы СУБД придала обычным символам (буквам и другим знакам) новое особое  значение.
Например, последовательность '\n' буквально означает 'перево строки'.

    SELECT "Текстовая строка Текстовая строка" AS String;

    String
    Текстовая строка Текстовая строка

    SELECT "Текстовая строка \n Текстовая строка" AS String;

    String
    Текстовая строка
    Текстовая строка

**Числовые литералы**

Включает в себя целые и дробные числа. Разделительный знак для дробного числа — «.» (точка) - 1, 2.9, 0.01

Может иметь только целую, дробную часть или обе сразу - .2, 1.1, 10

Может быть положительным и отрицательным числом (для положительного числа совсем не обязательно указывать знак) - +1, -10, -2.2

Могут быть представлены в экспоненциальном виде - 1e3 (=1000) 1e-3 (=0.001)

Арифметические операторы

Для числовых литералов в SQL есть все привычные нам арифметические операторы:

| Оператор | Описание | Пример |
| ------------- | ------------- | ------------- |
| %, MOD | Деление по модулю | 11 % 5 = 1 |
| * | Умножение | 10 * 16 = 160 |
| + | Сложение | 98 + 2 = 100 |
| - | Вычитание | 50 - 51 = -1 |
| / | Деление | 1 / 2 = 0.5 |
| DIV | Целочисленное деление | 10 DIV 4 = 2 |

Используя эти операторы можно построить любое арифметическое выражение, применяя стандартные правила арифметики.

Для примера:

    SELECT (5 * 2 - 6) / 2 AS Result;

    Result
    2

**Литералы даты и времени**

Значения даты и времени могут быть представлены в формате строки или числа.
Например, если мы хотим указать какую-то дату в запросе, то мы можем это сделать с помощью строки "1970-12-30", "19701230" или же числа 19701230. В обоих случаях эти значения будут интерпретироваться как дата «30 декабря 1970 года».

Ниже приведён пример использования литерала даты:

    SELECT * FROM FamilyMembers WHERE birthday > '1970-12-30';

Кроме самой даты, мы можем также указывать отдельно время или же всё вместе.

| Тип | Описание | Пример |
| ------------- | ------------- | ------------- |
| Дата | Интерпретируется как дата со временем, равным нулю | *YYYY-MM-DD, YYYYMMDD*; Вместо разделителя "-" можно использовать любой знак препинания; Например:'2020- 1-01' = 1 января 2020, 00:00:00 |
| Время | Содержит только время без конкретной даты | *hh:mm:ss, hh:mm, hh, ss*; Разделитель тоже можно опустить; Например: 12:11 = 12:11:00 |
| Дата и время | Дата с возможностью задать конкретное времяСложение | *YYYY-MM-DD hh:mm:ss YYYYMMDDhhmmss*; Например:'20200101183030' = 1 января 2020, 18:30:30 |


**Логические литералы**

Логический литерал - значения TRUE и FALSE, означающие истинность и ошибочность какого-либо утверждения. При интерпретации запроса, MySQL преобразует их в числа: TRUE и FALSE становятся 1 и 0 соответственно.

**NULL**

Значение NULL означает "нет данных", "нет значения". Оно нужно, чтобы отличать визуально пустые значения, такие как строка нулевой длины или "пробел", от того, когда значения вообще нет, даже пустого.

### #1.2 Применение функций

При составлении SQL запросов мы можем использовать встроенные функции. Например, если мы хотим вывести строку в верхнем регистре, то для этого мы можем использовать функцию UPPER.

    SELECT UPPER("Hello world") AS upper_string;
    
    upper_string
    HELLO WORLD

**Что такое встроенная функция?**

Встроенная функция – реализованный в СУБД кусок кода, с помощью которого можно выполнять преобразования строковых, числовых и других данных в запросах.
Каждая функция принимает набор аргументов определённого типа, выполняет заложенные в неё операции и обязательно возвращает один из возможных литералов. Стоит отметить, что функции могут принимать как ноль аргументов, так и несколько.
Например, функция NOW() принимает ноль аргументов и возвращает литерал в формате даты, а LENGTH('sql') принимает один строковый аргумент и возвращает числовой литерал «11».

**Примеры функций**

Функций достаточно много, но основные всегда можно найти с помощью поиска в шапке или же на странице справочника функций.
Вот некоторые из них:

**LOWER**

Возвращает строку, в которой все символы записаны в нижнем регистре

    SELECT LOWER('SQL Academy') AS lower_string;
    
    lower_string
    sql academy
	
**YEAR**

Возвращает год для указанной даты

    SELECT YEAR("2022-06-16") AS year;
    
    year
    2022
	
**INSTR**

Осуществляет поиск подстроки в строке, возвращая позицию её первого символа. При этом отсчёт начинается с единицы, а не нуля, как в большинстве языков программирования.
Функция работает путём посимвольного сравнения исходной строки с искомой. Например, в строке sql-academy подстрока academy появляется, начиная с пятого символа.

    SELECT INSTR('sql-academy', 'academy') AS idx;
    
    idx
    5

**LENGTH**

Возвращает длину указанной строки.

    SELECT LENGTH('sql-academy') AS str_length;
    
    str_length
    11

**Применение функций над значениями полей таблицы**

Функции можно применять не только над литералами, но и над значениями, взятыми из таблицы. При этом функция выполняет преобразования для каждой строки отдельно.
Например, давайте вернёмся к нашей базе данных и рассмотрим таблицу FamilyMembers: она содержит имя, статус и дату рождения людей.

    CREATE TABLE FamilyMembers (
            member_id INT PRIMARY KEY AUTO_INCREMENT,
            status VARCHAR(100),
            member_name VARCHAR(100),
            birthday DATETIME
        )
    
    CREATE TABLE Payments (
			payment_id INT PRIMARY KEY AUTO_INCREMENT,
			family_member INT,
			good INT,
			amount INT,
			unit_price INT,
			date DATETIME,
			FOREIGN KEY (family_member) REFERENCES FamilyMembers (member_id)
	)

	CREATE TABLE GoodTypes (
		good_types_id INT PRIMARY KEY AUTO_INCREMENT,
		good_types_name VARCHAR(255)
	)

    CREATE TABLE Goods (
		good_id INT PRIMARY KEY AUTO_INCREMENT,
		good_name VARCHAR(100),
		type INT,
		FOREIGN KEY (type) REFERENCES GoodTypes (good_types_id)
	)

Каждое значение этих полей мы можем изменить при выводе. Так нижележащий запрос высчитывает длину полного имени для каждого из членов семьи.

    SELECT member_name,
        LENGTH(member_name) AS fullname_length
    FROM FamilyMembers;

**Операции над результатом функции**

Поскольку мы знаем, что каждая функция должна вернуть какой-либо из возможных литералов, то её результат также можно использовать в дальнейших расчётах и преобразованиях.
К примеру, мы хотим получить первые три буквы в строке и преобразовать их в заглавные. Для этого нам будет достаточно скомбинировать две функции: LEFT и UPPER, где результат одной функции будет аргументом для второй.

    SELECT UPPER(LEFT('sql-academy', 3)) AS str;
    
    Str
    SQL

Или хотим вычислить длину фамилии человека, имея строку в формате имя<пробел>фамилия. Одним из возможных способов вычисления длины фамилии может быть применение функций LENGTH и INSTR, используя формулу <длина фамилии> = <длина всей строки> - (<длина имени> + <длина пробела>):
* Значение <длина всей строки> можно получить с помощью функции LENGTH
* Для <длина имени> + <длина пробела> нужно вычислить позицию символа, где заканчивается имя, и прибавить единицу, т.к. пробел имеет длину «1». Мы можем сделать это используя лишь функцию INSTR, ориентируясь на символ «пробел»
Так как обе функции возвращают числовые литералы, мы можем выполнять арифметические операции над ними. Давайте вычтем одно из другого и получим длину фамилии (lastname_length):

    SELECT member_name,
        LENGTH(member_name) AS full_length,
        INSTR(member_name, ' ') AS firstname_with_space_length,
        LENGTH(member_name) - INSTR(member_name, ' ') AS lastname_length
    FROM FamilyMembers;

### #1.3 Исключение дубликатов, DISTINCT

В некоторых ситуациях SQL запрос на выборку может возвращать повторяющиеся строки данных.
Например, давайте выведем поле class из таблицы Student_in_class из базы данных, в которой организовано хранение информации о расписании занятий в школе.

    CREATE TABLE Student_in_class (
            id INT AUTO_INCREMENT,
            class INT,
    )

    SELECT class FROM Student_in_class;

Поскольку в одном классе возможно нахождение нескольких студентов, то не удивительно, что при выводе мы можем наблюдать одинаковые значения. Чтобы при выборке избежать такого дублирования, есть оператор DISTINCT.

**Синтаксис оператора**

SELECT [DISTINCT] {column_name} FROM {table_name};
То есть в нашем случае запрос на получение уникальных классов, в которых есть хотя бы один студент, будет выглядеть следующим образом:

    SELECT DISTINCT class FROM Student_in_class;
    DISTINCT для нескольких колонок

При использовании оператора DISTINCT для двух и более колонок будут удаляться записи, которые имеют одинаковые значения по всем полям.

## #2 Условный оператор WHERE

Ситуация, когда требуется сделать выборку по определённому условию, встречается очень часто. Для этого в операторе SELECT существует оператор WHERE, после которого следуют условия для ограничения строк. Если запись удовлетворяет этому условию, то попадает в результат, иначе отбрасывается.
Общая структура запроса с оператором WHERE

    SELECT [DISTINCT] {column_name} FROM {table_name}
    WHERE условие_на_ограничение_строк
    
    [логический_оператор другое_условие_на_ограничение_строк];

Например, запрос с использованием оператора WHERE может выглядеть следующим образом:

    SELECT * FROM Student
    WHERE first_name = "Grigorij" AND YEAR(birthday) > 2000;

**Операторы сравнения**

Операторы сравнения служат для сравнения 2 выражений, результатом которого может являться:
* true (что эквивалентно 1)
* false (что эквивалентно 0)
* NULL

| Оператор | Обозначение | Описание |
| ------------- | ------------- | ------------- |
| Равенство | = | Если оба значения равны, то результат будет равен 1, иначе 0 |
| Эквивалентность | <=> | Аналогичен оператору равенства, за исключением того, что результат будет равен 1 в случае сравнения NULL с NULL и 0, когда идёт сравнение любого значения с NULL |
| Неравенство | <> или != | Если оба значения не равны, то результат будет равен 1, иначе 0 |
| Меньше | < | Если одно значение меньше другого, то результат будет равен 1, иначе 0 |
| Меньше или равно | <= | Если одно значение меньше или равно другому, то результат будет равен 1, иначе 0 |
| Больше | > | Если одно значение больше другого, то результат будет равен 1, иначе 0 |
| Больше или равно | >= | Если одно значение больше или равно другому, то результат будет равен 1, иначе 0 |

Результатом сравнения любого значения с NULL является NULL. Исключением является оператор эквивалентности.

    SELECT
        2 = 1,
        'a' = 'a',
        NULL <=> NULL,
        2 <> 2,
        3 < 4,
        10 <= 10,
        7 > 1,
        8 >= 10;

**Логические операторы**

Логические операторы необходимы для связывания операторов сравнения.

| Оператор | Описание |
| ------------- | ------------- |
| NOT | Меняет значение оператора сравнения на противоположный |
| OR | Возвращает общее значение выражения истинно, если хотя бы одно из них истинно |
| AND | Возвращает общее значение выражения истинно, если они оба истинны |
| XOR | Возвращает общее значение выражения истинно, если один и только один аргумент является истинным |

Пример:

    SELECT * FROM Trip
    WHERE plane = 'Boeing' AND NOT town_from = 'London';

### #2.1 Операторы IS NULL, BETWEEN, IN

Мы уже познакомились с синтаксисом оператора WHERE и операторами сравнения, но помимо них в условных запросах мы можем использовать следующие полезные операторы:
* IS NULL
* BETWEEN
* IN

Давайте рассмотрим их применение.

**IS NULL**

Оператор IS NULL позволяет узнать равно ли проверяемое значение NULL, т.е. пустое ли значение.
Для примера выведем всех преподавателей, у кого отсутствует отчество:

    SELECT * FROM Teacher
    WHERE middle_name IS NULL;

Для использования отрицания, то есть, если мы хотим найти все записи, где поле не равно NULL, мы должны использовать следующий синтаксис:

    SELECT * FROM Teacher
    WHERE middle_name IS NOT NULL;
    BETWEEN

Оператор BETWEEN min AND max позволяет узнать расположено ли проверяемое значение столбца в интервале между min и max, включая сами значения min и max. Он идентичен условию:

    WHERE field >= min AND field <= max

Используется данный оператор следующим образом:

    SELECT * FROM Payments
    WHERE unit_price BETWEEN 100 AND 500;

В качестве результата вернутся все записи из таблицы Payments, где значение поля unit_price будет от 100 до 500.

**IN**

Оператор IN позволяет узнать входит ли проверяемое значение столбца в список определённых значений.

    SELECT * FROM FamilyMembers
    WHERE status IN ('father', 'mother');

### #2.2 Оператор LIKE

Оператор LIKE используется при условных запросах, когда мы хотим узнать соответствует ли строка определённому шаблону.
Например, у нас есть таблица Users, в которой есть поле email:

    SELECT name, email FROM Users;

Допустим, мы хотим найти всех пользователей, чья почта лежит в домене второго уровня «hotmail». Т.е. нужно отобрать только те записи, что отвечают условию:
* после символа «@» следует «hotmail»
* после «hotmail» следует символ «.» и далее любая последовательность символов

Для таких нетривиальных поисков по строковым полям и нужен оператор LIKE.

**Синтаксис**

    WHERE поле_таблицы [NOT] LIKE шаблон_строки

Шаблон может включать следующие специальные символы:

| Символ | Описание |
| ------------- | ------------- |
| % | Последовательность любых символов (число символов в последовательности может быть от 0 и более) |
| _ | Любой идентичный символ |

Так наш запрос на поиск пользователей в домене «hotmail» может выглядеть следующим образом:

    SELECT name, email FROM Users
    WHERE email LIKE '%@hotmail.%'

Примеры

    WHERE поле_таблицы LIKE 'text%'

Сопоставляется любым строкам, начинающимся на «text»

    WHERE поле_таблицы LIKE '%text'

Сопоставляется любым строкам, заканчивающимся на «text»

    WHERE поле_таблицы LIKE '_ext'

Сопоставляется строкам, имеющим длину 4 символа, при этом 3 последних обязательно должны быть «ext». Например, слова «text» и «next»

    WHERE поле_таблицы LIKE 'begin%end'

Сопоставляется строкам, начинающихся на «begin» и заканчивающихся на «end»

В MySQL по умолчанию шаблоны не чувствительны к регистру

**ESCAPE-символ**

ESCAPE-символ используется для экранирования специальных символов (% и \). В случае если вам нужно найти строки, вы можете использовать ESCAPE-символ.
Например, вы хотите получить идентификаторы задач, прогресс которых равен 3%:

    SELECT job_id FROM Jobs
    WHERE progress LIKE '3!%' ESCAPE '!';

Если бы мы не экранировали трафаретный символ, то в выборку попало бы всё, что начинается на 3.

### #2.3 Оператор REGEXP

Оператор REGEXP (или его синоним RLIKE) в SQL используется для поиска и обработки строковых данных с помощью регулярных выражений. Регулярные выражения предоставляют мощные возможности для сложных шаблонов поиска, которые трудно реализовать с помощью оператора LIKE.

**Когда использовать REGEXP вместо LIKE?**

Оператор LIKE удобен для простых шаблонов поиска, таких как поиск строк, начинающихся или заканчивающихся на определённый набор символов, или содержащих определённые подстроки. Однако, если требуется более сложный и гибкий поиск, например, поиск по нескольким условиям или использование специальных символов и диапазонов, оператор REGEXP станет незаменимым инструментом.
Синтаксис регулярных выражений

    WHERE table_field REGEXP 'pattern';

Где pattern — это регулярное выражение, задающее шаблон поиска.
Важные нюансы

1.	Регистронезависимость
По умолчанию регулярные выражения в MySQL не чувствительны к регистру. Например, выражение REGEXP 'abc' найдёт строку и abc, и Abc, и ABC.

2.	Специальные символы
Некоторые символы имеют особое значение в регулярных выражениях и требуют экранирования (например, ., *, +, ?, [, ], (, ), {, }, |, \). Для экранирования используется обратная косая черта \.

**Специальные символы и структуры**

| Символы и структуры | Чему соответствует |
| ------------- | ------------- |
| * | 0 или более экземпляров предшествующей строки |
| +	| 1 или более экземпляров предшествующих строк |
| . | Любой одиночный символ |
| ? | 0 или 1 экземпляр предшествующей строки |
| ^ | Соответствует началу строки |
| $ | Соответствует окончанию строки |
| [abc]	| Любой символ, указанный в квадратных скобках |
| [^abc] | Любой символ, не указанный в квадратных скобках |
| [A-Z], [А-Я] | Соответствует любой заглавной букве латинского и кириллического алфавита соответственно |
| [a-z], [а-я]	| Соответствует любой строчной букве латинского и кириллического алфавита соответственно |
| [0-9] |	Соответствует любой цифре |
| p1|p2|p3	| Соответствует любому из паттернов p1 или p2 или p3 |
| {n} |	n экземпляров предыдущей строки |
| {m,n}	| от m до n экземпляров предыдущей строки |

**Примеры с объяснением**

* Получим всех пользователей, чьи имена начинаются на «John»:

    SELECT * FROM Users WHERE name REGEXP '^John';

| id |	name |	email |	email_verified_at |	password |	phone_number |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 18 |	John Travolta |	wainwrig@msn.com |	2016-11-19T12:30:43.000Z |	fzjhl0v82o0amalr8649 |	+1 202 555 0176 |
| 28 |	Johnny Depp | cgarcia@yahoo.ca | 2017-05-26T01:19:06.000Z |	qpp6hbnae42cdhmxlk4j |	+7 401 195 7363 |

Это выражение ищет строки, начинающиеся с «John». Символ ^ указывает на начало строки.

*Выведем все школьные предметы, название которых оканчивается на букву «e» или «y»:

    SELECT * FROM  Subject WHERE name REGEXP '[ey]$';

| id | name |
| ------------- | ------------- |
| 2	| Russian language |
| 3 | Literature |
| 5	| Chemistry |

В этом примере, [ey] определяет список возможных значений для паттерна $, определяющего на что должна заканчиваться строка.

* Найдём всех пользователей, чей адрес электронной почты oканчивается на «@outlook.com» или на «@icloud.com»:

    SELECT * FROM Users WHERE email REGEXP '@(outlook.com|icloud.com)$';

| id |	name |	email |	email_verified_at |	password |	phone_number |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 7	| Samuel L. Jackson | moonlapse@outlook.com | 2018-07-19T11:16:13.000Z | i6yvht95527z3idgqx9y | +1 202 555 0162 |
| 13 |	Steve Martin |	nelson@outlook.com | 2016-07-29T04:25:00.000Z  | w76yphg3kvzg77ilmxfs | +1 202 555 0138 |

Здесь также используется $ для обозначения конца строки и | для указания нескольких вариантов.

* Найдём всех пользователей, чей номер телефона не содержит цифр «2» и «8»:

    SELECT * FROM Users WHERE phone_number REGEXP '^[^28]*$';

| id |	name |	email |	email_verified_at |	password |	phone_number |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |
| 27 |	Brad Pitt |	kewley@optonline.net |	2017-02-11T05:45:15.000Z | 829j2ygocn8btzae49kv | +7 401 741 3797 |
|28	| Johnny Depp | cgarcia@yahoo.ca | 2017-05-26T01:19:06.000Z | qpp6hbnae42cdhmxlk4j | +7 401 195 7363 |

В этом примере символ [^28] обозначает любой символ, кроме «2» и «8», а * означает любое количество таких символов. Символы ^ и $ указывают на начало и конец строки соответственно, гарантируя, что вся строка соответствует шаблону.

* Найдём всех пользователей, чей номер телефона начинается на «+7»

    SELECT name, phone_number FROM Users WHERE phone_number REGEXP '^\\+7';

| name	| phone_number |
| ------------- | ------------- |
| Hideo Kojima | +7 401 452 0052 |
| ClINT Eastwood | +7 401 722 0912 |

В этом примере ^ означает начало строки. То есть, мы ищем строки, которые начинаются с определённого шаблона.
Поскольку + является специальным символом в регулярных выражениях, его нужно экранировать двойным обратным слэшем (\\), чтобы он воспринимался как обычный символ +. В результате, \\+ соответствует знаку + в строке.

## #3 Сортировка, оператор ORDER BY

При выполнении SELECT запроса, строки по умолчанию возвращаются в неопределённом порядке. Фактический порядок строк в этом случае зависит от плана соединения и сканирования, а также от порядка расположения данных на диске, поэтому полагаться на него нельзя. Для упорядочивания записей используется конструкция ORDER BY.

**Общая структура запроса с оператором ORDER BY**

    SELECT {column_name #1}, {column_name #2} FROM {table_name}
    WHERE ...
    ORDER BY {column_name #1} [ASC | DESC][, {column_name_n} [ASC | DESC]];

Где ASC и DESC - направление сортировки:

* ASC - сортировка по возрастанию (по умолчанию);
* DESC - сортировка по убыванию.

**Сортировка по возрастанию и убыванию для основных типов**

| Тип данных |	ASC (по возрастанию) |	DESC (по убыванию) |
| ------------- | ------------- | ------------- | 
| Строковый тип | Лексикографический (алфавитный) порядок от «A» до «Z» (или от «А» до «Я»); Сначала идут записи начинающиеся на «a», затем на «b» и т.д. | Лексикографический порядок от «Z» до «A» (или от «Я» до «А»); Сначала идут записи начинающиеся на «z», «y» и т.д.|
| Числовой тип | От меньшего к большему | От большего к меньшему |
| Дата и время | От более ранней даты/времени к более поздней; Например, сначала 01.01.2024, затем 01.02.2024 | От более поздней даты/времени к более ранней; Например, сначала 01.02.2024, затем 01.01.2024 |
| Булевый тип | False идёт перед True | True идёт перед False |

**Сортировка по нескольким столбцам**

Для сортировки результатов по двум или более столбцам их следует указывать через запятую.

    ...ORDER BY {column_name #1} [ASC | DESC], {column_name #2} [ASC | DESC]; 

Данные будут сортироваться по первому столбцу, но в случае если попадаются несколько записей с совпадающими значениями в первом столбце, то они сортируются по второму столбцу. Количество столбцов, по которым можно отсортировать, не ограничено.

Правило сортировки применяется только к тому столбцу, за которым оно следует.
ORDER BY {column_name #1}, {column_name #2} DESC не то же самое, что
ORDER BY {column_name #1} DESC, {column_name #2} DESC

Выведем информацию о полётах, отсортированную по городу вылета самолёта в порядке возрастания и по городу прибытия в аэропорт в порядке убывания, из таблицы Trip:

    SELECT DISTINCT town_from, town_to 
    FROM Trip
    ORDER BY town_from, town_to DESC;

| town_from | town_to |
| ------------- | ------------- |
| London | Singapore |
| London | Paris |
| Moscow | Rostov |
| Paris | Rostov |

В данном примере в начале записи сортируются по полю town_from. Затем, отрабатывает обратная сортировка по полю town_to для групп строк у которых в столбце town_from одинаковое значение.

## #4 Группировка, оператор GROUP BY

Выполним запрос:

    SELECT id, home_type, has_tv, price 
    FROM Rooms;

| id | home_type | has_tv | price |
| ------------- | ------------- | ------------- | ------------- |    
| 1 | Private room | 1 | 149 |
| 2 | Entire home/apt | 0 | 225 |
| 3 | Private room | 1 | 150|
| 4 | Shared room | 1 | 240 |
| 5 | Entire home | 0 | 60 |
| 6 | Shared room | 1 | 89 |     

Так мы получили информацию по каждому сдаваемому жилому помещению. А что если мы хотим получить информацию не о каждой записи отдельно, а о группах, которые они образуют?

Например, такими группами могут выступать записи разбитые по типу жилья:
* Shared room (аренда комнаты на несколько человек);
* Private room (аренда целой комнаты);
* Entire home/apt (аренда целой квартиры).

Эти группы включают разные записи в таблице и, соответственно, обладают разными характеристиками, которые нам могут быть весьма полезны.

Такой полезной информацией о группах может быть:
* средняя стоимость аренды комнаты или целого жилого помещения;
* количество сдаваемых жилых помещений каждого типа. 

Для ответов на все эти и многие другие вопросы есть оператор GROUP BY.

**Общая структура запроса с GROUP BY**

    SELECT [литералы, агрегатные_функции, поля_группировки]
    FROM {column_table}
    GROUP BY поля_группировки;

Для того, чтобы записи у нас образовали группы по типу жилья мы должны после GROUP BY указать home_type, т.е. поле, по которому будет происходить группировка.

    SELECT home_type FROM Rooms
    GROUP BY home_type
    home_type

| home_type |
| ------------- |    
| Private room |
| Entire home/apt |
| Shared room |

Следует иметь в виду, что для GROUP BY все значения NULL трактуются как равные, т.е. при группировке по полю, содержащему NULL-значения, все такие строки попадут в одну группу.
При использовании оператора GROUP BY мы перешли от работы с отдельными записями на работу с образовавшимися группами. В связи с этим мы не можем просто вывести любое поле из записи (например, has_tv или price), как мы это могли делать раньше. Так как в каждой группе может быть несколько записей и в каждой из них в этом поле может быть разное значение.

При использовании GROUP BY мы можем выводить только:
* литералы, т.е. указанное явным образом фиксированные значения.

Мы можем их выводить, так как это фиксированные значения, которые ни от чего не зависят.
Например,

    SELECT home_type, "literal" 
    FROM Rooms
    GROUP BY home_type;

| home_type	| literal |
| ------------- | ------------- |
| Private room	| literal |
| Entire home/apt |	literal |
| Shared room |	literal |

* результаты агрегатных функций, т.е. вычисленные значения на основании набора значений.

Детально агрегатные функцияи будут расмотрены в следующем разделе. Но для примера рассмотрим агрегатную функцию AVG.
Функция AVG принимает в качестве аргумента название поля, по которому мы хотим вычислить среднее значение для каждой группы.

    SELECT home_type, AVG(price) as avg_price FROM Rooms
    GROUP BY home_type

| home_type	| avg_price |
| ------------- | ------------- |
| Private room | 89.4286 |
| Entire home/apt |	148.6667 |
| Shared room | 40 |

Так выполненный запрос сначала разбивает все записи из таблицы Rooms на 3 группы, опираясь на поле home_type. Далее, для каждой группы суммирует все значения, взятые из поля price у каждой записи, входящей в текущую группу, и затем полученный результат делится на количество записей в данной группе.

* поля группировки.

Мы можем их выводить, так как в рамках одной группы поля, по которым осуществлялась группировка, одинаковые.
Группировка по 2 и более полям

**Группировка по 2 и более полям**

При группировке по 2 и более полям принцип остается такой же, только теперь образовавшиеся группы дополнительно разбиваются на более мелкие группы в зависимости от второго поля группировки.

### # 4.1 Агрегатные функции

Агрегатная функция – это функция, которая выполняет вычисление на наборе значений и возвращает одиночное значение.

**Общая структура запроса с агрегатной функцией**

    SELECT [литералы, агрегатные_функции, поля_группировки]
    FROM имя_таблицы
    GROUP BY поля_группировки;

Например, запрос с использованием агрегатной функции AVG может выглядеть так:

    SELECT home_type, AVG(price) as avg_price FROM Rooms
    GROUP BY home_type

| home_type	| avg_price |
| ------------- | ------------- |
| Private room | 89.4286 |
| Entire home/apt |	148.6667 |
| Shared room | 40 |

**Описание агрегатных функций**

| Функция | Описание |
| ------------- | ------------- |
| SUM(поле_таблицы) | Возвращает сумму значений |
| AVG(поле_таблицы) | Возвращает среднее значение |
| COUNT(поле_таблицы) | Возвращает количество записей |
| MIN(поле_таблицы) | Возвращает минимальное значение |
| MAX(поле_таблицы) | Возвращает максимальное значение |

Агрегатные функции применяются для значений, не равных NULL. Исключением является функция COUNT(*).

**Примеры**

* Найдём количество каждого вида жилья и отсортируем полученный список по убыванию:

    SELECT home_type, COUNT(*) as amount FROM Rooms
    GROUP BY home_type
    ORDER BY amount DESC

| home_type	| amount |
| ------------- | ------------- |
| Private room | 28 |
| Entire home/apt | 21 |
| Shared room | 1 |

* Для каждого жилого помещения найдём самую позднюю дату выезда (поле end_date):

    SELECT room_id, MAX(end_date) AS last_end_date FROM Reservations
    GROUP BY room_id


| room_id	| last_end_date |
| ------------- | ------------- |
| 1 | 2019-02-04T12:00:00.000Z |
| 2 | 2020-03-23T09:00:00.000Z |
| 13 | 2020-04-21T10:00:00.000Z |
| 16 | 2019-06-24T10:00:00.000Z |
| 21 | 2020-02-29T10:00:00.000Z |
| 19 | 2020-05-02T10:00:00.000Z |
| 8 | 2020-01-21T12:00:00.000Z |
| 7 | 2019-09-17T10:00:00.000Z |

## #5 Оператор HAVING

Оператор HAVING позволяет выполнить фильтрацию групп, то есть определяет, какие группы будут включены в выходной результат.

Оператор HAVING используется в сочетании с GROUP BY, чтобы ограничить группы возвращаемых строк, только тех, чьи условия истинны.

    SELECT home_type, AVG(price) as avg_price FROM Rooms
    GROUP BY home_type
    HAVING avg_price > 50

| home_type	| avg_price |
| ------------- | ------------- |
| Private room | 89.4286 |
| Entire home/apt |	148.6667 |

**Порядок выполнения SQL запроса**

* SELECT -  получение всех записей из таблицы

* WHERE - фильтрация записей по определенным условиям

* GROUP BY - формирование групп на основе записей после  фильтрации

* HAVING - фильтрация групп по определенным условиям

* ORDER BY - сортировка полученных результатов

**Общая структура запроса с оператором HAVING**

    SELECT [константы, агрегатные_функции, поля_группировки]
    FROM имя_таблицы
    WHERE условия_на_ограничения_строк
    GROUP BY поля_группировки
    HAVING условие_на_ограничение_строк_после_группировки
    ORDER BY условие_сортировки

**Пример использования HAVING**

Для примера давайте получим минимальную стоимость каждого типа жилья c телевизором. При этом нас интересуют только типы жилья, содержащие как минимум 5 жилых помещений, относящихся к ним.
Чтобы получить такой результат мы должны:

* Сначала получить все данные из таблицы

    SELECT ... FROM Rooms;

* Затем выбрать из всех записей таблицы Room только интересующие нас, т.е. только жильё с телевизором

    SELECT ... FROM Rooms
    WHERE has_tv = True

* Затем сгруппировать данные записи о жилых помещений по их типу

    SELECT ... FROM Rooms
    WHERE has_tv = True
    GROUP BY home_type

* После этого отфильтровать полученные группы по условию. Нас интересуют группы, имеющие как минимум 5 представителей

    SELECT ... FROM Rooms
    WHERE has_tv = True
    GROUP BY home_type
    HAVING COUNT(*) >= 5

* И под конец, посмотреть что нас просят в задании и, соответственно, добавить вывод необходимой информации. В нашем случае, нам необходимо вывести название типа жилья и его минимальную стоимость.

    SELECT home_type, MIN(price) as min_price FROM Rooms
    WHERE has_tv = True
    GROUP BY home_type
    HAVING COUNT(*) >= 5;

