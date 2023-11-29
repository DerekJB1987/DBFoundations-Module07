# Name: Derek Benak
## Date: November 20, 2023
## Course: Foundations of Databases & SQL Programming
### Assignment 7
https://github.com/DerekJB1987/DBFoundations-Module07

# Functions
## Introduction

This week I started diving deeper into the power of SQL functions and how they are used to retrieve information from a database.
## When to use a SQL UDF (User Defined Functions)

A programmer / data analyst can create custom defined functions which are commonly referred to as User Defined Functions or UDFs. These can be used to return a single (Scalar) value as an expression and/or use UDFs to check constraints. 

CREATE FUNCTION fProductInventoriesWithPreviousMonthCountsWithKPIs(@KPIValue int)
RETURNS Table
AS
    RETURN SELECT
    [ProductName]
    ,[InventoryDate]
    ,[InventoryCount]
    ,[PreviousMonthCount]
    ,[CountVsPreviousCountKPI]
    FROM vProductInventoriesWithPreviousMonthCountsWithKPIs
    WHERE [CountVsPreviousCountKPI] = @KPIValue;
go

SELECT * FROM fProductInventoriesWithPreviousMonthCountsWithKPIs(0) ORDER BY 1,2,3;


*Figure 1: Example of SQL code where a user created a custom UDF that uses a KPI integer value as a parameter to generate the list of every product (names) that qualifies with that inputted parameter of 0.*


![SQL code](https://github.com/DerekJB1987/DBFoundations-Module07/blob/9cfa3a2a530c34456ea2aa029aab5655ae6ed3ea/Image%201.jpg)
 

*Figure 2: Retrieved results from the UDF shown in Figure 1 above.*

## What are differences and similarities between Scalar, Inline, and Multi-Statement Functions

There are multiple looks and types of functions that can be used in SQL statements. Scalar, Inline, and Multi-statement functions are all UDFs.

A **Scalar function** is any function that returns a single value as an expression.

Create Function dbo.MultiplyValues(@Value1 Float, @Value2 Float)
 Returns Float 
 As
  Begin
   Return(Select @Value1 * @Value2);
  End 
go
-- Calling the function
Select Tempdb.dbo.MultiplyValues(4, 5);
go

*Figure 3: Example of SQL code where a user created a scalar function that will return a single value when a user inputs 2 integers that are multiplied when the function is executed*


An **Inline function** is a UDF that returns a table as its result. The UDF in Figure 1 and the retrieved results in the table shown in the Figure 2 image are an example of an inline function.


A **Multi-Statement** function is a UDF that returns a table of rows and columns.


## Summary

This writeup highlights the similarities, differences between scalar, inline and multi-statement functions and examines when you would want to create and use a SQL UDF.
