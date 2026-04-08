## 109. Types of Macro Variables

```
data police1;
infile "/home/u62043935/Dedic/londonoutcomes.csv" DSD missover firstobs=2;
length CrimeID $25;
input crimeID $ ReportedF $ Fallw $ Longitude Latitude Location $ LSOAC $ LSOAN $ OutcomeT$;
run;
proc print data=police1 (obs=10); run;

proc print data = police1 (keep=CrimeID obs=10);
%let site=New York;
title "Revenues for &site Training Centre";
runs;
```

<img width="806" height="636" alt="image" src="https://github.com/user-attachments/assets/2b265a16-949c-491a-8733-da150bea8887" />


## 111. Macro Variable Assignment Rules


```
%let name = Bill Fisher;
%let name2 = ' Bill Fischer    ';
/* when invoked, SAS will remove the leading and trailing spaces */
/* %let title = "Bill Fisher's Report"; */
/* %let start =; */


data temp;
	myvar = "&name2";
/* 	myvar2 = "&title"; */
/* 	myvar3 = "&start"; */
run;

proc print data=temp; run;
```

## 112. Masking Special Characters

```
data police1;
infile "/home/u62043935/Dedic/londonoutcomes.csv" DSD missover firstobs=2;
length CrimeID $25;
input crimeID $ ReportedF $ Fallw $ Longitude Latitude Location $ LSOAC $ LSOAN $ OutcomeT$;
run;

options symbolgen;
%let text=%str(Mike%'s Report);

proc print data= police1(keep=CrimeID obs=10);
title "&text";
run;
```

<img width="249" height="311" alt="image" src="https://github.com/user-attachments/assets/29a55125-3c05-4645-a2e9-7eabde06df29" />

## 113. Macro Functions (%Index and %Upcase)

### %index

```
data police1;
infile "/home/u62043935/Dedic/londonoutcomes.csv" DSD missover firstobs=2;
length CrimeID $25;
input crimeID $ ReportedF $ Fallw $ Longitude Latitude Location $ LSOAC $ LSOAN $ OutcomeT$;
run;

%let a=a very long value;
%let b=%index(&a, v);
%put The character v appears at position &b.;
```

<img width="859" height="308" alt="image" src="https://github.com/user-attachments/assets/387d0c3b-1c5f-42aa-9231-d280133091e3" />


## 114. Macro Functions 2 (%Scan)

```
data police1;
infile "/home/u62043935/Dedic/londonoutcomes.csv" DSD missover firstobs=2;
length CrimeID $25;
input crimeID $ ReportedF $ Fallw $ Longitude Latitude Location $ LSOAC $ LSOAN $ OutcomeT$;
run;

%let x=XYZ.ABC/XYY;
%let word=%scan(&x,3);
%let part=%scan(&x,1,Z);
%put &word;
%put &part;
```


<img width="672" height="296" alt="image" src="https://github.com/user-attachments/assets/f7fb1162-fd86-45ec-ae66-1f07bddbcb78" />


## 115. Creating a Macro variable (helps you modify data easier)

## How to print a column using Macro


```
data newhomes;
input type $ price tax;
datalines;
Duplex 150000 0.15
Duplex 160000 0.18
Duplex 180000 0.15
;
run;

%let newv=price;

proc print data=newhomes;
var &newv;
run;
```

<img width="107" height="106" alt="image" src="https://github.com/user-attachments/assets/6afa621e-4c08-42df-94f5-8720a7723243" />


### using MEANS procedure on a column

```
data newhomes;
input type $ price tax;
datalines;
Duplex 150000 0.15
Duplex 160000 0.18
Duplex 180000 0.15
;
run;

%let newv=price;

proc means data=newhomes;
var &newv;
run;
```

<img width="333" height="112" alt="image" src="https://github.com/user-attachments/assets/4f5fea6f-b701-4fb1-ac0b-3a89943a8867" />


## 116. Macro Programs Intro

```
data stats;
input sex $ age anxietylevel;
datalines;
male 21 7.0
female 19 8.3
female 21 7.4
male 22 6.5
male 22 6.2
female 18 7.5
run;

option mcompilenote=all;
%macro reg(predictors);
proc reg data = stats;
model anxietylevel = &predictors;
run;
%mend;

%reg(age)
```

<img width="849" height="1450" alt="image" src="https://github.com/user-attachments/assets/7502b7e3-3342-4456-87fb-820d2ee37beb" />


### default predictor

