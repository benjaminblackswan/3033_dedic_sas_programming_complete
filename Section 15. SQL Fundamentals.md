## 70. SQL Syntax

in **PROC SQL** dataset and table are equivalent.


```
data employeesales;
input empid$ fname$ payperhr salesm experience;
datalines;
00123 John 80 50000 5
00124 Mary 120 75000 6
00125 Lisa 200 100000 11
00126 Joseph 70 100000 16
00131 Glenn 50 60000 1
run;

proc sql outobs=2;
select *
from employeesales
where payperhr between 50 and 100
order by fname;
quit;
```

<img width="291" height="74" alt="image" src="https://github.com/user-attachments/assets/937ff018-8da1-49b2-aed2-67047c5f378e" />

## 71. WHERE Clause


```
data employeesales;
input empid$ fname$ payperhr salesm experience;
datalines;
00123 John 80 50000 5
00124 Mary 120 75000 6
00125 Lisa 200 100000 11
00126 Joseph 70 100000 16
00131 Glenn 50 60000 1
run;

proc sql outobs=2;
select *
from employeesales
where payperhr > 80
order by fname;
quit;
```

### AND / OR

```
data employeesales;
input empid$ dep$ fname$ payperhr salesm experience;
datalines;
00123 A John 80 50000 5
00124 A Mary 120 75000 6
00125 B Lisa 200 100000 11
00126 C Joseph 70 100000 16
00131 D Glenn 50 60000 1
run;

proc sql outobs=2;
select *
from employeesales
where (dep EQ 'A' or dep EQ 'B') and payperhr > 80
order by fname;
quit;
```

<img width="335" height="69" alt="image" src="https://github.com/user-attachments/assets/acd029a5-d0cd-43e8-9bb8-907d97f34c67" />


## IN operator

```
data employeesales;
input empid$ dep$ fname$ payperhr salesm experience;
datalines;
00123 A John 80 50000 5
00124 A Mary 120 75000 6
00125 B Lisa 200 100000 11
00126 C Joseph 70 100000 16
00131 D Glenn 50 60000 1
run;

proc sql outobs=2;
select *
from employeesales
where fname in ('John', 'Glenn')
order by fname;
quit;
```


<img width="326" height="86" alt="image" src="https://github.com/user-attachments/assets/1cb40513-cd91-4b19-827f-03db21f80388" />


## 72. SELECT statement and Columns


```
data insurance;
input name$ insurancen dep$ salary bonus;
datalines;
john 4958 MAR 55000 500
don 4567 . 45000 455
Shawn 4569 AAF 45495 1000
Ron 3456 RAD 45464 3000
run;

proc sql;
select *, sum(salary, bonus) as salbonus
from insurance
where dep EQ 'MAR' or dep EQ 'RAD';
quit;
```

<img width="342" height="80" alt="image" src="https://github.com/user-attachments/assets/ba609a56-12f1-4d40-bf8f-a430b2b126a5" />


### using calculated value in the WHERE clause

```
data insurance;
input name$ insurancen dep$ salary bonus;
datalines;
john 4958 MAR 55000 500
don 4567 . 45000 455
Shawn 4569 AAF 45495 1000
Ron 3456 RAD 45464 3000
run;

proc sql;
select *, sum(salary, bonus) as salbonus
from insurance
where (dep EQ 'MAR' or dep EQ 'RAD')
and calculated salbonus gt 55000;
quit;
```

<img width="351" height="60" alt="image" src="https://github.com/user-attachments/assets/8c67bc26-d8ce-4cee-8263-a9447dac43be" />



### using FORMAT in PROC SQL

```
data insurance;
input name$ insurancen dep$ salary bonus;
datalines;
john 4958 MAR 55000 500
don 4567 . 45000 455
Shawn 4569 AAF 45495 1000
Ron 3456 RAD 45464 3000
run;

proc sql;
select *, sum(salary, bonus) as salbonus
FORMAT=dollar8.
from insurance
where (dep EQ 'MAR' or dep EQ 'RAD')
and calculated salbonus gt 55000;
quit;
```

<img width="346" height="51" alt="image" src="https://github.com/user-attachments/assets/19f4c595-ff66-4336-a9e7-09b3ef7d8407" />



## 73. CASE Logic

```
data insurance;
input name$ insurancen dep$ salary bonus;
datalines;
John 4958 MAR 55000 500
Don 4567 EEL 45000 455
Shawn 4569 AAF 45495 1000
Ron 3456 RAD 45464 3000
run;

proc sql;
select name, insurancen, dep, salary
, case dep
		when 'MAR' then 500
		when 'AAF' then 5000
		when 'RAD' then 7500
		else 0
	end as holbon
from insurance
order by name;
quit;
```

<img width="350" height="148" alt="image" src="https://github.com/user-attachments/assets/84297667-2ee7-45b6-922a-fd9aafd615dd" />



## 74. Summary Functions


```
data insurance;
input name$ insurancen dep$ salary;
datalines;
John 4958 MAR 55000
Don 4567 EEL 45000
Shawn 4569 AAF 45495
Jerry 5768 AAF 47858
Ron 3456 RAD 45464
Bonny 7778 RAD 55640
run;

proc sql;
select name, dep,
avg(salary) as avsal,
sum(salary) as sumsal,
min(salary) as minsal,
max(salary) as maxsal
from insurance
group by dep
order by avsal desc;
quit;
```

<img width="414" height="213" alt="image" src="https://github.com/user-attachments/assets/f5c9ec68-8d78-4e8e-af23-cc9808eeac48" />
























