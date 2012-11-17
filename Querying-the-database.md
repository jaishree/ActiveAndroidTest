All queries in ActiveAndroid use the query builder syntax, or the Model.query() method.

Let's look at some queries by adding to our model. Here's what we have so far:

```java
@Table(name = "Items")
public class Item extends Model {
	@Column(name = "Name")
	public String name;

	@Column(name = "Category")
	public Category category;
}
```

It would be nice if we could get a random item from the database. Let's add a method to do that.

```java
public static Item getRandom() {
	return new Select().from(Item.class).orderBy("RANDOM()").executeSingle();
}
```

Building a query in ActiveAndroid is like building a normal SQL statement. We create a new select object, call from and pass in the Item class. We then call orderBy, passing in "RANDOM". To execute a query we call execute(), or in this case executeSingle().

If we only want to get items from a certain category, we pass in a string for our where class argument. The method would look like this:

```java
public static Item getRandom(Category category) {
	return new Select()
		.from(Item.class)
		.where("Category = ?", category.getId())
		.orderBy("RANDOM()")
		.executeSingle();
}
```

And here's how we get all the items in a category, sorted by name.

```java
public static List<Item> getAll(Context context, Category category) {
	return new Select()
		.from(Item.class)
		.where("Category = ?", category.getId())
		.orderBy("Name ASC")
		.execute();
}
```

Next, let's explore [Type serializers](Type-serializers).