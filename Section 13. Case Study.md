## 66. Case Study (Health Care Case Study) PART 1

```
libname dedic '/home/u62043935/Dedic';

data dedic.identifyconditions;
infile '/home/u62043935/Dedic/casestudy.csv' DSD missover firstobs=2;
informat DOB ddmmyy10.;
input ID$ SEX$ DOB Pdx Dx_2 Dx_3 Dx_4;
run;

proc sort data = dedic.identifyconditions out=dedic.identifyconditions;
by ID;
run;

proc print data=dedic.identifyconditions;
format DOB date9.;
run;
```

<img width="434" height="244" alt="image" src="https://github.com/user-attachments/assets/8efdea85-8e0d-4ec9-b44a-9b67ff90f1fc" />



## 67. Case Study (Health Care Case Study) PART 2

libname dedic '/home/u62043935/Dedic';

data dedic.identifyconditions;
infile '/home/u62043935/Dedic/casestudy.csv' DSD missover firstobs=2;
informat DOB ddmmyy10.;
input ID$ SEX$ DOB Pdx Dx_2 Dx_3 Dx_4;
run;

proc sort data = dedic.identifyconditions out=dedic.identifyconditions;
by ID;
run;

proc print data=dedic.identifyconditions;
format DOB date9.;
run;

data perm.MemberConditions;
set perm.identityconditionstwo;
by ID;
length Diabetes Depression COPD Asthema
CKD HIV Schizophrenia Hypertension Migraine $14 Conditions $50;
