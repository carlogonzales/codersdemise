# Fix Hadoop Sqoop Import Thrown Exception "ERROR manager.SqlManager: Error reading from database: java.sql.SQLException"

When you're trying to import and got the kind of log message you see below, then the problem came from an non explicit declaration of driver. Although there are other reasons for this error to be thrown, like old driver, we'll specifically solve the non-explicit declaration of driver on Sqoop. 

> ERROR manager.SqlManager: Error reading from database: java.sql.SQLException: Streaming result set com.mysql.jdbc.RowDataDynamic@6eb58296 is still active. No statements may be issued when any streaming result sets are open and in use on a given connection. Ensure that you have called .close() on any active streaming result sets before attempting more queries.
java.sql.SQLException: Streaming result set com.mysql.jdbc.RowDataDynamic@6eb58296 is still active. No statements may be issued when any streaming result sets are open and in use on a given connection. Ensure that you have called .close() on any active streaming result sets before attempting more queries.
>        at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:934)
>        at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:931)
>        at com.mysql.jdbc.MysqlIO.checkForOutstandingStreamingData(MysqlIO.java:2735)
>        at com.mysql.jdbc.MysqlIO.sendCommand(MysqlIO.java:1899)
>        at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2151)
>        at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2619)
>        at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2569)
>        at com.mysql.jdbc.StatementImpl.executeQuery(StatementImpl.java:1524)
>        at com.mysql.jdbc.ConnectionImpl.getMaxBytesPerChar(ConnectionImpl.java:3003)
>        at com.mysql.jdbc.Field.getMaxBytesPerCharacter(Field.java:602)
>        at com.mysql.jdbc.ResultSetMetaData.getPrecision(ResultSetMetaData.java:445)
>        at org.apache.sqoop.manager.SqlManager.getColumnInfoForRawQuery(SqlManager.java:286)
>        at org.apache.sqoop.manager.SqlManager.getColumnTypesForRawQuery(SqlManager.java:241)
>        at org.apache.sqoop.manager.SqlManager.getColumnTypes(SqlManager.java:227)
>        at org.apache.sqoop.manager.ConnManager.getColumnTypes(ConnManager.java:295)
>        at org.apache.sqoop.orm.ClassWriter.getColumnTypes(ClassWriter.java:1845)
>        at org.apache.sqoop.orm.ClassWriter.generate(ClassWriter.java:1645)
>        at org.apache.sqoop.tool.CodeGenTool.generateORM(CodeGenTool.java:107)
>        at org.apache.sqoop.tool.ImportTool.importTable(ImportTool.java:478)
>        at org.apache.sqoop.tool.ImportTool.run(ImportTool.java:605)
>        at org.apache.sqoop.Sqoop.run(Sqoop.java:148)
>        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
>        at org.apache.sqoop.Sqoop.runSqoop(Sqoop.java:184)
>        at org.apache.sqoop.Sqoop.runTool(Sqoop.java:226)
>        at org.apache.sqoop.Sqoop.runTool(Sqoop.java:235)
>        at org.apache.sqoop.Sqoop.main(Sqoop.java:244)

### Declaring Driver Explicitly

#### STEP 1

To fix the issue you have to add the driver explicitly, in my case I'm using MySQL. So, I'll add `--driver=com.mysql.jdbc.Driver` on my command.

```bash
sqoop import --connect jdbc:mysql://localhost/test --username=root --table=salaries --driver=com.mysql.jdbc.Driver
```
