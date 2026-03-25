## 39. Understanding SAS Functions

### List of functions

```
data summing;
sumthis = sum(7,9,13);
varargum = sum(sumthis);
numargum = sum(6, 8);
expargum = sum(sumthis * 7/2);
varargumlist = sum(of Var1-Var5);
datetoday = today();
run;

proc print data=summing; run;
```

<img width="627" height="48" alt="image" src="https://github.com/user-attachments/assets/3bbcf3ae-5561-4870-ba5d-126ccb72d98f" />

### Using format in PROC PRINT to format date

```
data summing;
sumthis = sum(7,9,13);
varargum = sum(sumthis);
numargum = sum(6, 8);
expargum = sum(sumthis * 7/2);
varargumlist = sum(of Var1-Var5);
datetoday = today();
run;

proc print data=summing;
format datetoday date11.;
run;
```

<img width="659" height="54" alt="image" src="https://github.com/user-attachments/assets/c8cfc19c-e7f9-49bc-9fa3-79c645a08588" />


### Using the Titantic dataset to split Title from Names

```
data splitname;
length name $16;
input name & $;
prefix = scan(name, 1);
datelines;
Mr Ermin Dedic
Dr Johanna Ratner
run;

proc print data=splitname; run;
```

<img width="189" height="70" alt="image" src="https://github.com/user-attachments/assets/130b5e6b-7260-42fb-86dd-ce92303c9317" />


## 40. RAND Function (producing a sample with distribution of your choice)

Just the 1 to ### to control how close the distribution is close to a normal distribution. 

```
 data rand;
 call streaminit(12345);
 do i = 1 to 1000;
 	x = rand("Normal");
 	output;
 end;
 run;
 
 proc sgplot data=rand;
 title "Random Values from N(0,1)";
 histogram x;
 run;
 
 proc freq data= rand;
 run;
```
<img width="704" height="524" alt="image" src="https://github.com/user-attachments/assets/c039a367-7424-4ced-9387-2833bb252906" />

<img width="324" height="703" alt="image" src="https://github.com/user-attachments/assets/445e7130-4306-46cb-9204-6624cb7f7996" />


## 41. LENGTH, LENGTHN, LENGTHC functions (are you working with a large data set?)

### LENGTH function

```
data lengthfunctions;
one = 'ABC       ';
two = ' ';
three = 'ABC   XYZ';
length_one = lengthn(one);
length_two = length(two);
length_three = length(three);
run;
 
proc print data = lengthfunctions; run;
```

<img width="395" height="49" alt="image" src="https://github.com/user-attachments/assets/2f33a89e-1692-4d25-a4bb-9e6fb4ce95c0" />






### LENGTHN function

```
data lengthfunctions;
one = 'ABC       ';
two = ' ';
three = 'ABC   XYZ';
length_one = lengthn(one);
length_two = lengthn(two);
length_three = lengthn(three);
run;
 
proc print data = lengthfunctions; run;
```

<img width="395" height="50" alt="image" src="https://github.com/user-attachments/assets/cc0888c6-1526-44b2-bd6e-ec9aad867995" />


### LENGTHC function

```
data lengthfunctions;
one = 'ABC       ';
two = ' ';
three = 'ABC   XYZ';
length_one = lengthc(one);
length_two = lengthc(two);
length_three = lengthc(three);
run;
 
proc print data = lengthfunctions; run;
```

<img width="392" height="48" alt="image" src="https://github.com/user-attachments/assets/8cf541b5-44c6-4617-a915-71fcc39df6da" />


## 42. TRIM function (want to get rid of trailing blanks?)

```
data trimlecture;
	input firstname$ lastname$ age tscore;
	length name$20;
	name=lastname||', '||firstname;
datalines;
Alex Benson 27 45
;
run;

proc print data=trimlecture; run;
```

<img width="332" height="51" alt="image" src="https://github.com/user-attachments/assets/a4939935-0378-44d7-a086-cc8996ad4640" />

Notice there is a space after Benson and before the ",".

Therefore you must get rid of the blank with **TRIM** function.

