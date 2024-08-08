# **SQL Query Commands**
 
### **SELECT** selects columns to return
>**Query Example:** SELECT **\*** FROM table
>> grabs everything
 
### **DISTINCT** selects only unique rows in the specified column
>**Query Example:** SELECT DISTINCT(column) FROM table
>> grabs unique columns only
 
### **COUNT** returns the number of input rows that match a specific condition or query
>**Query Example:** SELECT COUNT(column) FROM(table
>> returns the number of rows in name column from table
- parenthesis is required to specify column
- If checking how many rows are in a table COUNT(\*) is acceptable
> **NOTE:** SELECT COUNT( DISTINCT column) FROM table
>> returns the number of unique names in the column
 
### **WHERE** is used to filter rows returned from the SELECT statement 
>**Query Example:** SELECT column FROM table WHERE something = ‘something’ (case sensitive)
- Appears immediately after the FROM clause
- You can use comparison operators (=, &gt;, &lt;, &lt;= & &gt;=, &lt;&gt; or !=)
- You can use logical operators (AND, OR, NOT)

### **ORDER BY** is used to sort rows based on column value  
>**Query Example:** SELECT column1, column2 FROM table ORDER BY column1, column2 ASC/DESC
>>**NOTE:** This will order by column1  first, then column2
- Put towards the end of the query statement. Filter and select first, then order.
- Can do either ascending or descending
- Can sort multiple columns, but order by what column is listed first

### **LIMIT** allows us to limit the number of rows returned for a query
>**Query Example:** SELECT * FROM table LIMIT #
-	Useful in large tables, where we want to just get the top x of a query OR an idea of the top of the query results
-	Goes at the very bottom of the command request
> **NOTE:** SELECT * FROM table LIMIT 1
>> is commonly used to see the layout of a table

### **BETWEEN** is used to specify values in the middle of a low and high value
>**Query Example:** SELECT * FROM table WHERE column BETWEEN lowValue AND highValue
-	BETWEEN low and high is the same as WHERE (value >= low AND value <= high)
   -	**NOTE:** Just improved syntax
-	Also, can use NOT BETWEEN low AND high  

---
**Important:** Using **BETWEEN** for dates is not optimal  

Either explicitly cast    
> WHERE cast(created_at as date) BETWEEN '2013-05-01' AND '2013-05-01'  <br>

**Or**

Explicitly binary compare  
> WHERE created_at >= '2013-05-01' AND created_at < '2013-05-02'
---

### **IN** is used to filter rows that determine if the specified values exist within the columns.  
This is used when you want to specify multiple values in a  column typically.
> **Query Example:** SELECT column1 FROM table WHERE column1 in (value1, value2, ...)
-	This only shows the rows where value1 and value2  appear in column1
-	AKA WHERE column1 = ‘value1’ OR column1 = ‘value2’ OR ...

### **LIKE** allows you to match column values with general patterns.   
- IE ends with @gmail.com or all  names that end in ‘A’
- Wildcard char is % (percent sign)
> **Query Example:** WHERE name LIKE ‘A%’

returns all names that begin with an uppercase A
- Replace a single char by _ (underscore)
> **Query Example:** WHERE name LIKE ‘Mission  Impossible _’

returns all mission impossible movies

### **ILIKE** is case Insensitive
> **Query Example:** WHERE name ILIKE ‘A%’

returns all names that begin with A regardless of case.

