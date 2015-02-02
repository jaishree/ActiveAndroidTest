You can use a pre-populated database by following these steps: 

1. Place a copy of the SQLite database file in the `assets` directory of your application, for example: 

    `/myapp/src/main/assets/prepop.db`

2. Ensure you set the `AA_DB_NAME` in the manifest file, for example:

    ```xml
<meta-data android:name="AA_DB_NAME" android:value="prepop.db" />
```

Now when you deploy your application it will copy the `prepop.db` file from the `assets` directory to `/data/data/myapp/databases` storage. 

_Note: This will cause a duplication of the database as it will be both, packaged with the APK and copied to the storage directory._


#### Ensure the Database Works Properly with ActiveAndroid

To ensure the database works properly with ActiveAndroid take the following steps:

1. Setup the android_metadata table

    ```sql
CREATE TABLE "android_metadata" ("locale" TEXT DEFAULT 'en_US')

INSERT INTO "android_metadata" VALUES ('en_US')
```

2. If you have not defined the `id` column name for your models, ensure the primary keys are renamed to the default, `Id`, instead of `_id`, which is the standard for Android databases. However, if your data is to be displayed in `ListViews`, for example, it is recommended to define your primary key columns as `_id`. You can do this by simply adding a `id = "_id"` param to the `@Table` annotation on your model, like so:

    ```java
@Table(name = "Items", id = "_id")
public class Item extends Model {
```