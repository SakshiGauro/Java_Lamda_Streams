# JDBC Improvements (Java 7 – JDBC 4.1)

Java 7 introduced enhancements to JDBC through **JDBC 4.1**, making database operations safer and easier to manage.

**Key Improvements**
- **Automatic Resource Management** using _try-with-resources_
- **RowSet 1.1 Enhancements** to create all types of row sets supported by your JDBC driver
  - New `RowSetFactory` interface
  - New `RowSetProvider` class
  - Ability to create any supported RowSet type (CachedRowSet, JdbcRowSet, FilteredRowSet, JoinRowSet, WebRowSet)

Before Java 7, developers relied on specific implementation classes like `JdbcRowSetImpl`. Java 7 makes RowSet creation flexible and standardized.

---

## Try-With-Resources for JDBC

Java 7 allows `Connection`, `Statement`, and `ResultSet` to be automatically closed by the JVM.

**Before Java 7**
You had to manually close `con`, `stmt`, and `rs` in a `finally` block.

**From Java 7 onward**
The JVM closes them automatically.

### Example 1: Using _try-with-resources_ with ResultSet
```java
public static void viewResults() throws Exception {
    try (Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/organization", "root", "root");
            Statement stmt = con.createStatement();
            ResultSet rs = stmt.executeQuery("select * from employee");) {
        while (rs.next()) {
            System.out.println(rs.getString("NAME") + "" + rs.getInt("AGE") + "" + rs.getString("DEPARTMENT"));
        }
    } catch (Exception e) {
        throw e;
    }
}
```
**Benefit:**
No need to explicitly close `con`, `stmt`, or `rs`. JVM handles it automatically.

---

## RowSet vs ResultSet
In Java JDBC, both **ResultSet** and **RowSet** are used to represent tabular data retrieved from a database, but they differ significantly in their capabilities and how they interact with the database.

### What is a ResultSet?
- Represents the data returned from a SQL query.
- Usually connected, meaning it requires an active database (DB) connection.
- Cannot be **serialized**, meaning it cannot be easily passed across network boundaries or stored for later use without an active connection
- Not scrollable or updatable by default.
- Fetches data as needed, typically in a forward-only traversal of query results.


### What is a RowSet?
- A more advanced version of ResultSet (extends `ResultSet`).
- Can be either connected (like `JdbcRowSet`) or disconnected (like `CachedRowSet`, `WebRowSet`)
  - When it's disconnected, it fetches all data into memory, disconnects from the database, and allows operations and modifications while offline. It reconnects only when changes need to be written back to the database. 
- Serializable, making them suitable for passing data over networks, storing in files, or using in distributed applications.
- Scrollable and updatable depending on the type.
- Additional features like filtering and joining.
- Supports event listeners and JavaBeans properties.

### Summary
|Feature |	ResultSet | 	RowSet                                                                                                                                   |
|--------- |--------- |-------------------------------------------------------------------------------------------------------------------------------------------|
|Needs connection |Yes | Not always                                                                                                                                |
|Scrollable |No (default) | Yes                                                                                                                                       |
|Updatable |Limited | Yes                                                                                                                                       |
|Event listeners |No | Yes                                                                                                                                       |
|JavaBean support |No | Yes                                                                                                                                       |
|Serialization| Not serializable | **Disconnected** `RowSet` objects are serializable                                                                                        | 
|Flexibility| Less flexible| More flexible, especially **disconnected** `RowSets`                                                                                      |
| Use Case |Direct interaction with database, simple data retrieval | Distributed applications, offline data manipulation, data transfer RowSets provide more flexibility and usability compared to ResultSets. |

---

### Example 2: Creating a RowSet using RowSetProvider

```java
public static void createJdbcRowset() throws Exception {
    try (JdbcRowSet jRS = RowSetProvider.newFactory().createJdbcRowSet();) {
        jRS.setUrl("jdbc:mysql://localhost:3306/organization");
        jRS.setUsername("root");
        jRS.setPassword("root");
        jRS.setCommand("select * from employee");
        jRS.execute();
        while (jRS.next()) {
            System.out.println(jRS.getString("NAME") + "" + jRS.getInt("AGE") + "" + jRS.getString("DEPARTMENT"));
        }
    } catch (Exception e) {
        throw e;
    }
}
```

**RowSetProvider**

`JdbcRowSet jRS = RowSetProvider.newFactory().createJdbcRowSet();`

This lets JDBC dynamically create **any RowSet type supported by the driver**.

---
