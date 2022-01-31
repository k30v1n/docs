# How to select columns as json

Its possible to transform several columns into a json by using the following function.

```sql
SELECT 
    id,
    JSON_OBJECT (
        "id", id,
        "name", full_name,
        "created_date", creationdate,
        "details", JSON_OBJECT(
                "address", address_column,
                "country", country
            )
    ) as json_data
FROM table_name;
```

Generated json:
```json
{
    "id": 1,
    "name": "full name of someone",
    "created_date": "2022-01-31 00:00:00",
    "details": {
        "address": "the address of this someone",
        "country": "country code"
    }
}
```
