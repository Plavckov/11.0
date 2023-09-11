### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

```sql
select concat(s.first_name, " ", s.last_name) as staff,
       c.city                                 as city,
       count(c2.customer_id)                  as customres_count
from store
         join staff s on store.manager_staff_id = s.staff_id
         join address a on a.address_id = s.address_id
         join city c on a.city_id = c.city_id
         join customer c2 on store.store_id = c2.store_id
group by store.store_id
having customres_count > 300
```

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

```sql
select count(*) as count_film from film
where length > (select AVG(length) from film)
```

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

```sql
select	t.amount_of_payments,
	t.month_of_payments,
	(select count(r.rental_id)
	from sakila.rental r
	where DATE_FORMAT(r.rental_date, '%M %Y') = t.month_of_payments) 'count_of_rent'
from (
  select SUM(p.amount) 'amount_of_payments', DATE_FORMAT(p.payment_date, '%M %Y') 'month_of_payments' 
  from sakila.payment p 
  group by DATE_FORMAT(p.payment_date, '%M %Y')) t
order by t.amount_of_payments desc  
limit 1;
```
