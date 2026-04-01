## 77. How to Perform an Inner Join

```
data humanresources;
input empid $ title $ gender $;
datalines;
000123 Sales Male
000124 Sales Female
000125 Marketing Female
000126 Finance Female
000127 HR Male
000128 Sales Female
Run;

data contactinfo;
input empid $ fname $ phone email $50.;
datalines;
000123 Larry 4554545 larry@email.com
000124 Susan 123407 Susan@email.com
000125 Jen 125123 Jen@email.com
000126 Gloria 6343245 Gloria@email.com
000127 James 1236345 James@email.com
000128 Sharon 62345 Sharon@email.com
run;

proc sql;
select hr.*, fname, phone, email
from humanresources as hr
inner join contactinfo as ci
on hr.empid = ci.empid
order by hr.empid;
quit;
```

<img width="430" height="176" alt="image" src="https://github.com/user-attachments/assets/a978edc9-d502-408e-8736-2c656fd6b757" />



## 78. How to Join Three Tables
```
data humanresources;
input empid $ title $ gender $;
datalines;
000123 Sales Male
000124 Sales Female
000125 Marketing Female
000126 Finance Female
000127 HR Male
000128 Sales Female
Run;

data contactinfo;
input empid $ fname $ home_phone email $50.;
datalines;
000123 Larry 4554545 larry@email.com
000124 Susan 123407 Susan@email.com
000125 Jen 125123 Jen@email.com
000126 Gloria 6343245 Gloria@email.com
000127 James 1236345 James@email.com
000128 Sharon 62345 Sharon@email.com
run;

data backupcontacts;
input empid $ cell_phone;
datalines;
000123 3333333
000124 3333444
000125 3333555
000126 3333666
000127 3333777
000128 3333888
run;

proc sql;
select hr. *, fname, home_phone, email, cell_phone
from humanresources as hr
join contactinfo as ci
on hr.empid = ci.empid
join backupcontacts as bc
on ci.empid = bc.empid
;
quit;
```

<img width="478" height="156" alt="image" src="https://github.com/user-attachments/assets/aaf06377-f239-4454-bf8c-4f5b1ccc5c92" />




## 79. How to Perform a Left/Right Join

```
data idfname;
input empid $ fname $;
datalines;
000123 John
000124 Mary
000125 Shanan
000126 Jerry
000127 Samantia
000128 Doona
;
run;

data contactinfo;
input empid $ lname $20.;
datalines;
000123 Marris
000333 Ducet
000444 Slater
000126 Smith
000127 Jefferson
000128 Barrister
;
run;

proc sql;
select idfname.*, lname
from idfname
left join contactinfo
on idfname.empid = contactinfo.empid
order by empid
;
quit;
```
<img width="186" height="153" alt="image" src="https://github.com/user-attachments/assets/35dceaf7-532f-4e8c-8ed1-b6b0cea8fe4f" />


## 80. How to Perform a Full Join

```
data data1;
input empid $ fname $ height;
datalines;
333 John 175
999 Mary 155
125 Shawn 190
126 James 187
run;

proc print data=data1; run;

data data2;
input empidd $ fnamee $ weight;
datalines;
123 John 155
124 Mary 130
125 Shawn 230
126 James 225
run;

proc print data=data2; run;

proc sql;
select *
from data1 as d full join data2 as dd
on d.empid = dd.empidd;
quit;
```

<img width="356" height="500" alt="image" src="https://github.com/user-attachments/assets/84c1110f-4b77-486d-a758-5a08db1db83a" />

### Using Coalesce function in a full join


```
data data1;
input empid $ fname $ height;
datalines;
333 John 175
999 Mary 155
125 Shawn 190
126 James 187
run;

proc print data=data1; run;

data data2;
input empidd $ fnamee $ weight;
datalines;
123 John 155
124 Mary 130
. Shawn 230
126 James 225
run;

proc print data=data2; run;

proc sql;
select *
from data1 as d full join data2 as dd
on d.empid = dd.empidd;
quit;

proc sql;
select
coalesce(dd.empidd, d.empid) as empid
, coalesce(dd.fnamee, d.fname) as fname
, height
, weight
from data1 as d full join data2 as dd
on d.empid = dd.empidd;
quit;
```

<img width="332" height="732" alt="image" src="https://github.com/user-attachments/assets/1519e614-0709-4b3c-b0fd-1a46d5a1ccb1" />























