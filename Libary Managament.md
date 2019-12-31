# Libary_Management
* http://libarydetails.in

## Features
*List of Books and their maintainence record.

### Feature 1: List of book details.
```sql
create table books (
book_id number(10)  ,
book_name varchar2(100) not null,
book_cat varchar2(100) not null,
book_author varchar2(100),
book_edition number(10),
book_price number(10),
d_o_pur date default sysdate,
no_of_bks number(20) not null,
no_of_pgs number(20),
constraint book_id_prk primary key (book_id));

create sequence id_seq start with 001 increment by 1;

insert into books(book_id,book_name,book_cat,book_author,book_edition,no_of_bks,no_of_pgs)
values (id_seq.nextval,'Electronic Devices and Circuits','Electronics','Boylested,Robert.L',1,20,342);
insert into books(book_id,book_name,book_cat,book_author,book_edition,book_price,no_of_bks,no_of_pgs)
values (id_seq.nextval,'Ciruit Theory','Electrical','salaivananan',2,158,10,234);
insert into books(book_id,book_name,book_cat,book_author,book_edition,no_of_bks,no_of_pgs)
values (id_seq.nextval,'Bsuiness @ The Speed of Thought','Bussiness','Bill Gates',1,25,145);
insert into books(book_id,book_name,book_cat,book_author,book_edition,book_price,no_of_bks,no_of_pgs)
values (id_seq.nextval,'THE LIFE,LESSON_RULES FOR SUCCESS','Bussiness','Bill Gates',1,748,15,234);
insert into books(book_id,book_name,book_cat,book_author,book_edition,no_of_bks,no_of_pgs)
values (id_seq.nextval,'Gone with the Wind','Entertainment','Margaret Mitchell',1,5,543);

```
### Query
```
select * from books
```
