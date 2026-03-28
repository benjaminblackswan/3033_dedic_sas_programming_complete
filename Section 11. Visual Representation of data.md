## 55. Scatter Plot

```
data houseprice;
infile '/home/u62043935/Dedic/houseprice.txt';
input type$ price tax;
run;

proc gplot data=houseprice;
title 'Comparing the price and tax by type of home';
format price dollar9.;
symbol1 value = dot cv=blue;
symbol2 value = square cv=red;
plot price*tax=type;
run;
quit;

```
<img width="844" height="649" alt="image" src="https://github.com/user-attachments/assets/496dcb20-2bf7-43b2-8750-5fea3dca3ca7" />

## 56. Bar Graph

```
data houseprice;
infile '/home/u62043935/Dedic/houseprice.txt';
input type$ price tax;
run;

proc gchart data=houseprice;
title 'Comparing the price and tax by type of home';
format price dollar9.;
vbar price tax/ group=type;
pattern color=yellow;
run;
quit;
```

<img width="863" height="1259" alt="image" src="https://github.com/user-attachments/assets/d4cf4e2c-0bdd-4243-88d2-dee900cee394" />
