### Задание 1

Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

```sql
select district
from address
where district like "K%a" and  district not like "% %"
```

### Задание 2

Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года **включительно** и стоимость которых превышает 10.00.

```sql
select amount, date(payment_date)
from payment
where day(payment_date) between 15 and 18
and  month(payment_date) = 6
and year(payment_date) = 2005
and amount >= 10.00
``

### Задание 3

Получите последние пять аренд фильмов.

```sql
select *
from rental
order by rental_date desc
limit 5
```

### Задание 4

Одним запросом получите активных покупателей, имена которых Kelly или Willie. 

Сформируйте вывод в результат таким образом:
- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
- замените буквы 'll' в именах на 'pp'.

```sql
select concat(first_name, " ", last_name) as origin,
       lower(concat(replace(lower(first_name), "ll", "pp"), " ", last_name)) as modify
from customer
where lower(first_name) in ('kelly', 'willie')
```
