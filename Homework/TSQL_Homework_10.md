# Linh Nguyen
## TSQL Chapter 10

1. What is the purpose of transactions? Why do we use transactions in SQL scripts?

	A transaction is a unit of work that might include multiple activities that query and modify data and that can also change the data definition.
	Transactions are used to maintain data integrity for both related operations and when multiple users that update the database concurrently.

2. Briefly describe each of the ACID properties.

	Atomicity: either all changes in a transaction take place or none do.
	Consistency: the state of the data that the relational database system gives you access to as concurrent transactions modify and query it.
	Isolation: ensures that transactions access only consistent data.
	Durability: Data changes are always written to the database's transaction log on the disk before they are written to the data portion of the database on disk.

3. What do we mean when we talk about the granularity of locks?

	The level of detail of the lock. I.e. before getting a shared lock on a certain level of detail (granularity), your transaction must acquire intent shared locks on higher levels. I.e. if a row on a table is locked by a transaction, and a different transaction is asking for an incompatible lock on the whole page, the conflict is identified and an error is thrown.

4. What do we mean when we talk about the modes of locks?

	Different types of locks that are used when a transaction is processing. These locks prevent other transactions from querying the table, until the transaction is complete.
	Exclusive and Shared Lock. 

5. In your ownh words, describe blocking, and give an example.

	A transaction request on an incompatible lock on the same resource is blocked if another transaction holds a lock on it, and the requester enters a wait state. The blocked request keeps waiting until the blocker releases the interfering lock.
	My words: If someone is using a bathroom and another person tries to open the door, the door won't open because the door is locked. The person then has to wait until the bathroom door is unlocked and the person inside finishes.

6. What are the properties of locks? That is, list the column name and column type of the fields in sys.dm tran locks.

	session id, resource type, database id, dbname, res description, resource associated entity id, request mode, request status

7. What are the properties of sessions? That is, list the column name and column type of the fields in sys.dm exec connections.

	sessionid, connect_time, last_read, last_write, most_Recent_sql_handle

8. What are the requests of sessions? That is, list the column name and column type of the fields in sys.dm exec requests.

	session_id, login_time, host_name, program_name, login_name, nt_user_name, last_request_start_time, last_Request_end_time

9. What is an isolation level? Give an example of the operation of an isolation level.

	Isolation levels determine the level of consistency you get when you interact with data. In a box product, a reader uses shared locks on the target resources and a writer users exclusive locks. You cannot control the way writers behave in terms of the locks they acquire and the duration of the locks, but you can control how readers behave.

10. (Not in the book.) What do we mean when we say that an object is serializable?

	It means that an object converts its state to a byte stream, so the byte stream can be reverted back into a copy of the object.

11. What is an deadlock? Give an example of a deadlock?

	A deadlock is when two or more sessions block each other. When session A blocks session B and session B blocks session A.