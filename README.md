## create database store;
## create table countries
(
    code           int primary key,
    name           varchar(20) unique,
    continent_name varchar(20) not null
);
create table users
(
    id            int primary key,
    ful_name      varchar(20),
    email         varchar(20) unique,
    gender        char(1) check ( gender = 'm' or gender = 'f'),
    date_of_birth varchar(15) not null,
    created_at    datetime default now(),
    country_code  int,
    foreign key (country_code) references countries (code)
);
create table orders
(
    id         int primary key,
    user_id    int,
    status     varchar(6) check (status = 'start' or status = 'finish'),
    created_at datetime default now(),
    foreign key (user_id) references users (id)
);
create table order_products
(
    order_id   int,
    product_id int,
    quantity   int default (0),
    foreign key (order_id) references orders (id),
    foreign key (product_id) references products (id)
);
create table products
(
    id         int primary key,
    name       varchar(10) not null,
    price      int      default (0),
    status     varchar(10) check ( status = 'valid' or status = 'expired'),
    created_at datetime default now()
);
# -----------------------DML--------------------------------------------------
insert into countries values (2,'saudi','riyadh');
insert into users values (3,'ahmed_khaled','ahmed@outlook.com','m','1999/2/4',default,2);
insert into orders values (4,3,'start',default);
insert into products values (8,'coca-cola',3,'valid',default);
insert into order_products values (4,8,80);
update countries set name='kuwait',continent_name='kuwait' where code=2;
delete from products where status='expired';