```
data stats;
input sex $ age anxietylevel;
datalines;
male 21 7.0
female 19 8.3
female 21 7.4
male 22 6.5
male 22 6.2
female 18 7.5
run;

option mcompilenote=all;
%macro reg(predictors=age);
proc reg data = stats;
model anxietylevel = &predictors;
run;
%mend;

%reg(predictors=age)
```

<img width="931" height="1456" alt="image" src="https://github.com/user-attachments/assets/ca9b19e1-53be-4a28-853a-adf633ca96b8" />


## 117. Creating a Macro Example 1 (greater flexibility, +useful for repetitive coding)

```
data houseprice;
input type $ price tax;
datalines;
Single 300000 0.20
Single 250000 0.25
Duplex 175000 0.15
;
run;

%macro somestats;
proc means;
var price tax;
run;
%mend;

data housepricetwo;
set houseprice;
if type='Single';
run;

%somestats;
```

<img width="411" height="106" alt="image" src="https://github.com/user-attachments/assets/1c879152-001d-4a2a-b8c9-49d373b36de6" />


### Positional Parameters
```
data houseprice;
input type $ price tax;
datalines;
Single 300000 0.20
Single 250000 0.25
Duplex 175000 0.15
;
run;

%macro newstats (prog, vars);
proc &prog;
var &vars;
run;
%mend;

%newstats (means, price tax);
```

<img width="402" height="101" alt="image" src="https://github.com/user-attachments/assets/5ebdb336-a915-471b-b623-5f235bf3a7be" />

```
data houseprice;
input type $ price tax;
datalines;
Single 300000 0.20
Single 250000 0.25
Duplex 175000 0.15
;
run;

%macro newstats (prog, vars);
proc &prog;
var &vars;
run;
%mend;

%newstats (univariate, price);
```

<img width="434" height="800" alt="image" src="https://github.com/user-attachments/assets/2bd37192-8b4a-4d41-92dd-03b6b86344e3" />


## 118. Creating a Macro Example 2 (unique sales reports for different days)
```
data sales;
infile '/home/u62043935/Dedic/sales.txt';
input unit_price;
run;

%macro daily_report;
proc means data=sales sum;
title "Daily Report";
run;
%mend;

%macro wednesday_report;
proc means data=sales sum min max std;
var unit_price;
Title "Wednesday sales report";
run;
%mend;

%macro reportcondition;
%daily_report;
%if &sysday=Wednesday %Then %Wednesday_report;
%mend;

%reportcondition;
```

<img width="324" height="345" alt="image" src="https://github.com/user-attachments/assets/02db0ea0-0c46-40d4-8497-b2d0b9334628" />




## 119. Creating a Macro Example 3 (calculating average sales for multiple years)
```
data yr2005;
input name $ sales;
datalines;
Greg 10
John 15
Lisa 50
Mark 20
run;

data yr2006;
input name $ sales;
datalines;
Greg 15
John 35
Lisa 45
Mark 34
run;

data yr2007;
input name $ sales;
datalines;
Greg 67
John 34
Lisa 45
Mark 23
run;

data yr2008;
input name $ sales;
datalines;
Greg 54
John 32
Lisa 46
Mark 57
run;

data yr2009;
input name $ sales;
datalines;
Greg 77
John 45
Lisa 78
Mark 87
run;

data yr2010;
input name $ sales;
datalines;
Greg 99
John 87
Lisa 98
Mark 104
run;

%macro average;

%do i = 2005 %to 2010;

proc means data = yr&i;
var sales;
title "Average Sales from &i";
run;
%end;
%mend;

%average;
```

<img width="410" height="1126" alt="image" src="https://github.com/user-attachments/assets/1a3a871e-0f28-40fa-abb9-c732453f2490" />


## 120. Debugging Options


### Mprint
Add `options mprint;` to get generated SAS code in the log.

```
options mprint;
%macro average;

%do i = 2005 %to 2010;

proc means data = yr&i;
var sales;
title "Average Sales from &i";
run;
%end;
%mend;

%average;
```

<img width="866" height="703" alt="image" src="https://github.com/user-attachments/assets/bf62412a-eac4-4c8c-84a0-7cf6e3e7b7ee" />

### Mlogic

```
options mlogic;
%macro average;

%do i = 2005 %to 2010;

proc means data = yr&i;
var sales;
title "Average Sales from &i";
run;
%end;
%mend;

%average;
```

<img width="1100" height="634" alt="image" src="https://github.com/user-attachments/assets/5d6d55d7-0e03-4e62-83f8-514204335c4d" />



## 121. Storing Macros (External)


