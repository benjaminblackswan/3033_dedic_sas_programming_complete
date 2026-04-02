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
