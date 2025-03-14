---
title: Date_Bucket (Transact-SQL) - Azure SQL Edge
description: Learn about using Date_Bucket in Azure SQL Edge
author: rwestMSFT
ms.author: randolphwest
ms.reviewer: randolphwest
ms.date: 09/03/2020
ms.service: sql-edge
ms.topic: reference
keywords:
  - Date_Bucket
  - SQL Edge
services: sql-edge
---

# Date_Bucket (Transact-SQL)

This function returns the datetime value corresponding to the start of each datetime bucket, from the timestamp defined by the `origin` parameter or the default origin value of `1900-01-01 00:00:00.000` if the origin parameter is not specified.

See [Date and Time Data Types and Functions &#40;Transact-SQL&#41;](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql/) for an overview of all Transact-SQL date and time data types and functions.

[Transact-SQL Syntax Conventions](/sql/t-sql/language-elements/transact-sql-syntax-conventions-transact-sql/)

## Syntax

```syntaxsql
DATE_BUCKET (datepart, number, date, origin)
```

## Arguments

*datepart*

The part of *date* that is used with the ‘number’ parameter. Ex. Year, month, minute, second etc.

> [!NOTE]
> `DATE_BUCKET` does not accept user-defined variable equivalents for the *datePart* arguments.

|*datePart*|Abbreviations|
|---|---|
|**day**|**dd**, **d**|
|**week**|**wk**, **ww**|
|**month**|**mm**, **m**|
|**quarter**|**qq**, **q**|
|**year**|**yy**, **yyyy**|
|**hour**|**hh**|
|**minute**|**mi**, **n**|
|**second**|**ss**, **s**|
|**millisecond**|**ms**|

*number*

The *integer* number that decides the width of the bucket combined with *datepart* argument. This represents the width of the datepart buckets from the origin time. **`This argument has to be a positive integer value`**.

*date*

An expression that can resolve to one of the following values:

+ **date**
+ **datetime**
+ **datetime2**
+ **datetimeoffset**
+ **smalldatetime**
+ **time**

For *date*, `DATE_BUCKET` will accept a column expression, expression, or user-defined variable if they resolve to any of the data types mentioned above.

**Origin**

An optional expression that can resolve to one of the following values:

+ **date**
+ **datetime**
+ **datetime2**
+ **datetimeoffset**
+ **smalldatetime**
+ **time**

The data type for `Origin` should match the data type of the `Date` parameter.

`DATE_BUCKET` uses a default origin date value of `1900-01-01 00:00:00.000` i.e. 12:00 AM on Monday, January 1 1900, if no Origin value is specified for the function.

## Return Type

The return value data type for this method is dynamic. The return type depends on the argument supplied for `date`. If a valid input data type is supplied for `date`, `DATE_BUCKET` returns the same data type. `DATE_BUCKET` raises an error if a string literal is specified for the `date` parameter.

## Return Values

### Understanding the output from `DATE_BUCKET`

`Date_Bucket` returns the latest date or time value, corresponding to the datePart and number parameter. For example, in the expressions below, `Date_Bucket` will return the output value of `2020-04-13 00:00:00.0000000`, as the output is calculated based on one week buckets from the default origin time of `1900-01-01 00:00:00.000`. The value `2020-04-13 00:00:00.0000000` is 6276 weeks from the origin value of `1900-01-01 00:00:00.000`.

```sql
declare @date datetime2 = '2020-04-15 21:22:11';
Select DATE_BUCKET(WEEK, 1, @date);
```

For all the expressions below, the same output value of `2020-04-13 00:00:00.0000000` will be returned. This is because `2020-04-13 00:00:00.0000000` is 6276 weeks from the origin date and 6276 is divisible by 2, 3, 4 and 6.

```sql
declare @date datetime2 = '2020-04-15 21:22:11';
Select DATE_BUCKET(WEEK, 2, @date);
Select DATE_BUCKET(WEEK, 3, @date);
Select DATE_BUCKET(WEEK, 4, @date);
Select DATE_BUCKET(WEEK, 6, @date);
```

The output for the expression below is `2020-04-06 00:00:00.0000000`, which is 6275 weeks from the default origin time `1900-01-01 00:00:00.000`.

```sql
declare @date datetime2 = '2020-04-15 21:22:11';
Select DATE_BUCKET(WEEK, 5, @date);
```

The output for the expression below is `2020-06-09 00:00:00.0000000` , which is 75 weeks from the specified origin time `2019-01-01 00:00:00`.

```sql
declare @date datetime2 = '2020-06-15 21:22:11';
declare @origin datetime2 = '2019-01-01 00:00:00';
Select DATE_BUCKET(WEEK, 5, @date, @origin);
```

## datepart Argument

**dayofyear**, **day**, and **weekday** return the same value. Each *datepart* and its abbreviations return the same value.

## number Argument

The *number* argument cannot exceed the range of positive **int** values. In the following statements, the argument for *number* exceeds the range of **int** by 1. The following statement returns the following error message: "`Msg 8115, Level 16, State 2, Line 2. Arithmetic overflow error converting expression to data type int."`

```sql
declare @date datetime2 = '2020-04-30 00:00:00';
Select DATE_BUCKET(DAY, 2147483648, @date);
```

If a negative value for number is passed to the `Date_Bucket` function, the following error will be returned.

```txt
Msg 9834, Level 16, State 1, Line 1
Invalid bucket width value passed to date_bucket function. Only positive values are allowed.
````

## date Argument

`DATE_BUCKET` return the base value corresponding to the data type of the `date` argument. In the following example, an output value with datetime2 datatype is returned.

```sql
Select DATE_BUCKET(DAY, 10, SYSUTCDATETIME());
```

## origin Argument

The data type of the `origin` and `date` arguments in must be the same. If different data types are used, an error will be generated.

## Remarks

Use `DATE_BUCKET` in the following clauses:

+ GROUP BY
+ HAVING
+ ORDER BY
+ SELECT \<list>
+ WHERE

## Examples

### A. Calculating Date_Bucket with a bucket width of 1 from the origin time

Each of these statements increments *date_bucket* with a bucket width of 1 from the origin time:

```sql
declare @date datetime2 = '2020-04-30 21:21:21'
Select 'Week',  DATE_BUCKET(WEEK, 1, @date)
Union All
Select 'Day',  DATE_BUCKET(DAY, 1, @date)
Union All
Select 'Hour',  DATE_BUCKET(HOUR, 1, @date)
Union All
Select 'Minutes',  DATE_BUCKET(MINUTE, 1, @date)
Union All
Select 'Seconds',  DATE_BUCKET(SECOND, 1, @date);
```

Here is the result set.

```txt
Week    2020-04-27 00:00:00.0000000
Day     2020-04-30 00:00:00.0000000
Hour    2020-04-30 21:00:00.0000000
Minutes 2020-04-30 21:21:00.0000000
Seconds 2020-04-30 21:21:21.0000000
```

### B. Using expressions as arguments for the number and date parameters

These examples use different types of expressions as arguments for the *number* and *date* parameters. These examples are built using the 'AdventureWorksDW2017' Database.

#### Specifying user-defined variables as number and date

This example specifies user-defined variables as arguments for *number* and *date*:

```sql
DECLARE @days int = 365,
        @datetime datetime2 = '2000-01-01 01:01:01.1110000'; /* 2000 was a leap year */;
SELECT Date_Bucket(DAY, @days, @datetime);
```

Here is the result set.

```txt
---------------------------
1999-12-08 00:00:00.0000000

(1 row affected)
```

#### Specifying a column as date

In the example below, we are calculating the sum of OrderQuantity and sum of UnitPrice grouped over weekly date buckets.

```sql
SELECT
    Date_Bucket(WEEK, 1 ,cast(Shipdate as datetime2)) AS ShippedDateBucket
    ,Sum(OrderQuantity)  As SumOrderQuantity
    ,Sum(UnitPrice) As SumUnitPrice
FROM dbo.FactInternetSales FIS
where Shipdate between '2011-01-03 00:00:00.000' and '2011-02-28 00:00:00.000'
Group by Date_Bucket(week, 1 ,cast(Shipdate as datetime2))
order by ShippedDateBucket;
```

Here is the result set.

```txt
ShippedDateBucket           SumOrderQuantity SumUnitPrice
--------------------------- ---------------- ---------------------
2011-01-03 00:00:00.0000000 21               65589.7546
2011-01-10 00:00:00.0000000 27               89938.5464
2011-01-17 00:00:00.0000000 31               104404.9064
2011-01-24 00:00:00.0000000 36               118525.6846
2011-01-31 00:00:00.0000000 39               123555.431
2011-02-07 00:00:00.0000000 35               109342.351
2011-02-14 00:00:00.0000000 32               107804.8964
2011-02-21 00:00:00.0000000 37               119456.3428
2011-02-28 00:00:00.0000000 9                28968.6982
```

#### Specifying scalar system function as date

This example specifies `SYSDATETIME` for *date*. The exact value returned depends on the
day and time of statement execution:

```sql
SELECT Date_Bucket(WEEK, 10, SYSDATETIME());
```

Here is the result set.

```txt
---------------------------
2020-03-02 00:00:00.0000000

(1 row affected)
```

#### Specifying scalar subqueries and scalar functions as number and date

This example uses scalar subqueries, `MAX(OrderDate)`, as arguments for *number* and *date*. `(SELECT top 1 CustomerKey FROM dbo.DimCustomer where GeographyKey > 100)` serves as an artificial argument for the number parameter, to show how to select a *number* argument from a value list.

```sql
SELECT DATE_BUCKET(WEEK,(SELECT top 1 CustomerKey FROM dbo.DimCustomer where GeographyKey > 100),
    (SELECT MAX(OrderDate) FROM dbo.FactInternetSales));
```

#### Specifying numeric expressions and scalar system functions as number and date

This example uses a numeric expression ((10/2)), and scalar system functions (SYSDATETIME) as arguments for number and date.

```sql
SELECT Date_Bucket(WEEK,(10/2), SYSDATETIME());
```

#### Specifying an aggregate window function as number

This example uses an aggregate window function as an argument for *number*.

```sql
Select
    DISTINCT DATE_BUCKET(DAY, 30, Cast([shipdate] as datetime2)) as DateBucket,
    First_Value([SalesOrderNumber]) OVER (Order by DATE_BUCKET(DAY, 30, Cast([shipdate] as datetime2))) as First_Value_In_Bucket,
    Last_Value([SalesOrderNumber]) OVER (Order by DATE_BUCKET(DAY, 30, Cast([shipdate] as datetime2))) as Last_Value_In_Bucket
    from [dbo].[FactInternetSales]
Where ShipDate between '2011-01-03 00:00:00.000' and '2011-02-28 00:00:00.000'
order by DateBucket;
GO
```
### C. Using a non-default origin value

This example uses a non-default origin value to generate the date buckets.

```sql
declare @date datetime2 = '2020-06-15 21:22:11';
declare @origin datetime2 = '2019-01-01 00:00:00';
Select DATE_BUCKET(HOUR, 2, @date, @origin);
```

## See also

[CAST and CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql/)
