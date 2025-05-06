# Power BI Reference

[Data Analysis Expressions (DAX)](https://learn.microsoft.com/en-us/dax/)

0. [Misc](#misc)
1. [Aggregate](#aggregate)
2. Date and Time
3. [Filter](#filter)
4. Financial
5. INFO
6. Information
7. Logical
8. Math and trig
9. Other
10. Parent and child
11. Relationship
12. Statistical
13. [Table Manipulation](#table-manipulation)

<!-- ----------------------------------------------------------------------- -->

## MISC

```sql
'table_name'[column_name] = "value"
```

* filter on specific value

<!-- ----------------------------------------------------------------------- -->

## AGGREGATE

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

<!-- *  -->

```sql
COUNTROWS(table)
```

* often used to count the number of rows that result from filtering a table

<!-- ----------------------------------------------------------------------- -->

## FILTER

```sql
CALCULATE(expression, filter1, filter2, ...) -- filters are optional
```

* `filter` - boolean expression or table expression

```sql
REMOVEFILTERS(table_or_column, column...) -- parameters are optional
```

* clear filters

<!-- ----------------------------------------------------------------------- -->

## TABLE MANIPULATION

```sql
VALUES(table_or_column)
```

* used as an intermediate function, nested in a formula, to get a list of distinct values that can be
  * counted
  * used to filter or sum other values

<!-- * `column` - single column table of unique values
* `table` - table with same columns -->
