# 12-3
Домашнее задание к занятию «SQL. Часть 1»
#### Задание 1
Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

```
SELECT DISTINCT district 
FROM address 
WHERE district  LIKE 'k%a' and district not LIKE  '% %';

```
<img width="551" height="288" alt="image" src="https://github.com/user-attachments/assets/8743bcb7-d223-486e-aded-405a671df741" />


#### Задание 2
Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.

```
SELECT *
FROM payment
WHERE payment_date  BETWEEN '2005-06-15' and '2005-06-19' and amount > 10
ORDER BY payment_date;
```
<img width="847" height="302" alt="image" src="https://github.com/user-attachments/assets/f65973f6-36fd-444c-a306-3b52187b5840" />


#### Задание 3
Получите последние пять аренд фильмов.

```
SELECT *  
FROM rental   
ORDER by rental_date DESC 
LIMIT 5;
```
<img width="884" height="276" alt="image" src="https://github.com/user-attachments/assets/eadab436-d28e-4bd0-9ef7-c58207452b9f" />

#### Задание 4
Одним запросом получите активных покупателей, имена которых Kelly или Willie.

Сформируйте вывод в результат таким образом:

все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
замените буквы 'll' в именах на 'pp'.
```
SELECT LOWER(REPLACE(first_name, 'L', 'p')), LOWER(last_name) 
FROM customer
WHERE first_name LIKE 'Willie' OR first_name  LIKE 'Kelly';
```
<img width="572" height="242" alt="image" src="https://github.com/user-attachments/assets/9ea55c95-648b-4b32-88f0-b347c403d9c1" />


Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

#### Задание 5*
Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.
```
SELECT email, SUBSTRING_INDEX(email , '@', 1), SUBSTRING_INDEX(email , '@', -1)
FROM customer;
```
<img width="904" height="409" alt="image" src="https://github.com/user-attachments/assets/34f95db6-0e68-4c2a-bae6-b4b091c00ea0" />


#### Задание 6*
Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.

```
SELECT email  , SUBSTRING_INDEX(email  , '@', 1), 
CONCAT ( LEFT(UPPER(SUBSTRING_INDEX(email  , '@', 1)), 1), LOWER(SUBSTR((SUBSTRING_INDEX(email , '@',1)),2))) as '1' ,  
SUBSTRING_INDEX(email  , '@', -1) ,
CONCAT(LEFT(UPPER(SUBSTRING_INDEX(email  , '@', -1)), 1), LOWER(SUBSTR((SUBSTRING_INDEX(email , '@',-1)),2))) as '2'
FROM customer c;
```
<img width="898" height="293" alt="image" src="https://github.com/user-attachments/assets/dd7a4230-b341-41d8-8106-ace2767d7a67" />
