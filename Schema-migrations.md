If new classes are added, ActiveAndroid will automatically add them to the database. If you want to change something in an existing table however (e.g. add or delete a column), this is done using sql-scripts which can be put in `assets/migrations`. Whenever your schema (i.e. classes that extend `Model`) changes you need to

1. increment the database version number, either through `Configuration` or AA_DB_VERSION meta-data.
2. provide a script `<NewVersion>.sql` in `/assets/migrations`.

ActiveAndroid will execute a script if its filename if greater then the old database-version and smaller or equal to the new version.

Let’s assume you added a column `colour` to the `Items` table. You now need to increase AA_DB_VERSION to 2 and provide a script `2.sql`. 

```sql
ALTER TABLE Items ADD COLUMN Color INTEGER;
```