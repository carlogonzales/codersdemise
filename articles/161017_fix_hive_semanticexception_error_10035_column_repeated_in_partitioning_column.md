# Fix Hive `SemanticException [Error 10035]: Column repeated in partitioning columns`

While creating a new table with partition and you got this error:

```bash
SemanticException [Error 10035]: Column repeated in partitioning columns
```

You have redundantly included a column to be partitioned on your create table clause.

Say we want to create a *user* table partitioned by *lastname* the following create statement will generate the above error:

```bash
CREATE TABLE `user` (
  `firstname` STRING,
  `lastname` STRING,
  `age` INT
)
PARTITIONED BY (lastname STRING);
```

## Moving of Columns to Partioned By Clause

To fix this, we need to remove the declaration of *lastname* column from the create table clause.

```bash
CREATE TABLE `user` (
  `firstname` STRING,
  `age` INT
)
PARTITIONED BY (`lastname` STRING);
```
