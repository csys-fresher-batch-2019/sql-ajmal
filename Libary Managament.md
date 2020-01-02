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
book_author varchar2(100)not null,
book_edition number(10)not null,
book_price number(10),
purchased_date date ,
no_of_bks number(20) not null,
no_of_pgs number(20),
constraint book_id_prk primary key (book_id),
constraint book_edition_ck check(book_edition>=0),
constraint book_id_uk unique(book_id,book_name,book_edition),
constraint no_of_bks_ck check (no_of_bks>0));

create sequence id_seq start with 101 increment by 1;

insert into books(book_id,book_name,book_cat,book_author,book_edition,no_of_bks,no_of_pgs,purchased_date)
values (id_seq.nextval,'Electronic Devices and Circuits','Electronics','Boylested,Robert.L',1,20,342,to_date ('15-FEB-1998','dd-MM-yyyy'));

insert into books(book_id,book_name,book_cat,book_author,book_edition,book_price,no_of_bks,no_of_pgs,purchased_date)
values (id_seq.nextval,'Ciruit Theory','Electrical','salaivananan',2,158,10,234,to_date ('15-FEB-2015','dd-MM-yyyy'));

insert into books(book_id,book_name,book_cat,book_author,book_edition,no_of_bks,no_of_pgs,purchased_date)
values (id_seq.nextval,'Bsuiness @ The Speed of Thought','Bussiness','Bill Gates',1,25,145,to_date ('15-FEB-2017','dd-MM-yyyy'));

insert into books(book_id,book_name,book_cat,book_author,book_edition,book_price,no_of_bks,no_of_pgs,purchased_date)
values (id_seq.nextval,'THE LIFE,LESSON_RULES FOR SUCCESS','Bussiness','Bill Gates',1,748,15,234,to_date ('15-FEB-2017','dd-MM-yyyy'));

insert into books(book_id,book_name,book_cat,book_author,book_edition,no_of_bks,no_of_pgs,purchased_date)
values (id_seq.nextval,'Gone with the Wind','Entertainment','Margaret Mitchell',1,5,543,to_date ('15-FEB-2017','dd-MM-yyyy'));

```
### Query
```sql
select * from books
```


### Feature 2: List of Student details.

```sql
create table student(
std_id number(20),
std_name varchar2(30) not null,
std_dept varchar2(100)not null,
std_dob date,
std_mail_id varchar2(50),
std_mob_no number(12)not null,
joining_yr number(5)not null,
pass_yr number(5)not null,
constraint std_id_pk primary key (std_id));

create sequence std_seq start with 1001 increment by 1;

insert into student(std_id,std_name,std_dept,std_dob,std_mail_id,std_mob_no,joining_yr,pass_yr)
values (std_seq.nextval,'mohumkumar','EEE',to_date ('02-JAN-1993','dd-MM-yyyy'),'mohu.momo@hotmail.com',8616261872,2016,2022);

insert into student(std_id,std_name,std_dept,std_dob,std_mail_id,std_mob_no,joining_yr,pass_yr)
values (std_seq.nextval,'sandy sam','MECH',to_date ('08-DEC-1986','dd-MM-yyyy'),'sam.bro@yahoo.com',9983762351,2014,2020);

insert into student(std_id,std_name,std_dept,std_dob,std_mail_id,std_mob_no,joining_yr,pass_yr)
values (std_seq.nextval,'sugu','EEE',to_date ('12-MAR-1997','dd-MM-yyyy'),'sugu.raja@gmail.com',8616261872,2016,2022);

insert into student(std_id,std_name,std_dept,std_dob,std_mail_id,std_mob_no,joining_yr,pass_yr)
values (std_seq.nextval,'suri','MECH',to_date ('15-FEB-1998','dd-MM-yyyy'),'suri.parotta@hotmail.com',8874663782,2012,2020);


```

### Query
```sql
select * from student;
```


### Feature 3: Creation and updation of table details 
(Books taken by student and fine amount and returned date).

```sql
create table details(
book_count number(20)not null,
book_id number(20) not null,
std_id number(10) not null,
issue_date date default sysdate,
due_date date default sysdate+15,
returned_date date,
fine_amt number(20),
constraint book_id_fk foreign key (book_id) references books(book_id),
constraint book_count_pk primary key(book_count),
constraint std_id_fk foreign key (std_id) references student(std_id),
constraint details_uq unique (book_id,std_id));

create sequence book_count_sq start with 1 increment by 1;

