Schemas are migrated using sql-scripts in `/assets/migrations`. Whenever your schema (e.g. classes that are annotated with `@Table(…)`) changes you need to

1. increase the meta-information AA_DB_VERSION.
2. provide a script `<NewVersion>.sql` in `/assets/migrations`.

ActiveAndroid will execute a script if its filename if greater then the old database-version and smaller or equal to the new version.

Let’s assume you added a column `colour` to the `Items` table. You now need to increase AA_DB_VERSION to 2 and provide a script `2.sql`. 

```sql
alter table Items add colour(varchar);
```
