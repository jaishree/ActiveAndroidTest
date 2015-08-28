Creating the database model is easy. Just create classes named your desired table name, which have annotated fields for each of the columns.

There are only two important things to keep in mind. Your class must extend the Model class and your members must be annotated using **@Column**. ActiveAndroid will handle primitive data types as well as relationships to other tables and date classes.

One important thing to note is that ActiveAndroid creates an id field for your tables. This field is an auto-incrementing primary key.

### Constructors
ActiveAndroid uses the standard-constructor of your class to instantiate objects. If you define your own constructors you have to define a parameterless constructor as well. Look in the source code for more documentation.

```java
@Table(name = "Items")
public class Item extends Model {
        // If name is omitted, then the field name is used.
        @Column(name = "Name")
        public String name;

        @Column(name = "Category")
        public Category category;

        public Item() {
                super();
        }

        public Item(String name, Category category) {
                super();
                this.name = name;
                this.category = category;
        }
}
```

### Relationships

In the previous article we used the example of Categories and Items. Items belong in a Category and Categories have many Items. How do we represent that relationship with ActiveAndroid?

In the Item class we can make a direct relationship to the Category it is in by creating a Category member.

```java
@Table(name = "Items")
public class Item extends Model {

	@Column(name = "Name")
	public String name;

	@Column(name = "Category")
	public Category category;
}
```

Similarly, the Category class can indicate it’s relationship to many Items. We do this with a helper method.

```java
@Table(name = "Categories")
public class Category extends Model {
	@Column(name = "Name")
	public String name;

        // This method is optional, does not affect the foreign key creation.
	public List<Item> items() {
		return getMany(Item.class, "Category");
	}
}
```

### Setting indexes

You can set indexes on specified columns by setting `index = true` in the Column definition annotation.

```java
	@Column(name = "Name", index = true)
	public String name;

	@Column(name = "Category", index = true)
	public String category;
```

This will create a query on both columns

### Speeding up application startup

ActiveAndroid will look through all your files to find your Model classes. This process can be very slow if you have a lot of dependencies. To speed up this process, specify your Model classes explicitely in your AndroidManifest:

```xml
<meta-data
    android:name="AA_MODELS"
    android:value="com.myapp.model.Item, com.myapp.model.Category" />
```

### Reserved Table and Column Names

Do not use the following table and column names or trouble will ensue:
```
ABORT               DEFAULT         INNER         REGEXP
ACTION              DEFERRABLE      INSERT        REINDEX
ADD                 DEFERRED        INSTEAD       RELEASE
AFTER               DELETE          INTERSECT     RENAME
ALL                 DESC            INTO          REPLACE
ALTER               DETACH          IS            RESTRICT
ANALYZE             DISTINCT        ISNULL        RIGHT
AND                 DROP            JOIN          ROLLBACK
AS                  EACH            KEY           ROW
ASC                 ELSE            LEFT          SAVEPOINT
ATTACH              END             LIKE          SELECT
AUTOINCREMENT       ESCAPE          LIMIT         SET
BEFORE              EXCEPT          MATCH         TABLE
BEGIN               EXCLUSIVE       NATURAL       TEMP
BETWEEN             EXISTS          NO            TEMPORARY
BY                  EXPLAIN         NOT           THEN
CASCADE             FAIL            NOTNULL       TO
CASE                FOR             NULL          TRANSACTION
CAST                FOREIGN         OF            TRIGGER
CHECK               FROM            OFFSET        UNION
COLLATE             FULL            ON            UNIQUE
COLUMN              GLOB            OR            UPDATE
COMMIT              GROUP           ORDER         USING
CONFLICT            HAVING          OUTER         VACUUM
CONSTRAINT          IF              PLAN          VALUES
CREATE              IGNORE          PRAGMA        VIEW
CROSS               IMMEDIATE       PRIMARY       VIRTUAL
CURRENT_DATE        IN              QUERY         WHEN
CURRENT_TIME        INDEX           RAISE         WHERE
CURRENT_TIMESTAMP   INDEXED         RECURSIVE     WITH
DATABASE            INITIALLY       REFERENCES    WITHOUT
                    ID
```

*If you find others, please add them to the list.*

--------------------------------------------------------

That’s all there is to it! Next, let's take a look at [saving to the database](Saving-to-the-database).