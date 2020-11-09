# Linh Nguyen
## TSQL Homework 9

1.What is a temporal table?

	A system-versioned temporal table has two columns representing the validity period of the row, plus a linked history table with a mirrored schema holding older states of modified rows.
	it's something that allows you to go back in time. So, if you wanted to see exactly what the situation was, you could.
	
2.Under what circumstances would you use a temporal table? Temporal tables are in widespread use in certain kinds of businesses.

	To find data from a time range, Auditing.
	To look up the history of a banking account for example. Any time you would want to look up anything important to you in history.
	
3.What are the semantics of a temporal table? There are seven of them.

	A primary key, Two columns defined as DATETIME2, A start column, An end column, A designation of the period columns, The table option SYSTEM_VERSIONING, A linked history table.	
	
4.How do you search a history table?

	Browse the object tree in Object Explorer in SQL Server Management Studio (SSMS).
	you run a query against the main table
	
5.How do you modify a history table?

	You modify only the current table with INSERT, UPDATE, DELETE, and MERGE statements.
	Modifying temporal tables is similar to modifying regular tables. You modify only the current table with INSERT, UPDATE, DELETE, and MERGE statements. You modify the current table.
	
6.How do you delete date from a history table? Why would you want to delete data from a history table?

	Delete row.
	Use the 'DELETE' command. The need to track something is no longer needed. 'DELETE' the row or drop the column
	
7.How do you search a history table?

	SELECT statement uses the FOR SYSTEM_TIME FROM TO clause to retrieve all active rows within the time range specified by the @StartTime and @EndTime values.
	
8.How do you query all data from both a history file and the current data?

	If you want to query the current state of the data, you simply query the current table as you would query a normal table. If you want to query a past state of the data, you still query the current table, but you add a clause called FOR SYSTEM_TIME and a sub clause that indicates the validity point or period of time you’re interested in.
	You utilize the 'GO' command, between to different queries.
	
9.How do you drop a temporal table?

	SYSTEM_VERSIONING OFF, DROP TABLE IF EXISTS.