## 12. Data set options

```
data salaryemp (keep = salary rename=salary=salaryemp);
infile '/home/u62043935/Dedic/salary.txt';
input year salary;
run;

proc print data=salaryemp;
run;
```

<img width="129" height="174" alt="image" src="https://github.com/user-attachments/assets/093edeb8-9b14-4379-a4b5-4f4c61686d80" />


### limit printing to only 4 observations

```
data salaryemp (keep = salary rename=salary=salaryemp);
infile '/home/u62043935/Dedic/salary.txt';
input year salary;
run;

proc print data=salaryemp(obs=4);
run;
```

<img width="133" height="134" alt="image" src="https://github.com/user-attachments/assets/3fa88187-72dd-4037-8a19-07c2855024fb" />



### limit printing to a range of observations
```
data salaryemp (keep = salary rename=salary=salaryemp);
infile '/home/u62043935/Dedic/salary.txt';
input year salary;
run;

proc print data=salaryemp(firstobs=3 obs=4);
run;
```

<img width="139" height="84" alt="image" src="https://github.com/user-attachments/assets/c6ca08ce-8bab-4467-b2cb-dc0ea9e3637c" />


## 13. what if your data is separated by a dot or something else? Delimiters

if your text file uses non space delimiter, you must specific it with DLM option

```
data salary;
infile '/home/u62043935/Dedic/salary_dot_delimiter.txt' DLM=".";
input year salary;
run;

proc print data=salary;
run;
```

<img width="142" height="182" alt="image" src="https://github.com/user-attachments/assets/c7e8645e-d69f-40b1-9e6e-a4ca37b6d692" />

## 14. Reading data instream in data step (typing data right into coding area)

### Free formatted

```
data beer;
input brand$ origin$ price;
cards;
budweiser USA 14.99
Heineken NED 13.99
Corona MEX 12.99
SamAdams USA 14.79
Guiness IRE 17.99
;
run;

proc print data=beer;
run;
```

<img width="236" height="158" alt="image" src="https://github.com/user-attachments/assets/d4ed3a57-6e4b-496b-9b1d-7ddbba259c64" />

### Fixed formatted
```
data beer;
input brand$ 1-9 origin$ 10-12 price 13-17;
cards;
budweiserUSA14.99
Heineken NED13.99
Corona   MEX12.99
SamAdams USA14.79
Guiness  IRE17.99
;
run;

proc print data=beer;
run;
```

<img width="236" height="158" alt="image" src="https://github.com/user-attachments/assets/d4ed3a57-6e4b-496b-9b1d-7ddbba259c64" />


##14. Reading Dates in Data

```
data dates;
input name$ bday date11.;
cards;
Eric 4 Mar 1985
Doug 15 Feb 1976
Sean 14 Jun 1975
Lisa 5 Jan 1988
;
run;

proc print data=dates; run;
```

<img width="153" height="135" alt="image" src="https://github.com/user-attachments/assets/b803b10e-5ca0-4d11-9a2d-a6037e1c2d56" />

you can see the dates are the number of dates from 1960-01-01.

we need to change the format in the PROC PRINT statement

```
data dates;
input name$ bday date11.;
cards;
Eric 4 Mar 1985
Doug 15 Feb 1976
Sean 14 Jun 1975
Lisa 5 Jan 1988
;
run;

proc print data=dates;
format bday date9.;
run;
```

<img width="189" height="133" alt="image" src="https://github.com/user-attachments/assets/e69813ab-49ea-4a2b-be75-fbc0be82546f" />


## 16. Creating variables and calculations

```
data houseprice;
infile '/home/u62043935/Dedic/houseprice.txt';
input type$ price tax;
Actualamountoftax = round( price * tax);
run;

proc print data=houseprice; run;
```

<img width="343" height="113" alt="image" src="https://github.com/user-attachments/assets/6ee0321e-6b4d-4033-a306-5f1869f407f6" />


### using datalines / cards statement

```
data houseprice;
input type$ price tax;
Actualamountoftax = round( price * tax);
datalines;
Single 300000 0.20
Single 250000 0.25
Duplex 175000 0.15
run;

proc print data=houseprice; run;
```


## 17. More on creating variables

**CARDS** statement is the legacy version of **DATALINES** statement



```
data sales;
input Name$ Sales_1-Sales_4;
Cards;
Greg 10 2 40 0
John 15 5 10 100
Lisa 50 10 15  50
Mark 20 0 5 20
;

run;

proc print data = sales; run;
```

<img width="360" height="134" alt="image" src="https://github.com/user-attachments/assets/116286d1-0676-4faa-a6ef-5db286c2527e" />

Adding new variables

