# SQL_courses

Рассказываю о своих навыках, полученных на [курсах от Stepik](https://stepik.org/course/63054/syllabus).

*Задание:*
Для каждой отдельной книги необходимо вывести информацию о количестве проданных экземпляров и их стоимости за текущий и предыдущий год . Вычисляемые столбцы назвать Количество и Сумма. Информацию отсортировать по убыванию стоимости.

*Фрагмент логической схемы базы данных:*


![](https://github.com/SvetlanaKhlobustova50809/SQL_courses/blob/main/shop14.jpg)

*Информация о продажах прошлого года хранится в таблице buy_archive следующей структуры:*


![](https://github.com/SvetlanaKhlobustova50809/SQL_courses/blob/main/shop15.jpg)

**Мой код:**
```
select title, sum(amount1) as 'Количество',sum(cost) as 'Сумма'
from (
select title,sum(buy_book.amount) as amount1,sum(book.price*buy_book.amount) as cost
from book
             inner join buy_book using(book_id)
             inner join buy using(buy_id)
             inner join buy_step using(buy_id)
             inner join step using(step_id)
where not (date_step_end is null) and step_id = 1
group by 1
union all
select title,sum(buy_archive.amount) as amount1,sum(buy_archive.amount*buy_archive.price) as cost
    from book
    inner join buy_archive using(book_id)
    group by 1
) as full_table
group by full_table.title
order by 3 desc;
```

**Вывод:**


![](https://github.com/SvetlanaKhlobustova50809/SQL_courses/blob/main/2022-07-25_13-17-15.png)



**Сертификат о прохождении курсов:**


![](https://github.com/SvetlanaKhlobustova50809/SQL_courses/blob/main/SQL%20курс%20Степик_page-0001.jpg)
