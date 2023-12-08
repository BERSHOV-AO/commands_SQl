### SQL ###


docker run -v /pg_data:/var/lib/postgresql/data -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres

docker run -e POSTGRES_PASSWORD=mypass -p 5432:5432 postgres:9.6.24

docker run -v /pg_data:/var/lib/postgresql/data -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres




1. create schema netology2; - создаем схему под названием netology2

2. serial- это формат с автоинкрементном, то есть serial это int + auto_increment, primary key - данный ключ
будет приватным, автоматически будут настройки Not Null
   varchar - это строка, нужно поставить размер, или он сам установит (255).

create table netology2.employees(
id serial primary key,
name varchar(50),
age int,
position varchar(90)
);


3. Добавляем еще одну колонку в таблицу (колонку с зарплатой)
alter table netology2.employees add column salary int;
(add column salary int - добавляем колонку с названием salary расширением int )


4. Устанавливаем свойство на имя, что бы оно было not null
   alter table netology2.employees alter column name set not null;


5. Создаем сущность для таблицы
   (id - не будем заполнять, он будет заполняться сам)

insert into netology2.employees (name, age, position)
values('Jhon', 24, 'Java Developer');


5*. Выгружаем данные из таблицы
"*" - это покажи все данные
select* from netology2.employees;
то же самое
select id, name, age,  position, salary, company from netology2.employees;
поля можно менять местами, выборка так же поменяется


6. Удаление объекта по id
   delete from netology2.employees where id = 1;


7. Добавление в таблицу новой колонки, с дефолтным значением
   alter table netology2.employees add column company varchar default 'Sber';


8.Выборки
where - где

// всех сотрудников возраст которых больше 30
select* from netology2.employees
where age > 30;

// всех сотрудников с позицией 'Java Developer'
select* from netology2.employees
where position = 'Java Developer';

// сотрудников не зависимо от регистра
select* from netology2.employees
where lower(position)  = 'java developer';
lower() - это функция

// есть оператор and или оператор or ! выборка с условиями
select* from netology2.employees
where lower(position)  = 'java developer'
or lower(position) = 'golang developer';

// выборка по части строки = 'golang
select* from netology2.employees
where lower(position)  = 'java developer'
or lower(position) like 'golang%';


9. Сортировка - (order) - сортировка по конечной выборке
   select* from netology2.employees
   where lower(position)  = 'java developer'
   or lower(position) like 'golang%'
   order by salary; - сортирует по возрастанию зарплаты asc - по дефолту

select* from netology2.employees
where lower(position)  = 'java developer'
or lower(position) like 'golang%'
order by salary desc; - сортирует по убыванию зарплаты


10. выборка по столбцу, пример по позиции
    select position from netology2.employees


10. Убрать повторы выборок
    select distinct position from netology2.employees;


11. Количество повторов по каждому пункту position
    select position, count(*) from netology2.employees
    group by position


12. Обновление данных
    update netology2.employees set company = 'Yandex'; - у всех установится yandex

update netology2.employees set company = 'Yandex'
where id = 2; - указываем id

12*. Удаление данных
delete from netology2.employees where id = 2; удалить по id
delete from netology2.employees; - удалить все данные

14. Удаление таблицы
    drop table netology2.employees;


### ****************************************************** ###


create schema netology2;

create table netology2.employees(
id serial primary key,
name varchar(50),
age int,
position varchar(90)
);

alter table netology2.employees add column salary int;

alter table netology2.employees add column company varchar default 'Sber';

alter table netology2.employees alter column name set not null;

insert into netology2.employees (name, age, position, salary)
values('Jhon', 24, 'Java Developer', 1000);

insert into netology2.employees (name, age, position, salary, company)
values('Rick', 36, 'Golang Developer', 2000, 'Yandex');

insert into netology2.employees (name, age, position, salary)
values('Tom', 20, 'Golang Developer', 500);

insert into netology2.employees (name, age, position, salary, company)
values('Michael', 40, 'DevOps', 5000, 'Yandex');

delete from netology2.employees where id = 1;

select* from netology2.employees;

select id, name, age,  position, salary, company from netology2.employees;

select* from netology2.employees
where age > 30;

select* from netology2.employees
where position = 'Java Developer';

select* from netology2.employees
where lower(position)  = 'java developer';

select* from netology2.employees
where lower(position)  = 'java developer'
or lower(position) = 'golang developer';

select* from netology2.employees
where lower(position)  = 'java developer'
or lower(position) like 'golang%';

select* from netology2.employees
where lower(position)  = 'java developer'
or lower(position) like 'golang%'
order by salary;

select* from netology2.employees
where lower(position)  = 'java developer'
or lower(position) like 'golang%'
order by salary desc;

select distinct position from netology2.employees;

select position, count(*) from netology2.employees
group by position

select* from netology2.employees;

update netology2.employees set company = 'Yandex'
where id = 2;

delete from netology2.employees where id = 2;














