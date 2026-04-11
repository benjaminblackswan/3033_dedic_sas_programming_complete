## 131. Data audit

```
libname dedic '/home/u62043935/Dedic';

data dedic.train;
infile "/home/u62043935/Dedic/train.csv" dsd missover firstobs=2;
input Loan_ID $ Gender $ Married $ Dependents Education $
Self_Employed $ ApplicantIncome CoapplicantIncome LoanAmount
Loan_Amount_Term Credit_History Property_Area $ Loan_Status $
;
run;

data dedic.test;
infile "/home/u62043935/Dedic/train.csv" dsd missover firstobs=2;
input Loan_ID $ Gender $ Married $ Dependents Education $
Self_Employed $ ApplicantIncome CoapplicantIncome LoanAmount
Loan_Amount_Term Credit_History Property_Area $
;
run;

proc contents data=dedic.train; run;
```

## 132. Univariate Analysis

