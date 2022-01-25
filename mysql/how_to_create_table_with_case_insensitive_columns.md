# How to create table with case insensitive columns

MySQL includes character set support that enables you to store data using a variety of character sets and perform comparisons according to a variety of collations. The default MySQL server character set and collation are utf8mb4 and utf8mb4_0900_ai_ci, but you can specify character sets at the server, database, table, column, and string literal levels.

- [Chapter 10 Character Sets, Collations, Unicode](https://dev.mysql.com/doc/refman/8.0/en/charset.html)
- [10.3 Specifying Character Sets and Collations](https://dev.mysql.com/doc/refman/8.0/en/charset-syntax.html)
- [10.3.1 Collation Naming Conventions](https://dev.mysql.com/doc/refman/8.0/en/charset-collation-names.html)

Every “character” column (that is, a column of type CHAR, VARCHAR, a TEXT type, or any synonym) has a column character set and a column collation. Column definition syntax for CREATE TABLE and ALTER TABLE has optional clauses for specifying the column character set and collation:

```sql
col_name {CHAR | VARCHAR | TEXT} (col_length)
    [CHARACTER SET charset_name]
    [COLLATE collation_name]
```
These clauses can also be used for ENUM and SET columns:

```sql
col_name {ENUM | SET} (val_list)
    [CHARACTER SET charset_name]
    [COLLATE collation_name]
```


Examples
```sql
CREATE TABLE t1
(
    col1 VARCHAR(5)
      CHARACTER SET latin1
      COLLATE latin1_german1_ci
);


ALTER TABLE t1 MODIFY
    col1 VARCHAR(5)
      CHARACTER SET latin1
      COLLATE latin1_swedish_ci;


CREATE TABLE t2
(
    col1 CHAR(10) CHARACTER SET utf8 COLLATE utf8_unicode_ci
) CHARACTER SET latin1 COLLATE latin1_bin;

CREATE TABLE t3
(
    col1 CHAR(10) CHARACTER SET utf8
) CHARACTER SET latin1 COLLATE latin1_bin;
```

[10.3.5 Column Character Set and Collation](https://dev.mysql.com/doc/refman/8.0/en/charset-column.html)


In MySQL(5.7) we can create a table with case insensitive columns by using  "COLLATE  utf8mb4_unicode_ci" in the column definition.

In MySQL(8.0) and up we can create a table with Case insensitive and Accent sensitive columns by declaring  "COLLATE  utf8mb4_0900_as_ci" in the column definition.
