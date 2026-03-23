## 33. List Input

In list input, missing data has to be indicated with a period (.)

for example, the full list is

```
data sales1;
input Name$ Sales_1-Sales_4;
datalines;
Greg 10 2 40 0
John 15 5 10 100
Lisa 50 10 15 50
Mark 20 0 5 20
;
run;

proc print data=sales1; run;
```

<img width="303" height="114" alt="image" src="https://github.com/user-attachments/assets/e7718fe2-7845-40fe-8915-7e0978fc6ba6" />

now if the second value for Greg is missing

```
data sales1;
input Name$ Sales_1-Sales_4;
datalines;
Greg 10 40 0
John 15 5 10 100
Lisa 50 10 15 50
Mark 20 0 5 20
;
run;

proc print data=sales1; run;
```

<img width="316" height="91" alt="image" src="https://github.com/user-attachments/assets/4d25c992-45e0-4571-a9f2-61a6e701a58f" />

the data will get messed up as shown.

Therefore, we must indicate the missing value with a period like this.

```
data sales1;
input Name$ Sales_1-Sales_4;
datalines;
Greg 10 . 40 0
John 15 5 10 100
Lisa 50 10 15 50
Mark 20 0 5 20
;
run;

proc print data=sales1; run;
```
<img width="309" height="110" alt="image" src="https://github.com/user-attachments/assets/70f5479f-edc9-4dea-86d0-f8cf2403b7f1" />


### Issue two with List Input is, that it is limited to only 8 bytes.

eg John's full first name is Johnnathan, which is more than 8 characters.

```
data sales1;
input Name$ Sales_1-Sales_4;
datalines;
Greg 10 . 40 0
Johnnathan 15 5 10 100
Lisa 50 10 15 50
Mark 20 0 5 20
;
run;

proc print data=sales1; run;
```

Johnnathan's name will be cut off in the output.

<img width="318" height="110" alt="image" src="https://github.com/user-attachments/assets/9ec77066-f7c0-4bfb-b70f-3d7b76d5a2b3" />

## 34. Column Input

spaces are not required between values.

```
data sales1;
input Name$ 1-4 Sales_1-Sales_4 @5;
datalines;
Greg 10 2 40 0
John 15 5 10 100
Lisa 50 10 15 50
Mark 20 0 5 20
;
run;

proc print data=sales1; run;
```
<img width="301" height="112" alt="image" src="https://github.com/user-attachments/assets/690efb4a-4e56-40e1-8e78-0d72fd2059f4" />

## 35. Formatted Input And Informats

```
data police1;
infile "/home/u62043935/Dedic/londonoutcomes.csv" DSD missover firstobs=2;
length CrimeID $25 Reportedby $25 Fallswithin $25 Longitude 4 Latitude 4 Location $25 LSOAcode $25 LSOAname $25 Outcometype $25;
input CrimeID$	Reportedby$	Fallswithin$ Longitude Latitude Location$ LSOAcode$ LSOAname$ Outcometype$;
run;

proc print data=police1;
```

<img width="1116" height="450" alt="image" src="https://github.com/user-attachments/assets/da1dcfe7-7acc-482b-8ba7-65a2fa4f0ed5" />

## 36. User Defined Formats

### using informat in the proc print

```
data disease;
input diagcode$;
datalines;
001
290
800
;
run;

proc print data=disease; run;

proc format;
value $codetwo
'001' = 'Malaria'
'290' = 'Social Anxiety Disorder'
'800' = 'Leg Injury'
run;

proc print data=disease;
format diagcode $codetwo.
run;
```

<img width="171" height="227" alt="image" src="https://github.com/user-attachments/assets/5a0945cf-358f-44d6-a181-25d96f681316" />

### using PUT statement to display both diagnosic code and description

```
data disease;
input diagcode$;
datalines;
001
290
800
;
run;

proc print data=disease; run;

proc format;
value $codetwo
'001' = 'Malaria'
'290' = 'Social Anxiety Disorder'
'800' = 'Leg Injury'
run;

data diseasereal;
set disease;
diagdesc=put(diagcode,$codetwo.);
run;

proc print data=diseasereal; run;
```

<img width="233" height="236" alt="image" src="https://github.com/user-attachments/assets/93c0bed8-866b-459c-9b46-be949cae72a8" />








































