Now that you have your database model setup, let’s save some records to the database.

### Inserting and updating records

To save a new record, just create a new instance of an ActiveAndroid Model class, assign values to its fields, and call the save() method. That’s all. The save method works for both inserting and updating records.

Here’s an example

```java
Category restaurants = new Category();
restaurants.name = "Restaurants";
restaurants.save();
```

Now let’s create an Item record, and assign a category to it

```java
Item item = new Item();
item.category = restaurants;
item.name = "Outback Steakhouse";
item.save();
```

Let’s add some more items. We don’t need to create new objects though, we just need to call the object’s constructor again.

```java
item = new Item();
item.category = restaurants;
item.name = "Red Robin";
item.save();
 
item = new Item();
item.category = restaurants;
item.name = "Olive Garden";
item.save();
```

### Deleting records

What about deleting a record? Well, to delete a single record just call the delete() method. In the following example we’ll load an Item object by Id and delete it.

```java
Item item = Item.load(Item.class, 1);
item.delete();
```

You can also use the query builder syntax

```java
new Delete().from(Item.class).where("Id = ?", 1).execute();
```

Next, let's look at [Querying the database](Querying-the-database).