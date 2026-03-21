

## 06 Import .txt

```
data salary;
infile '/home/u62043935/Dedic/salary.txt';
input year salary;
run;
```

## 07 Import csv

```
data weighgain;
infile '/home/u62043935/Dedic/weightgain.csv' DSD missover firstobs=2;
input id source$ type$ weightg;
run;
```

## 08 Import Excel
```
proc import out=salesdata datafile = "/home/u62043935/Dedic/Sample-Sales-Data.xlsx" dbms=xlsx replace;
sheet = "Sheet1";
*getnames=YES will use the first row in excel file as the column header;
getnames=YES;
*mixed=YES if SAS detect multiple formats, then the values will be read in as string format;
mixed=YES;
run;
```
