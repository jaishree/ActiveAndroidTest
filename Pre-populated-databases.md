To use a pre populated database place a copy of it in the assets directory. To ensure the database works properly with Android take the following steps:

1. Setup the android_metadata table
```sql
    CREATE TABLE "android_metadata" ("locale" TEXT DEFAULT 'en_US')

    INSERT INTO "android_metadata" VALUES ('en_US')
```

2. Rename all the primary key fields to named Id (not _id like standard Android databases)


#### Notes

This will cause duplication of the database as it will be packaged with the apk and copied into the `/data/data/yourpackage/databases` directory as well.