```
data sales;
input Name$ Sales_1-Sales_4;
Total = Sales_1 + Sales_2 +Sales_3 +Sales_4;
Cards;
Greg 10 2 40 0
John 15 5 10 100
Lisa 50 10 15  50
Mark 20 0 5 20
;

run;

proc print data = sales; run;
```

<img width="411" height="132" alt="image" src="https://github.com/user-attachments/assets/939552e3-79ed-4797-a536-e8b86313de90" />


## 18. Automatic Variables

```
data test;
input x y;
if _error_ = 1 then
put "** Error in row " _n_ " **";
datalines;
1 1
2 3
3 n
4 4
run;
```


<img width="547" height="233" alt="image" src="https://github.com/user-attachments/assets/35b6ea61-8327-4c48-95e7-e2adaa62218e" />

<img width="870" height="430" alt="image" src="https://github.com/user-attachments/assets/9c396412-0143-40f6-803b-a9655f30c234" />



## 19. Filtering Observations (so only some data show up)

```
data houseprice;
infile '/home/u62043935/Dedic/houseprice.txt';
input type$ price tax;
run;

data filter;
set houseprice;
if price<200000;

proc print data=filter; run;
```

<img width="213" height="61" alt="image" src="https://github.com/user-attachments/assets/7f18fcf5-1c3f-4452-b2e9-dc4c0de33d26" />


## 21. If-then Conditional Logic


### Adding a conditional logic, if name is Greg, then total is 0.

```
Data sales;
input Name$ Sales_1-Sales_4;
Total = Sales_1 + Sales_2 +Sales_3 +Sales_4;
IF Name='Greg' THEN Total=0;
Cards;
Greg 10 2 40 0
John 15 5 10 100
Lisa 50 10 15  50
Mark 20 0 5 20
;
run;

proc print data=sales;run;
```
<img width="411" height="130" alt="image" src="https://github.com/user-attachments/assets/699f65b9-5672-4a26-aa4e-e8794955fe96" />



### Adding two conditions in the IF statement.

```
Data sales;
input Name$ Sales_1-Sales_4;
Total = Sales_1 + Sales_2 +Sales_3 +Sales_4;
Fired='';
IF Name='Greg' and Total =>52 THEN Fired='N';
Cards;
Greg 10 2 40 0
John 15 5 10 100
Lisa 50 10 15  50
Mark 20 0 5 20
;
run;

proc print data=sales;run;
```

<img width="459" height="130" alt="image" src="https://github.com/user-attachments/assets/3c113adb-f2d1-42b9-81f5-e34d086d353d" />


### Using **DO** statement to have two more actions in the **THEN** statement

```
Data sales;
input Name$ Sales_1-Sales_4;
Total = Sales_1 + Sales_2 +Sales_3 +Sales_4;
Fired='';
IF Name='Greg' and Total =>52 THEN
DO;
Fired='N';
Total = Total + 10;
end;

Cards;
Greg 10 2 40 0
John 15 5 10 100
Lisa 50 10 15  50
Mark 20 0 5 20
;
run;

proc print data=sales; run;
```

<img width="457" height="135" alt="image" src="https://github.com/user-attachments/assets/bafb4164-5064-4c1e-9b7d-d0583309b462" />


### Using IF THEN ELSE IF THEN

```
Data sales;
input Name$ Sales_1-Sales_4;
Total = Sales_1 + Sales_2 +Sales_3 +Sales_4;
Fired='';
Performance='';

IF total =<10 then Performance = 'l';
else if total < 50 then performance = 'a';
else performance = 'h';

DATALINES;
Greg 10 2 40 0
John 15 5 10 100
Lisa 50 10 15  50
Mark 20 0 5 20
;
run;

proc print data=sales; run;
```

<img width="558" height="130" alt="image" src="https://github.com/user-attachments/assets/d4dbaa66-fe69-49fd-ac10-c26263cabfbd" />


## 22. DO Iterative Loop and Variations (DO WHILE, DO Until)

### The Do Loop

```
data A;
do i = 1 to 5;
y = i*2;
output;
end;
run;

proc print data = A; run;
```

<img width="105" height="155" alt="image" src="https://github.com/user-attachments/assets/316a8a23-d14f-475c-bdc3-4697a37ad8cd" />

The default increment is 1, if you want to change to the different value, use the BY statement.

```
data A;
do i = 1 to 5 by 0.5;
y = i*2;
output;
end;
run;

proc print data = A; run;
```

<img width="112" height="260" alt="image" src="https://github.com/user-attachments/assets/eb9e6e44-63f0-4dfa-a39e-73dc3f4ca2ac" />

### DO WHILE

The do while loop evaluates before the loop starts, may have a minimum execution of 0 times.

```
data A;
DO i = 1 to 5 by 0.5 WHILE (y<8);
y = i*2;
output;
end;
run;

proc print data = A; run;
```

