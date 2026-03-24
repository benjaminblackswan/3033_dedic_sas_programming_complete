## 39. Understanding SAS Functions

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