```
data trimlecture;
	input firstname$ lastname$ age tscore;
	length name$20;
	name=trim(lastname)||', '||firstname;
datalines;
Alex Benson 27 45
;
run;

proc print data=trimlecture; run;
```

<img width="325" height="50" alt="image" src="https://github.com/user-attachments/assets/767a0069-9510-4be8-ad9a-4f430106e5c2" />


## 43. COMPRESS Function (remove characters from string, and all types of blanks)

```
data compressed;
input phone_no $1-15;
phone_no1 = compress(phone_no); 
phone_no2 = compress(phone_no, '(-)'); 
phone_no3 = compress(phone_no, '(-)', 's'); 

datalines;
(314)456-4678
(314) 456-46 78
;
run;

proc print data=compressed; run; 
```



Note: the default behaviour of **COMPRESS**  is to get rid of spaces, but if you passed the second argument, in the case of phone_no2, then spaces will not be automatically compressed, you must explicitly compressed it with a 's' argument as in phone_no3.


<img width="374" height="72" alt="image" src="https://github.com/user-attachments/assets/27c5b657-afa8-4ae0-81dd-8fd096b8e3e5" />


## 44. Input and Put Functions

### character variable to number

```
data inputfunc;
input sale $9.;
numsale = input(sale, comma9.);
datalines;
6,515,353
;
runs;

proc print data=inputfunc; run;

proc contents data=inputfunc; run;
```
<img width="1017" height="871" alt="image" src="https://github.com/user-attachments/assets/3651b95f-90bb-4585-8a1d-34abce779a2e" />

### number to character variable

```
data inputfunc;
input sale;
charsale = put(sale, 7.);
datalines;
6515353
;
runs;

proc print data=inputfunc; run;

proc contents data=inputfunc; run;
```

<img width="999" height="867" alt="image" src="https://github.com/user-attachments/assets/9aeefcc9-fd24-4f89-8b49-c385f66ee39e" />

## 45. CATX function

```
data bringittogether;
separator = ',';
first = '    Larry';
last = 'Larryson    ';
result = catx(separator, first, last);
drop separator;
run;

proc print data =bringittogether; run;
```


<img width="245" height="53" alt="image" src="https://github.com/user-attachments/assets/99108d31-6cc7-4fdf-8d40-d8c9224d3a51" />


## 46. SCAN function

```
data bringittogether;
separator = ',';
first = '    Larry';
last = 'Larryson    ';
result = catx(separator, first, last);
scann = scan(result, 1);
drop separator;
run;

proc print data =bringittogether; run;
```

<img width="314" height="62" alt="image" src="https://github.com/user-attachments/assets/c6b395f6-cf3f-4ea8-8981-e6c85d98777f" />



## 48. Coalesce function

```
data coalesce;
input home cell;
numavailable=coalesce(home, cell);
datalines;
6578975
6448565
run;

proc print data=coalesce; run;
```

<img width="281" height="61" alt="image" src="https://github.com/user-attachments/assets/1fd79be4-b9e6-4865-8582-f22693df3866" />



## 49. Verify function

```
data errors valid;
input id$ stage : $5.;
if verify(stage, 'abcd') then output errors;
else output valid;
datalines;
001 aabcd
002 aabqc
;
run;

proc print data=errors; title 'Errors dataset'; run;

proc print data=valid; title 'Valid dataset'; run;
```

<img width="140" height="230" alt="image" src="https://github.com/user-attachments/assets/9336b1f9-6522-441c-8026-e186c545eb3f" />


## 50. Substr function

### using SUBSTR to extract a portion of a string.

```
data news;
date='06MAY98';
month=substr(date, 3, 5);

proc print data=news; run;
```

<img width="165" height="58" alt="image" src="https://github.com/user-attachments/assets/242c8cb0-b152-4677-9a2f-9b82511b1e1c" />

### Using SUBSTR to replace a portion of a string

```
data news;
date='06MAY98';

month = substr(date, 6, 2) = '16'; 

proc print data=news; run;
```

<img width="121" height="59" alt="image" src="https://github.com/user-attachments/assets/d28fc09b-38a3-442a-b425-e4fa83284984" />












