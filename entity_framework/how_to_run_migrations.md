# How to run Entity Framework migrations

To add migration
```
add-migration MIGRATION_NAME	>> adds a new migratin
dotnet ef migrations add MIGRATION_NAME -o OUTPUT_PATH -c DB_CONTEXT_NAMESPACE
```

To remove the latest migration
```
remove-migration
```

Updates the current database with the latest migration version on the project selected
```
update-database	
```

rollback/upgrade current database with this migration version
```
update-database MIGRATION_NAME
```

Translate migrations to SQL script
```
dotnet ef migrations script <FROM> <TO> -o OUTPUT_FILE_PATH -c CONTEXT
```