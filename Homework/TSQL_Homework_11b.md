# Linh Nguyen
## TSQL Homework 11b

1. What is dynamic SQL?

	Construct a batch of T-SQL code as a character string and then execute that batch.(pg.379)	

2. In executing dynamic SQL, what are the differences between using the EXEC command and the sp executesp stored procedure?

	The EXEC command accepts a character string in parentheses as input and executes the batch of code within the character string.
	The sp_executesql stored procedure is an alternative tool to the EXEC command for executing dynamic SQL code. It’s more secure and more flexible in the sense that it has an interface; that is, it supports input and output parameters.

3. What is a SQL injection attack? Give an example of an attack.

	SQL injection is a web security vulnerability that allows an attacker to interfere with the queries that an application makes to its database. It generally allows an attacker to view data that they are not normally able to retrieve.

4. How do you execute the EXEC command? Write a complete example using the TSQLV4 database.

	Stores a character string with a PRINT statement in the variable @sql and then uses the EXEC command to invoke the batch of code stored within the variable:
	DECLARE @sql AS VARCHAR(100);
	SET @sql = 'PRINT ''This message was printed by a dynamic SQL batch.'';';
	EXEC(@sql);

5. Describe the use of input parameters and output parameters for the sp executesql stored procedure.

	parameters that appear in the code cannot be considered part of the code—they can only be considered operands in expressions. So, by using parameters, you can eliminate your exposure to SQL injection. 

6. What are the three kinds of routines that T-SQL recognizes?

	User-defined functions, stored procedures, and triggers.

7. What is the difference between a stored procedure, a user defined function, and a 	trigger?

	The purpose of a user-defined function (UDF) is to encapsulate logic that calculates something, possibly based on input parameters, and return a result. A UDF appears anywhere in query where an expression return a value. 
	
	Stored procedures are routines that encapsulate code. They can have input and output parameters, they can return result sets of queries, and they are allowed to have side effects. Not only can you modify data through stored procedures, you can also apply schema changes through them. 
	
	A trigger is a special kind of stored procedure—one that cannot be executed explicitly. Instead, it’s attached to an event. Whenever the event takes place, the trigger fires and the trigger’s code runs.
	

8. What is the primary function of a UDF? This is not specifically stated in the book but is clear fro the context of the discussion n the book.

	Accept parameters, perform an action, such as a complex calculation, and return the result of that action as a value. The return value can either be a single scalar value or a result set.

9. (Not in book.) What are side effects, and why are they dangerous?

	Anything that happens outside the boundary of a function. 

10. What is the principle distinction between a UDF and a stored procedure?

	The major difference is that UDFs can be used like any other expression within SQL statements, whereas stored procedures must be invoked using the CALL statement.
	UDFs are not allowed to have any side effects. 

11. Given that you cannot execute a trigger explicitly, what is the advantage of using triggers?

	A trigger is considered part of the transaction that includes the event that caused the trigger to fire. Issuing a ROLLBACK TRAN command within the trigger’s code causes a rollback of all changes that took place in the trigger, and also of all changes that took place in the transaction associated with the trigger.
	
	You can use triggers for many purposes, including auditing, enforcing integrity rules that cannot be enforced with constraints, and enforcing policies. 

12. In using error handling in T-SQL, can you mimic a finally block? If so, how?

	Yes. Try...Catch. If the TRY block has no error, the CATCH block is simply skipped. If the TRY block has an error, control is passed to the corresponding CATCH block. 

13. Write a user defined function that returns a Booleans as to whether a customer may purchase alcohol as of the instant that the function runs.

	DROP FUNCTION IF EXISTS dbo.GetAge;
	GO
	CREATE FUNCTION dbo.GetAge
	(
	 @birthdate AS DATE, 
	  @eventdate AS DATE
	)
	RETURNS INT
	AS
	BEGIN
	 RETURN
	 DATEDIFF(year, @birthdate, @eventdate)
	 - CASE WHEN 100 * MONTH(@eventdate) + DAY(@eventdate)
	 < 100 * MONTH(@birthdate) + DAY(@birthdate)
	 THEN 1 ELSE 0
	 END;
	END;
	GO

14. Write a trigger that places a customer in the OFF LIMITS table if he attempt to purchase alcohol when he is underage.

		
	DROP TABLE IF EXISTS dbo.T1_Audit, dbo.T1;
	CREATE TABLE dbo.T1
	(
	 keycol INT NOT NULL PRIMARY KEY,
	 datacol VARCHAR(10) NOT NULL
	);
	CREATE TABLE dbo.T1_Audit
	(
	 audit_lsn INT NOT NULL IDENTITY PRIMARY KEY,
	 dt DATETIME2(3) NOT NULL DEFAULT(SYSDATETIME()),
	 login_name sysname NOT NULL DEFAULT(ORIGINAL_LOGIN()),
	 keycol INT NOT NULL,
	 datacol VARCHAR(10) NOT NULL
	);


15. Write a stored procedure that deletes customers from the OFF LIMITS table when they have reached their 21st birthday.

	DROP PROC IF EXISTS Sales.GetCustomerOrders;
	GO
	CREATE PROC Sales.GetCustomerOrders
	 @custid AS INT,
	 @fromdate AS DATETIME = '19000101',
	 @todate AS DATETIME = '99991231',
	 @numrows AS INT OUTPUT 
	AS
	SET NOCOUNT ON;
	SELECT orderid, custid, empid, orderdate
	FROM Sales.Orders
	WHERE custid = @custid
	 AND orderdate >= @fromdate
	 AND orderdate < @todate;
	SET @numrows = @@rowcount;
	GO
