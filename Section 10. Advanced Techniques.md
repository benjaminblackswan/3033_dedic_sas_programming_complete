## 53. Flexible Programming 1 - Combining multiple raw data files vertically

### Using filename variable
```
filename sales '/home/u62043935/Dedic/mon*.txt';

data rollingquarter;
infile sales dlm=',';
input Customer_ID$ order_id order_type order_date : date9. Delivery_date : date9.;
run;

proc print data=rollingquarter; run;
```

<img width="421" height="278" alt="image" src="https://github.com/user-attachments/assets/56b04214-e6e6-429e-8ffd-22fb4c411d85" />


### Using DO loop

```
data rollingquarter2;
drop i;
length customer_id $ 40 order_id 4 order_type 4 order_date 4
delivery_date 4;
	do i=5 to 7;
	NextFile=cats('/home/u62043935/Dedic/mon', i, '.txt');
	infile order filevar=NextFile dlm=',' end=LastObs;
		do while(not LastObs);
		input customer_id$ order_id order_type
		order_date : date9. Delivery_date : date9.;
		output;
		end;
	end;
stop;
run;

proc print data=rollingquarter2; run;
```

<img width="414" height="275" alt="image" src="https://github.com/user-attachments/assets/912e1cfb-9452-42f1-a90c-4393cee02bf0" />


### Rolling month range with MONTH Function

```
data rollingquarter3;
drop i;
length customer_id $ 40 order_id 4 order_type 4 order_date 4
delivery_date 4;
MonNum = month(today());
MidMon = MonNum -1;
MonLast = MidMon - 1;
do i = MonNum, MidMon, MonLast;
	NextFile=cats('/home/u62043935/Dedic/mon', i, '.txt');
	infile ORD filevar=NextFile dlm=',' end=LastObs;
	do while (not LastOBS);
		input customer_id$ order_id order_type order_date : date9. Delivery_date : date9.;
		output;
	end;
end;
stop;
run;

proc print data=rollingquarter3; run;
```













