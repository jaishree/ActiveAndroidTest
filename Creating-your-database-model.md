Creating the database model is easy. Just create classes named your desired table name, which have annotated fields for each of the columns.

There are only two important things to keep in mind. Your class must extend the Model class and your members must be annotated using **@Column**. ActiveAndroid will handle primitive data types as well as relationships to other tables and date classes.

One important thing to note is that ActiveAndroid creates an id field for your tables. This field is an auto-incrementing primary key.

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

	public static List<Item> items() {
		return getMany(Item.class, "Category");
	}
}
```

That’s all there is to it!