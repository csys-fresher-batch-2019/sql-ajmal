#Libary_Management
* http://libarydetails.in

##Features
*List of Books and their maintainence record.

###Feature 1: List of book details.

create table books (
book_id number(10) not null unique,
book_name varchar2(100) not null,
book_cat varchar2(100) not null,
book_author varchar2(100),
book_edition number(10),
book_price number(10)
constraint book_id_pk primary key (book_id));


###Query

select * from books