<img width="112" height="207" alt="image" src="https://github.com/user-attachments/assets/811c5340-be9d-4003-bed4-60f269c79a7b" />

Output goes up to Y = 8 because the DO WHILE condition evaluates Y<8 for i = 3.5 and y = 7 which is still True, so i = 4.0 and y = 8 is still true.


### DO UNTIL

```
data A;
do i = 1 to 5 by 0.5 until (y<8);
y = i*2;
output;
end;
run;

proc print data = A; run;
```

<img width="94" height="54" alt="image" src="https://github.com/user-attachments/assets/81f1f2fe-8042-4a31-8dff-059e3a26750d" />

The DO UNTIL loop evaluates after each iteration, so it must run at least once. In this situation, this loop will run until the y<8 condition is met, which it does after one single iteration for i = 1, y=2 (which is less than 8).

### FOR EACH LOOP

```
data A;
do v = 1,5,9,10,15;
y = v*2;
output;
end;
run;

proc print data = A; run;
```

<img width="109" height="153" alt="image" src="https://github.com/user-attachments/assets/d03264b6-f69c-4bc9-82ba-01169e24c34b" />

## 23. More on DO Group Processing (without index/counter variable)

```
data A;
input years;
datalines;
4
3
6
3
9
runs;

data B;
set A;
if years > 5 then
DO;
months=years*12;
put years= months=;
end;
else yearsleft=5-years;
run;

proc print data=B; run;
```

<img width="234" height="155" alt="image" src="https://github.com/user-attachments/assets/699c4735-a189-414a-91e8-bc061dd0fa80" />


## 24. More on the WHERE Expression/Statement

### As part of PROC SQL

```
Data sales;
input Name$ Sales_1-Sales_4;
Total = Sales_1 + Sales_2 +Sales_3 +Sales_4;
Cards;
Greg 10 2 40 0
John 15 5 10 100
Lisa 50 10 15  50
Mark 20 0 5 20
;
run;


PROC SQL;
select total from sales
where total > 50;
```

<img width="52" height="104" alt="image" src="https://github.com/user-attachments/assets/b9358ae1-ac23-4bef-b870-53e3ce8a8983" />

### As part of PROC PRINT

```
Data sales;
input Name$ Sales_1-Sales_4;
Total = Sales_1 + Sales_2 +Sales_3 +Sales_4;
Cards;
Greg 10 2 40 0
John 15 5 10 100
Lisa 50 10 15  50
Mark 20 0 5 20
;
run;


proc print data = sales (where=(total>50));
run;
```

<img width="410" height="102" alt="image" src="https://github.com/user-attachments/assets/7ffb0bff-0e8c-424c-96c7-f7993e96bb1b" />


```
Data sales;
input Name$ Sales_1-Sales_4;
Total = Sales_1 + Sales_2 +Sales_3 +Sales_4;
Cards;
Greg 10 2 40 0
John 15 5 10 100
Lisa 50 10 15  50
Mark 20 0 5 20
;
run;


proc print data = sales;
where total > 50;
run;
```

<img width="412" height="103" alt="image" src="https://github.com/user-attachments/assets/6bbd764b-8fca-46d2-ab7c-006527be1ea9" />

## 26. Sorting Observations (PROC SORT and BY statements)


```
data houseprice;
infile '/home/u62043935/Dedic/houseprice.txt';
input type$ price tax;
run;

proc sort data=houseprice out=houseprice2;
by tax;
run;

proc print data=houseprice2; run;

proc sort data=houseprice out=houseprice2;
by descending tax;
run;

proc print data=houseprice2; run;
```

Now the output is sorted by the Tax column in ascending order.

<img width="237" height="318" alt="image" src="https://github.com/user-attachments/assets/4f8a282a-017d-4885-becd-306d9843e8d9" />

## 27. Merging Two Data Sets

```
data houseprice;
infile '/home/u62043935/Dedic/houseprice.txt';
input type$ price tax;
run;

proc print data = houseprice; run;

data newhomes;
infile '/home/u62043935/Dedic/newhomes.txt';
input type$ price tax;
run;

proc print data = newhomes; run;

proc sort data = houseprice out=houseprice2;
by price;
run;

proc sort data = newhomes out=newhomes2;
by price;
run;

data newcollections;
merge houseprice2 newhomes2;
by price;
run;

proc print data = newcollections; run;
```

<img width="227" height="544" alt="image" src="https://github.com/user-attachments/assets/dfd90942-408a-4a96-b04b-669ddf569330" />

see how the data is in ascending order because the PROC SORT was in ascending order. 

### In Descending order

