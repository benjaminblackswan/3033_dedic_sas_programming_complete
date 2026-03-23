## 37. Arrays 1 (Recoding Variables)

first read in the 6var.txt

```
data sixvar;
infile '/home/u62043935/Dedic/6var.txt';
input var_1 var_2 var_3 var_4 var_5 var_6;
run;

proc print data=sixvar; run;
```

<img width="296" height="173" alt="image" src="https://github.com/user-attachments/assets/eba8e3a7-4d01-40c8-87c9-ebba1553fc90" />


```
data sixvar;
infile '/home/u62043935/Dedic/6var.txt';
input var_1 var_2 var_3 var_4 var_5 var_6;
run;

data recode_array;
set sixvar;
array recodearr(6) var_1-var_6;
DO i = 1 to 6;
if recodearr(i) < 40 then recodearr(i)=.;
end;
run;

proc print data=recode_array;
var var_1-var_6;
run;
```

<img width="294" height="172" alt="image" src="https://github.com/user-attachments/assets/5f4e9f73-0902-4805-b3ff-e49ea23ac01a" />

## 38. Arrays 2 (Constructing new variables)

```
data sixvar;
infile '/home/u62043935/Dedic/6var.txt';
input var_1 var_2 var_3 var_4 var_5 var_6;
run;

data newvar;
set sixvar;
array ovar(6) var_1-var_6;
array newtax(6) tax_1-tax_6;
do i = 1 to 6;
newtax(i) = ovar(i) * 0.05 + ovar(i);
end;
run;

proc print data=newvar;
var var_1-var_6 tax_1-tax_6;
run;
```

<img width="558" height="176" alt="image" src="https://github.com/user-attachments/assets/92bdd05b-15a3-4dd2-9b19-4b07b57574b8" />


