### BST
### HEAPS
### STACK
### QUEUE
### SEGMENT TREE
### RED BLACK TREE
### RECURSION
### DYNAMIC PROGRAMMING
### STRINGS
### ARRAYS
### LINKEDLIST
### THREADING
* https://www.callicoder.com/java-locks-and-atomic-variables-tutorial/
* https://www.callicoder.com/java-8-completablefuture-tutorial/
* blocking queue
* producer & consumer
* even & odd thread

### HASHING
* collision
* equals & hashcode
* double hashing
* concurrent read one write bucket

### COMPLETABLE FUTURE

### CLONING & SINGLETON
* deep cloning
* swallow cloning

### SERIALIZATION

### MUTABLE
* string, stringbuffer, string builder

### OAUTH
* https://medium.com/@athiththan11/oauth-2-grant-types-a-story-guide-582580a3c4c2
* https://tools.ietf.org/html/rfc6749#section-1.3

### SQL

	Join (All types of join)- left outer, right inner, full join, 

	Indexing- Cluster index and non-clustered index?

	Having and group by

	Emp table.
Name	ID	Salary	Department	Manager
				
				

Sample queries
* Write a query to find 2nd highest salary and 3rd highest salary from a table.
* Query to find out the all the dept. names consists more than 100 emp?
* Query to find out the Emp name whose salary is more than his manager?
* Query to find the max salary?
* Query to Find duplicate rows in a table? And delete the duplicate records?
```sql
-- asssume name is duplicate.
-- find duplicate records using inner query
 SELECT * FROM TBL_CUST C WHERE C.NAME IN (SELECT NAME FROM TBL_CUST GROUP BY NAME HAVING COUNT(*) > 1)
-- find duplicate records using join. having count by with group by name > 1
SELECT C.* FROM TBL_CUST C 
JOIN (SELECT * FROM TBL_CUST GROUP BY NAME HAVING COUNT(*) > 1) B
ON C.NAME=B.NAME;
-- find duplicate records to delete. delete the record other than max(id)
SELECT * FROM TBL_CUST K
JOIN (
SELECT MAX(C.ID) ID,C.NAME FROM TBL_CUST C 
JOIN (SELECT * FROM TBL_CUST GROUP BY NAME HAVING COUNT(*) > 1) B
ON C.NAME=B.NAME GROUP BY C.NAME
) T 
ON K.ID < T.ID AND K.NAME=T.NAME;
```

