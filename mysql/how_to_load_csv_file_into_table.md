# How to load CSV file into a table

## TL;DR;
```sql
LOAD DATA
	LOCAL INFILE '/Users/<user>/file.csv' 
	REPLACE 
	INTO TABLE target_table 
	FIELDS TERMINATED BY ','
	IGNORE 1 LINES (
		`id`,
		`name`,
		@phone_number,
		`creation_date`,
		@active
	)
  SET `phone_number` = REPLACE(@phone_number, '"', ''),
      `active` = @IsActive AND 1;
```

Some key points below extracted from original doc https://dev.mysql.com/doc/refman/8.0/en/load-data.html . Also at the bottom a common error that may occur about `Loading local data is disabled; this must be enabled on both the client and server sides`.

## LOAD DATA statement

The `LOAD DATA` statement reads rows from a text file into a table at a very high speed. The file can be read from the server host or the client host, depending on whether the LOCAL modifier is given. LOCAL also affects data interpretation and error handling.

```sql
LOAD DATA
    [LOW_PRIORITY | CONCURRENT] [LOCAL]
    INFILE 'file_name'
    [REPLACE | IGNORE]
    INTO TABLE tbl_name
    [PARTITION (partition_name [, partition_name] ...)]
    [CHARACTER SET charset_name]
    [{FIELDS | COLUMNS}
        [TERMINATED BY 'string']
        [[OPTIONALLY] ENCLOSED BY 'char']
        [ESCAPED BY 'char']
    ]
    [LINES
        [STARTING BY 'string']
        [TERMINATED BY 'string']
    ]
    [IGNORE number {LINES | ROWS}]
    [(col_name_or_user_var
        [, col_name_or_user_var] ...)]
    [SET col_name={expr | DEFAULT}
        [, col_name={expr | DEFAULT}] ...]
```

`LOCAL` compared to `NON-LOCAL` statements:
- It changes the expected location of the input file;
- It changes the statement security requirements; 
- It has the same effect as the IGNORE modifier on the interpretation of input file contents and error handling (Duplicate-Key and Error Handling)

> `LOCAL` works only if the server and your client both have been configured to permit it. For example, if mysqld was started with the local_infile system variable disabled, LOCAL produces an error. See Section 6.1.6, “Security Considerations for LOAD DATA LOCAL”.


## Character Set

The file name must be given as a literal string. On Windows, specify backslashes in path names as forward slashes or doubled backslashes. The server interprets the file name using the character set indicated by the character_set_filesystem system variable.

## Input File Location

`non-LOCAL`:
- If the file name is an absolute path name, the server uses it as given.
- If the file name is a relative path name with leading components, the server looks for the file relative to its data directory.
- If the file name has no leading components, the server looks for the file in the database directory of the default database.
> The non-LOCAL rules mean that the server reads a file named as ./myfile.txt relative to its data directory

`LOCAL`
- If the file name is an absolute path name, the client program uses it as given.
- If the file name is a relative path name, the client program looks for the file relative to its invocation directory.

> When `LOCAL` is used, the client program reads the file and sends its contents to the server. The server creates a copy of the file in the directory where it stores temporary files. Lack of sufficient space for the copy in this directory can cause the LOAD DATA LOCAL statement to fail.

## Security requirements
For `non-LOCAL` the load operation reads data from the server host, so these securities requirements should be satisfied:
- The connected user should have `FILE` privilege
- The operation is subject to `the secure_file_priv` system variable setting:

For `LOCAL`
- The client program reads a text file located on the client host. Because the file contents are sent over the connection by the client to the server. 
- Dont need FILE privilege

> Using LOCAL is a bit slower than when the server accesses the file directly. On the other hand, you do not need the FILE privilege, and the file can be located in any directory the client program can access.


## Duplicate-Key and Error Handling
The `REPLACE` and `IGNORE` modifiers control handling of new (input) rows that duplicate existing table rows on unique key values (`PRIMARY KEY` or `UNIQUE index` values):

- With `REPLACE`, new rows that have the same value as a unique key value in an existing row replace the existing row
> So it would work like `UPSERT`, where new values would be inserted and existing values updated.

