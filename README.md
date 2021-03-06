## SAS_STUDIO_CRASH_COURSE

### 1. Create Dataset

```.sas
DATA mydata;
INPUT name $ 10. mobile gender$ 1-2;
DATALINES;
Anant 9312585135 M
Priya 9999 F
; 
RUN;
```

### 2. Print

```.sas
PROC PRINT DATA=mydata;
title 'ABC';
RUN;
```

### 3. Some Proc statements

```.sas
PROC CONTENTS DATA=mydata; *metadata;
PROC MEANS DATA=mydata; *mean,max,min,SD;
PROC UNIVARIATE DATA=mydata; *all details, use BY/ID;
PROC FREQ DATA=mydata;

proc sort data=company;
   by Name;
run;

```

### 4. Import

```.sas
data imp_data;
infile '/folders/myfolders/b.txt' dlm=',';
input A$ B;
run;

*PROC IMPORT datafile ='/folders/myfolders/a.xlsx' OUT=imp_data dbms="xlsx";
*run;
```

### 5. Loops

```.sas
* do;
data A;
do i = 1 to 5 by 0.5;
   y = i**2; /* values are 1, 2.25, 4, ..., 16, 20.25, 25 */
   output;
end;
run;

*do while;
data A;
n=0;
do while(n<5);
   put n=;
   n+1;
   output;
end;

*do until;
data A;
n=0;
do until(n>=5);
   put n=;
   n+1;
   output;
end;
```

### 6. Conditions

```.sas
IF expression THEN statement;
*<ELSE statement;>
```

### 7. Set/ Concatenate 
- same attributes

```.sas
data x;
   set data1 data2;
run;
```

### 8. Merge
- like join 

```.sas
data employee_info;
   merge company finance;
   by name;
run;
```

### 9. Export

```.sas
proc export data=mydata
  dbms=xlsx
  outfile='/folder/mydolder/a.xlsx' replace;
  sheet="Sheet1";
run;

ods
```

### 10. Linear Regression (*)

```.sas
DATA x;
input xx yy;
datalines;
1 2
2 3
3 5
4 8
0 9
;
run;

PROC SGSCATTER DATA=x;
PLOT xx*yy;

PROC reg data=x;
model yy=xx/clb;

DATA x2;
input xx yy;
datalines;
8.5 .
;

DATA x3;
set x x2;

PROC REG data=x3;
model yy=xx/cli; 

PROC PRINT data=x3;

```
