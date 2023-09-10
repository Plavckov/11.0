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
select month(payment_date) as p_date, SUM(amount) as amount, count(r.rental_id) as count_rental
from payment
         join rental r on r.rental_id = payment.rental_id
group by p_date
order by amount desc
limit 1
```