```
data houseprice;
infile '/home/u62043935/Dedic/houseprice.txt';
input type$ price tax;
run;

proc print data = houseprice; run;

data newhomes;
infile '/home/u62043935/Dedic/newhomes.txt';
input type$ price tax;
run;

proc print data = newhomes; run;

proc sort data = houseprice out=houseprice2;
by descending price;
run;

proc sort data = newhomes out=newhomes2;
by descending price;
run;

data newcollections;
merge houseprice2 newhomes2;
by descending price;
run;

proc print data = newcollections; run;
```

<img width="211" height="515" alt="image" src="https://github.com/user-attachments/assets/9dd132d3-6f2d-4d45-996f-afe1b1af5fe1" />


**note: the sort order in the PROC SORT must be the same as the DATA STEP, otherwise you will not get the correct sort order.**

## 28. Using SET statement to Merge

```
Data sales1;
input Name$ Sales_1-Sales_4;
Total = Sales_1 + Sales_2 +Sales_3 +Sales_4;
Cards;
Greg 10 2 40 0
John 15 5 10 100
Lisa 50 10 15  50
Mark 20 0 5 20
run;

proc print data=sales1; run;

Data sales2;
input Names$ Sales_1-Sales_4;
Total = Sales_1 + Sales_2 +Sales_3 +Sales_4;
Cards;
Eric 17 5 40 0
Lori 15 12 10 100
Bill 50 14 15  50
Mark 22 3 5 16
run;

proc print data=sales2; run;

data mergesales;
set sales1 sales2(rename=(Names=Name));
run;

proc print data=mergesales; run;
```

<img width="409" height="619" alt="image" src="https://github.com/user-attachments/assets/a290586a-064b-416b-a72d-84e17c81c7a4" />


## 29. Data Reduction and Cleaning your Data

### Using Keep

```
data newhomes;
input type$ price tax;
datalines;
duplex 150000 0.15
duplex 160000 0.18
duplex 180000 0.15
run;

data reducednewhomes;
set newhomes;
keep type price;
run;

proc print data=reducednewhomes; run;
```

<img width="161" height="102" alt="image" src="https://github.com/user-attachments/assets/26464526-a209-4733-8018-7c07b1e74e20" />

### Using Drop

```
data newhomes;
input type$ price tax;
datalines;
duplex 150000 0.15
duplex 160000 0.18
duplex 180000 0.15
run;

data reducednewhomes;
set newhomes;
drop type price;
run;

proc print data=reducednewhomes; run;
```

<img width="92" height="105" alt="image" src="https://github.com/user-attachments/assets/0eee403b-8c5a-446f-a03a-2c42a5727896" />

### Rename variables

```
data newhomes;
input x$ y z;
datalines;
duplex 150000 0.15
duplex 160000 0.18
duplex 180000 0.15
run;

data cleannewhomes; set newhomes;
rename x=type
		y=price
		z=tax;
run;

proc print data = cleannewhomes; run;
```

<img width="208" height="108" alt="image" src="https://github.com/user-attachments/assets/1ebf9fe4-d90c-45be-8f56-2bd84316935c" />



### using LABEL statement

```
data newhomes;
input x$ y z;
datalines;
duplex 150000 0.15
duplex 160000 0.18
duplex 180000 0.15
run;

data cleannewhomes; set newhomes;
rename x=type
		y=price
		z=tax;
run;

	
	data cleannewhomes; set cleannewhomes;
	label type='Type of Home'
		  price='Price of Home'
		  tax='Tax Percentage of Home';
		  run;
		  
	proc freq data=cleannewhomes;
	table type price tax;
	run;
```

<img width="396" height="474" alt="image" src="https://github.com/user-attachments/assets/5ae0f4f8-7836-4870-a1ac-898b1f8f3c0d" />

## 30. LENGTH statement

```
data mydata;
length age 3 sex$ 6 bmi 8 children 3 smoker$ 3 region$ 15 charges 8;
infile "/home/u62043935/Dedic/insurance.csv" DSD MISSOVER Firstobs=2;
input age sex$ bmi children smoker$ region$ charges;
run;

proc print data=mydata; run;
```

<img width="493" height="740" alt="image" src="https://github.com/user-attachments/assets/7c6ee1fd-186d-45ea-a7e0-bf363aa204c1" />


## 31. Creating a Counting (Enumeration) Variable

```
data studentscores;
input gender score;
datalines;
1 48
1 45
2 50
2 42
1 41
2 51
1 52
1 43
2 52
; 

run;

proc sort data=studentscores;
by gender;
runs;

proc print data=studentscores; run;

data studentscore1; set studentscores;
count + 1;
by gender;
if first.gender then count=1;
run;

proc print data=studentscore1; run;
```

<img width="217" height="572" alt="image" src="https://github.com/user-attachments/assets/9f2783e3-79c3-426a-9c2e-07387d1d6b6b" />













































