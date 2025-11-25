# JDBC Improvements

JDBC 4.1, which is part of Java 7, introduces the following features:
✓ The ability to use a try-with-resources statement to automatically close resources of type
Connection, ResultSet, and Statement
✓ RowSet 1.1: The introduction of the RowSetFactory interface and the RowSetProvider class,
which enable you to create all types of row sets supported by your JDBC driver.
• You can use a try-with-resources statement to automatically close java.sql.Connection,
java.sql.Statement, and java.sql.ResultSet objects, regardless of whether a SQLException or any
other exception has been thrown. A try-with-resources statement consists of a try statement
and one or more declared resources (which are separated by semicolons).
• With the help of new RowSetFactory interface and the RowSetProvider class, we can create a
RowSet objects of CachedRowSet/ FilteredRowSet / JdbcRowSet / JoinRowSet / WebRowSet.
Before Java 7 we used to depend on JdbcRowSetImpl class for the same.