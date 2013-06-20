ActiveAndroid handles many types by default. If the need arrises for handling a custom data type, you easily do so using TypeSerializer. The best way to learn how it works is by looking at an example. Let's consider the Date type.

When creating a TypeSerializer we must consider how we can reduce the Data type down to a primitive type that ActiveAndroid can handle. Dates can be converted to a Long, so let's use that type.

Here's the code used in the ActiveAndroid source for Dates.

```java
final public class UtilDateSerializer extends TypeSerializer {
	@Override
	public Class<?> getDeserializedType() {
		return Date.class;
	}

	@Override
	public SerializedType getSerializedType() {
		return SerializedType.INTEGER;
	}

	@Override
	public Long serialize(Object data) {
		if (data == null) {
			return null;
		}

		return ((Date) data).getTime();
	}

	@Override
	public Date deserialize(Object data) {
		if (data == null) {
			return null;
		}

		return new Date((Long) data);
	}
}
```

The first method we see is getDeserializedType. In this method we return the class we are serializing. For the Date TypeSerializer we return Date.class.

The second method returns the inverse type. That is, the type we want to store in the database. Rather than expecting a literal type returned, we have an enumeration value to choose from.

You can use the following enumeration values for this method.

```java
public enum SQLiteType {
	INTEGER, REAL, TEXT, BLOB
}
```

The next method transforms our supported data type into a data type ActiveAndroid can store. Here we use the getTime() method of Date to return a Long.

The last method inflates the data stored in the database into the supported data type. Date can be constructed with a Long, so we use the stored Long data to return a new Date object.

To register your custom type serializers with Active Android, you need to declare them in AndroidManifest.xml.

```xml
<meta-data android:name="AA_SERIALIZERS" android:value="my.package.CustomTypeSerializer, my.package.AnotherCustomerTypeSerializer" />
```