- With IGNORE, new rows that duplicate an existing row on a unique key value are discarded. 
> So it would work like a `INSERT IGNORE`, where new values would be inserted and existing values ignored. 

Loading data using  The `LOCAL` modifier has the same effect as `IGNORE`. This occurs because the server has no way to stop transmission of the file in the middle of the operation.

If none of `REPLACE`, `IGNORE`, or `LOCAL` is specified, an error occurs when a duplicate key value is found, and the rest of the text file is ignored.

`IGNORE` and `LOCAL` also affects error handling

- With neither IGNORE nor LOCAL, data-interpretation errors terminate the operation.
- With IGNORE or LOCAL, data-interpretation errors become warnings and the load operation continues, even if the SQL mode is restrictive

## Field and Line Handling
If you specify no FIELDS or LINES clause, the defaults are the same as if you had written this:

```sql
LOAD DATA INFILE '/tmp/test.txt' INTO TABLE test
    FIELDS TERMINATED BY '\t' ENCLOSED BY '' ESCAPED BY '\\'
    LINES TERMINATED BY '\n' STARTING BY ''
```

> For a text file generated on a Windows system, proper file reading might require LINES TERMINATED BY `'\r\n'` because Windows programs typically use two characters as a line terminator

If all the input lines have a common prefix that you want to ignore, you can use LINES STARTING BY 'prefix_string' to skip the prefix and anything before it. If a line does not include the prefix, the entire line is skipped. Suppose that you issue the following statement:


```sql
LOAD DATA INFILE '/tmp/test.txt' INTO TABLE test
  FIELDS TERMINATED BY ','  LINES STARTING BY 'xxx';
```

So if data is like that
```txt
xxx"abc",1
something xxx"def",2
"ghi",3
```

The resulting rows are ("abc",1) and ("def",2). **The third row in the file is skipped because it does not contain the prefix**.

The IGNORE number LINES clause can be used to ignore lines at the start of the file. For example, you can use `IGNORE 1 LINES` to skip an initial header line containing column names:

```sql
LOAD DATA INFILE '/tmp/test.txt' INTO TABLE test IGNORE 1 LINES;
```

To read the comma-delimited file.
```sql
LOAD DATA INFILE 'data.txt' INTO TABLE table2
  FIELDS TERMINATED BY ',';
```

For example a CSV file would be something like
```sql
LOAD DATA INFILE 'data.txt' INTO TABLE table2
  FIELDS TERMINATED BY ','
  IGNORE 1 LINES;
```


## Column list specification

The following example loads all columns of the persondata table:
```sql
LOAD DATA INFILE 'persondata.txt' INTO TABLE persondata;
```

By default, when no column list is provided at the end of the LOAD DATA statement, input lines are expected to contain a field for each table column. If you want to load only some of a table's columns, specify a column list:

```sql
LOAD DATA INFILE 'persondata.txt' INTO TABLE persondata
(col_name_or_user_var [, col_name_or_user_var] ...);
```
> You must also specify a column list if the order of the fields in the input file differs from the order of the columns in the table. Otherwise, MySQL cannot tell how to match input fields with table columns.


# ERRORS TROUBLESHOOT

### `Error Code: 3948. Loading local data is disabled; this must be enabled on both the client and server sides`

It is missing to activate the feature on both on the SERVER and on the used CLIENT connection. - https://dev.mysql.com/doc/refman/8.0/en/load-data-local-security.html

To solve that first enable this on the server side
```sql
SET GLOBAL local_infile=1; -- enable the server side
```

Then enable on the client side. Check the two available instructions 
- `mysql` CLI - Connect to the host and enable `local-infile=1` option
```console
mysql --local-infile=1 -u root -p1
```
- `MySql Workbench client` - follow the instructions bellow to enable the `local-infile` option on the connection

``` 
Edit the connection, on the Connection tab, go to the 'Advanced' sub-tab, and in the 'Others:' box add the line `OPT_LOCAL_INFILE=1`.
```

Done, right now the `LOAD DATA` statement should work. But after the process disable this option from the server side.

```sql
SET GLOBAL local_infile=0; -- disable from the server
```
