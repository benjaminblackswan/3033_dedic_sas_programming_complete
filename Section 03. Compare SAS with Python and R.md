

```
proc python;
submit;
import pandas as pd
import numpy as np

d = {'First_Name'; ['Jordan'],
     'Last_Name'; ['Latner']}
	
df = pd.DataFrame(d)
print(df)
endsubmit;
run;
```


```
data personnel;
input First_Name$ Last_Name$ Age;
datalines;
Jordan Latner 27
Larry Benner 33
Sarah Luc 45
run;
```