insert into details(book_id,std_id,issue_date,due_date,book_count)
values (101,1001,to_date ('12-APR-2019','dd-MM-yyyy'),to_date('27-APR-2019','dd-MM-yyyy'),book_count_sq.nextval);
insert into details(book_id,std_id,issue_date,due_date,book_count)
values (102,1001,to_date ('12-MAY-2019','dd-MM-yyyy'),to_date('27-MAY-2019','dd-MM-yyyy'),book_count_sq.nextval);
insert into details(book_id,std_id,issue_date,due_date,book_count)
values (104,1002,to_date ('12-JUN-2019','dd-MM-yyyy'),to_date('27-JUN-2019','dd-MM-yyyy'),book_count_sq.nextval);
insert into details(book_id,std_id,issue_date,due_date,book_count)
values (105,1003,to_date ('12-DEC-2019','dd-MM-yyyy'),to_date ('27-DEC-2019','dd-MM-yyyy'),book_count_sq.nextval);
insert into details(book_id,std_id,issue_date,due_date,book_count)
values (103,1002,to_date ('12-NOV-2019','dd-MM-yyyy'),to_date ('27-NOV-2019','dd-MM-yyyy'),book_count_sq.nextval);
insert into details(book_id,std_id,issue_date,due_date,book_count)
values (102,1004,to_date ('13-DEC-2019','dd-MM-yyyy'),to_date ('28-DEC-2019','dd-MM-yyyy'),book_count_sq.nextval);
insert into details(book_id,std_id,issue_date,due_date,book_count)
values (103,1005,to_date ('12-NOV-2019','dd-MM-yyyy'),to_date ('27-NOV-2019','dd-MM-yyyy'),book_count_sq.nextval);

create or replace procedure details_pr
(i_book_id number,
i_std_id number ,
i_returned_date date,
v_error out varchar2)
as
v_due_date date ;
begin
    select due_date into v_due_date from details where book_id =i_book_id and std_id=i_std_id;
    update details set returned_date = sysdate where book_id =i_book_id and std_id =i_std_id;
    if v_due_date < i_returned_date then
        update details set fine_amt=((i_returned_date-v_due_date)*2) where book_id =i_book_id and std_id =i_std_id;
    else 
        update details set fine_amt=0 where book_id =i_book_id and std_id =i_std_id;
    end if;
commit;
exception when others then
v_error :='invalid input'; 
end details_pr;

DECLARE
i_book_id number:= 101 ;
i_std_id number:= 1001 ;
i_returned_date date:= sysdate;
v_error varchar2(100);
BEGIN
details_pr(i_book_id,i_std_id,i_returned_date, v_error );
END;
DECLARE
i_book_id number:= 102 ;
i_std_id number:= 1001 ;
i_returned_date date:= sysdate;
v_error varchar2(100);
BEGIN
details_pr(i_book_id,i_std_id,i_returned_date, v_error );
END;
DECLARE
i_book_id number:= 104 ;
i_std_id number:= 1002 ;
i_returned_date date:= sysdate;
v_error varchar2(100);
BEGIN
details_pr(i_book_id,i_std_id,i_returned_date, v_error );
END;
DECLARE
i_book_id number:= 105 ;
i_std_id number:= 1003 ;
i_returned_date date:= sysdate;
v_error varchar2(100);
BEGIN
details_pr(i_book_id,i_std_id,i_returned_date, v_error );
END;
DECLARE
i_book_id number:= 103 ;
i_std_id number:= 1002 ;
i_returned_date date:= sysdate;
v_error varchar2(100);
BEGIN
details_pr(i_book_id,i_std_id,i_returned_date, v_error );
END;
```

```
### Query
```sql
select * from details;
```

### Insertion Part
```sql
insert into books(book_id,book_name,book_cat,book_author,book_edition,no_of_bks,no_of_pgs,purchased_date)
values (id_seq.nextval,'&book_name','&book_cat','&book_author',&book_edition,&no_of_bks,&no_of_pgs,&purchased_date);

insert into student(std_id,std_name,std_dept,std_dob,std_mail_id,std_mob_no,joining_yr,pass_yr)
values (std_seq.nextval,'&std_name','&std_dept',to_date ('&std_dob','dd-MM-yyyy'),'&std_mail_id',&std_mob_no,&joining_yr,&pass_yr);

insert into details(,book_id,std_id,book_count)
values (&book_id,&std_id,book_count_sq.nextval);

DECLARE
i_book_id number:= &book_id ;
i_std_id number:= &std_id ;
i_returned_date date:= sysdate;
v_error varchar2(100);
BEGIN
details_pr(i_book_id,i_std_id,i_returned_date, v_error );
END;

```
