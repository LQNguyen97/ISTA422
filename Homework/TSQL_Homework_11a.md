# Linh Nguyen
## TSQL Chapter 11a

1. Why do we use variables in T-SQL? How do you declare and initialize T-SQL variables? Can you declare and initialize a variable in a single step?

	To temporarily store data values for later use in the same batch in which they were
	declared
	Use a DECLARE statement to declare one or more variables
	use a SET statement to assign a value to a single variable
	Yes. DECLARE @i AS INT = 10;

2. Why is the assignment SET method for setting a variable safer than the assignment SELECT method?

	It requires you to use a scalar subquery to pull data from a table
	Scalar subquery fails at run time if it returns more than one value

3. Describe what is meant by a batch file in T-SQL? What is the difference between batches and transactions?

	One or more T-SQL statements sent by a client application to SQL Server for execution as a single unit.
	A transaction is an atomic unit of work. A batch can have multiple transactions

4. Can a transaction be split between multiple batches? Can a batch be split between multiple transactions? Explain.

	Yes. A transaction can be submitted in parts as multiple batches.
	Yes. A batch can have multiple transactions

5. What is meant when the book says that “a batch is a unit of resolution?” Explain binding.

	This means that checking the existence of objects and columns happens at the batch level.

6. What is the scope of variables with respect to T-SQL batches?

	The scope of a variable is the range of Transact-SQL statements that can reference the variable. The scope of a variable lasts from the point it is declared until the end of the batch or stored procedure in which it is declared.

7. Give a practical example of the use of the GO n operator that is not in the book.

	Use it when you don't want to write something over and over again.

8. How to you delimit if ...else constructions that contain multiple statements?

	you need to use a statement block. You mark the boundaries of a statement block with the BEGIN and END keywords

9. Does T-SQL provide a SWITCH ...CASE type of construct? See chapter 2 if you don’t recall. If it exists, is it interchangeable with the if ...else construct?

	Not interchangeable, If...Else program construct does not return a value, Switch...Case statement is an expression that return a value.

10. What is the difference between a relation and a cursor?

	A relation is another name for a table/ a set
	A cursor is used to retrieve results, a cursor is not a set/relation. It is a collection.

11. What are the specific steps to use a cursor? List the steps.

	1. Declare the cursor based on a query.
	2. Open the cursor.
	3. Fetch attribute values from the first cursor record into variables.
	4. As long as you haven’t reached the end of the cursor (while the value of a function called @@FETCH_STATUS is 0), loop through the cursor records; in each iteration of the loop, perform the processing needed for the current row, and then fetch the attribute values from the next row into the variables.
	5. Close the cursor./Close the address.
	6. Deallocate the cursor./Deallocate the memory.

12. What is the scope of a local temporary table?

	A local temporary table is visible only to the session that created it, in the creating level and all inner levels in the call stack (inner procedures, triggers, and dynamic batches).

13. When are global temporary tables destroyed? What is the main difference between local temporary tables and global temporary tables?

	A local temporary table is destroyed automatically by SQL Server when the creating level in the call stack goes out of scope. global temporary table is visible to all other sessions.

14. Under what conditions would you use a table variable instead of a local temporary table? Why would you refer to use a local temporary table instead of a table variable?

	It depend, you need to see which one run faster.
	usually it makes more sense to use table variables with small volumes of data (only a few rows) and to use local temporary tables otherwise.

15. What is a table type? What is the syntax for creating a table type? Whhat is the syntax for using a table type?

	Table definition. Saving a schema and you don't have to recreate a schema everytime.

