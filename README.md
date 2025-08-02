# Power BI Reference

> [Data Analysis Expressions (DAX)](https://learn.microsoft.com/en-us/dax/)  
> [DAX guide](https://dax.guide/)

[**Functions**](#functions)  

0. [Misc](#misc)
1. [Aggregate](#aggregate)
2. Date and Time
3. [Filter](#filter)
4. Financial
5. INFO
6. [Information](#information)
7. Logical
8. Math and trig
9. [Other](#other)
10. Parent and child
11. Relationship
12. Statistical
13. [Table Manipulation](#table-manipulation)
14. [Text](#text)
15. Time intelligence

[**Statements**](#statements)

1. DEFINE
2. EVALUATE
3. MEASURE
4. ORDER BY
5. START AT
6. [VAR](#var)

[**Clear Metadata**](#clear-metadata)

<!-- ----------------------------------------------------------------------- -->

## FUNCTIONS

<!-- ----------------------------------------------------------------------- -->

### MISC

```sql
'table_name'[column_name] = "value"
```

* filter on specific value

<!-- ----------------------------------------------------------------------- -->

### AGGREGATE

```sql
AVERAGE(column)
```

```sql
AVERAGEX(table, expression)
```

```sql
DIVIDE(numerator, denominator, alternate_result) -- alternate_result is optional
```

```sql
SUM(column)
```

* adds all values in a column

```sql
SUMX(table, expression)
```

* evaluated for each row in a table

```sql
COUNTROWS(table)
```

* often used to count the number of rows that result from filtering a table

```sql
MAXX(table, expression, variant) -- variant is optional
```

<!-- ----------------------------------------------------------------------- -->

### FILTER

```sql
CALCULATE(expression, filter1, filter2, ...) -- filters are optional
```

* `filter` - boolean expression or table expression

```sql
REMOVEFILTERS(table_or_column, column...) -- parameters are optional
```

* clear filters

<!-- ----------------------------------------------------------------------- -->

### INFORMATION

```sql
ISINSCOPE(column)
```

* can be used to
  * adjust how totals are calculated (fixes unwanted logic in totals)

```sql
HASONEVALUE(column)

-- example: blank value for table totals
.Actual Avg Total Dept Total Pay (Bin) = 
IF(
  HASONEVALUE('payroll'[pay_year]) && HASONEVALUE('payroll'[department_title]),
  FLOOR([.Avg Total Pay (Bin)] / 5000, 1) * 5000, -- show each individual row
  BLANK() -- hide at total level
)
```

* returns `true` when the context has been filtered down to one distinct value only

<!-- ----------------------------------------------------------------------- -->

### OTHER

```sql
BLANK()

-- example: blank value for table totals
.Actual Avg Total Dept Total Pay (Bin) = 
IF(
  HASONEVALUE('payroll'[pay_year]) && HASONEVALUE('payroll'[department_title]),
  FLOOR([.Avg Total Pay (Bin)] / 5000, 1) * 5000,
  BLANK()
)
```

<!-- ----------------------------------------------------------------------- -->

### LOGICAL

```sql
IF(logical_test, value_if_true, value_if_false) -- value_if_false is optional
```

```sql
SWITCH(expression, value, result)

-- extra [value, result] pairs and [else] are optional
SWITCH(expression, value, result[, value, result] ... [, else])

SWITCH(
  expression, 
  
  value, 
  result
  
  [, value, 
  result]
  
  ...
  
  [, else]
)
```

* switch case
* can be used to avoid nested IF statements

```sql
TRUE()
FALSE()
```

#### OPERATOR

```SQL
NOT(value_or_expression) -- boolean
```

<!-- ----------------------------------------------------------------------- -->

### TABLE MANIPULATION

```sql
VALUES(table_or_column)
```

* used as an intermediate function, nested in a formula, to get a list of distinct values that can be
  * counted
  * used to filter or sum other values

<!-- * `column` - single column table of unique values
* `table` - table with same columns -->

```sql
SUMMARIZE(table, groupby_column, "alias", expression) -- groupby_column is optional
SUMMARIZE(table, groupby_column[, groupby_column] ... [, "alias", expression] ...)
```

```sql
ADDCOLUMNS(table, "alias", expression)
ADDCOLUMNS(table, "alias1", expression1, "alias2", expression2, ...)
```

```sql
TOPN(#_of_rows, table, orderby_expression, order) -- order is optional
TOPN(#_of_rows, table, orderby_expression, order[, orderby_expression, order] ...)
```

<!-- ----------------------------------------------------------------------- -->

### TEXT

```sql
FORMAT(value_or_expression, format_string, locale_name) -- locale_name is optional

-- example: add commas and truncate decimals
FORMAT(value_or_expression, "#,###0") --> turns 130000 to 130,000
```

* `FORMAT` changes data type to **text**
* `value_or_expression` - if blank, returns an empty string
* `format_string` - if blank, formats with a "general number" or "general date"

<!-- ----------------------------------------------------------------------- -->

## STATEMENTS

<!-- ----------------------------------------------------------------------- -->

## VAR

```sql
VAR name = expression

RETURN
...
```

<!-- ----------------------------------------------------------------------- -->

## CLEAR METADATA

<!-- ----------------------------------------------------------------------- -->

Step 1:

* Home > Transform data > Data source settings > Edit Permissions > Credentials > Delete > OK

or

* Home > Transform data > Data source settings > Clear Permissions

Step 2:

* Home > Transform data > Transform data > `Source{[Schema="...`
