# **SQL Query Commands**
 
### **SELECT** 
Selects columns to return
>**Query Example:** SELECT **\*** FROM table
>
> Grabs everything
 
### **DISTINCT** 
Selects only unique rows in the specified column
>**Query Example:** SELECT DISTINCT(column) FROM table
>
> Grabs unique columns only
 
### **COUNT** 
Returns the number of input rows that match a specific condition or query
> **Query Example:** SELECT COUNT(column) FROM(table
>
> Returns the number of rows in name column from table
- Parenthesis is required to specify column
- If checking how many rows are in a table COUNT(\*) is acceptable
> [!NOTE]
> SELECT COUNT( DISTINCT column) FROM table
>
> Returns the number of unique names in the column
 
### **WHERE** 
Is used to filter rows returned from the SELECT statement 
> **Query Example:** SELECT column FROM table WHERE something = ‘something’ (case sensitive)
- Appears immediately after the FROM clause
- You can use comparison operators (=, &gt;, &lt;, &lt;= & &gt;=, &lt;&gt; or !=)
- You can use logical operators (AND, OR, NOT)

### **ORDER BY** 
Is used to sort rows based on column value  
> **Query Example:** SELECT column1, column2 FROM table ORDER BY column1, column2 ASC/DESC

> [!NOTE]
> This will order by column1  first, then column2
- Put towards the end of the query statement. Filter and select first, then order.
- Can do either ascending or descending
- Can sort multiple columns, but order by what column is listed first

### **LIMIT** 
Allows us to limit the number of rows returned for a query
> **Query Example:** SELECT * FROM table LIMIT #
-	Useful in large tables, where we want to just get the top x of a query OR an idea of the top of the query results
-	Goes at the very bottom of the command request
> [!NOTE]
>  SELECT * FROM table LIMIT 1
>
> Is commonly used to see the layout of a table

### **BETWEEN** and **NOT BETWEEN**
Is used to specify values in the middle of a low and high value
>**Query Example:** SELECT * FROM table WHERE column BETWEEN lowValue AND highValue

> [!NOTE]
>	BETWEEN low and high is the same as WHERE (value >= low AND value <= high)
> 
>	Just improved syntax
> 
>	Also, can use NOT BETWEEN low AND high  

---
> [!Important]
> Using **BETWEEN** for dates is not optimal
>
> Either explicitly cast    
> WHERE cast(created_at as date) BETWEEN '2013-05-01' AND '2013-05-01'
>
> **Or**
>
> Explicitly binary compare  
> WHERE created_at >= '2013-05-01' AND created_at < '2013-05-02'
---

### **IN** 
Is used to filter rows that determine if the specified values exist within the columns.  
This is used when you want to specify multiple values in a  column typically.
> **Query Example:** SELECT column1 FROM table WHERE column1 in (value1, value2, ...)
-	This only shows the rows where value1 and value2  appear in column1
-	AKA WHERE column1 = ‘value1’ OR column1 = ‘value2’ OR ...

### **LIKE** 
Allows you to match column values with general patterns.   
- IE ends with @gmail.com or all  names that end in ‘A’
- Wildcard char is % (percent sign)
> **Query Example:** WHERE name LIKE ‘A%’
>
> Returns all names that begin with an uppercase A
- Replace a single char by _ (underscore)
> **Query Example:** WHERE name LIKE ‘Mission  Impossible _’
>
> Returns all mission impossible movies

### **ILIKE** 
Is case Insensitive
> **Query Example:** WHERE name ILIKE ‘A%’
>
> Returns all names that begin with A regardless of case.

## Aggregate Functions
#### Aggregate Functions take multiple inputs and returns a single output (IE SUM)

### AVG()
Returns a float   
> [!TIP]
> complement this with **ROUND**(AVG(column1), # of decimals) to prevent long decimal outputs

### COUNT()
- COUNT(*) is acceptable

### MAX()
### MIN()
### SUM()

### GROUP BY 
Allows us to aggregate some columns per some category
> **Query Example:** SELECT column1, AGG(column2) FROM table GROUP BY column1
> 
> Column1 must be a category column & column2 must be a data column

> **Query Example:** SELECT company, division, SUM(sales) from table GROUP BY company, division ORDER BY division, company
>
>  You can group by multiple columns similar to how you can **ORDER BY** multiple columns, both columns must be category columns

- **MUST** choose a category column to **GROUP BY** (IE towns, states, type of cars, department of work)
- Categorical columns are unique ID's, phone numbers
- ORDER BY and GROUP BY statements will overwrite the SELECT statements when showing the output

### DATE 
Removes the timestamp from the DATETIME column
- Very useful for using DATE as a categorical column instead of unique timestamp

### HAVING 
Allows you to filter aggregate data columns like the WHERE clause for category columns
> **Query Example:** SELECT column1, SUM(column2) FROM table WHERE column1 != ’whatever’ GROUP BY column1 HAVING SUM(column2) > 1000
> 
> This means our output table won't include any SUM less than 1000
   
> [!Important]
> This does nothing to affect calculating the SUM, only omitting the specified final aggregate answer.

### AS
Allows us to rename a column in the output table, (this is strictly for readability)
> **Query Example::** SELECT column1, SUM(column2) AS total spent FROM table GROUP BY column1 ORDER BY SUM(column2) HAVING SUM(column2) > 100      

> [!Important]
> that you reference SUM(column2) for all query statements since AS total statement is only in the visual aspect and will throw an error if used elsewhere in the query statement

## Joins
Joins allow the combination of multiple tables together to retreive values on either table. Venn diagrams are a good visual representation of how this happens. Visual examples of joins [here](https://blog.codinghorror.com/a-visual-explanation-of-sql-joins/).
> **Query Example:** SELECT foo FROM bar JOIN FooBar

> [!Important]
> To specify columns in joins uses the syntax tableA.column1 and tableB.column1. You do not need to specify which table if there is no column with the same name.

![Join representation]()

### Inner Joins
| | |
|-|-|
| **Query Example:** SELECT column1 FROM TableA <br> **INNER JOIN** TableB ON TableA.col = TableB.col <br><br> This returns columns where both table have the same value| ![img](pictures/Venn_diagram_inner_join.png)|

### Full Outer Joins
| | |
|-|-|
| **Query Example:** SELECT column1 FROM TableA <br> **FULL OUTER JOIN** TableB ON TableA.col = TableB.col <br><br> This returns all columns. If there is no match, the missing side will have null as values but still be apart of the table| ![img](pictures/Venn_diagram_full_outer.png)|

| | |
|-|-|
| **Query Example:** SELECT * FROM tableA <br> FULL OUTER JOIN tableB ON tableA.col = tableB.col <br> **WHERE tableA.col IS null OR tableB IS null**<br><br> This returns all columns that do not match. **The opposite of an inner join**| ![img](pictures/.png)|

### Left Outer Join
| | |
|-|-|
| **Query Example:** SELECT column1 FROM TableA <br> **LEFT OUTER JOIN** TableB ON TableA.col = TableB.col <br><br> This returns all values in TableA and values in TableB that match TableA. | ![img](pictures/Venn_diagram_full_outer.png)|

| | |
|-|-|
| **Query Example:** SELECT column1 FROM TableA <br> LEFT OUTER JOIN TableB ON TableA.col = TableB.col <br> **WHERE TableA.col IS null or TableB.col IS null** <br><br> This returns all columns in TableA that dont match TableB| ![img](pictures/Venn_diagram_full_outer.png)|

### Unions
This is essentially pasting a table below the current table. To do this you need to have tables with the same number of columns and preferrably matching columns. (IE Q1 sales and Q2 sales tables) 
> **Query Example:** SELECT column_name(s) FROM table1
> **UNION (ALL)**
> SELECT column_name(s) FROM table2;

![Visual represenation of Unions]()
