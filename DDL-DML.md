### Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

1.2. Создайте учётную запись sys_temp. 

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

1.4. Дайте все права для пользователя sys_temp. 

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос: 
```sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

```sql
CREATE USER 'sys_test'@'localhost' IDENTIFIED BY 'password';
SELECT user FROM mysql.user;  
```

```sql
GRANT ALL PRIVILEGES ON *.* TO 'sys_test'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
SHOW GRANTS FOR 'sys_test'@'localhost';
```

```bash
mysql -u sys_test -p sakila < sakila-schema.sql
mysql -u sys_test -p sakila < sakila-data.sql
```

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*


![image](https://github.com/Plavckov/11.0/assets/130914025/971fd372-6b4c-4351-a517-9883e256dce4)
![image](https://github.com/Plavckov/11.0/assets/130914025/5da83037-64f7-4f6e-bc11-65aff54b583e)
![image](https://github.com/Plavckov/11.0/assets/130914025/5ee35891-7451-48fa-8495-f9b305fa3a63)



### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)
```
Название таблицы | Название первичного ключа
customer         | customer_id
```

```sql
select tab.table_name, sta.index_name as pk_name,
       sta.column_name


from information_schema.tables as tab
         inner join information_schema.statistics as sta
                    on sta.table_schema = tab.table_schema
                        and sta.table_name = tab.table_name
                        and sta.index_name = 'primary'
where tab.table_schema = 'sakila'
  and tab.table_type = 'BASE TABLE'
order by tab.table_name;
```

![image](https://github.com/Plavckov/11.0/assets/130914025/d0c43850-98b5-49c4-9389-2cfe091696cc)
