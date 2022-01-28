# How to perform UPSERT

When there is a `PRIMARY KEY` or a `UNIQUE INDEX` that will violate UNIQUE CONSTRAINT it is possible to use an UPSERT approacy. Where the MySQL database will tro to insert the value but in case the value throws an unique exception it will update it. 

The follow command can be used:

```sql
INSERT INTO table (c1, c2, c3)
VALUES (v1, v2, v3) AS NEW_VALUES
ON DUPLICATE KEY UPDATE
   c1 = NEW_VALUES.v1, 
   c2 = NEW_VALUES.v2,
   c3 = NEW_VALUES.v3,
   c4 = DEFAULT
```

Full doc https://dev.mysql.com/doc/refman/8.0/en/insert-on-duplicate.html