Let’s get started with ActiveAndroid. The first thing you need to do, if you haven’t already done so, is download the ActiveAndroid library. 

## Adding the JAR
By cloneing the source, or downloading it you can build the jar file by running `ant` in the root folder. Your ActiveAndroid.jar, which is what we need, will be in the dist folder.

Now that you have the ActiveAndroid library you can **add it to your project’s build path**. We’ll assume you’re using Eclipse. If you haven’t done so already, create an Android project.

Right click on your project and select _Build Path > Configure Build Path…_

Click the _Add External Jars…_ button and choose the ActiveAndroid jar file.

## Installing from Maven
First clone the source from Git and install the package to your local repository

* git clone https://github.com/pardom/ActiveAndroid.git
* cd ActiveAndroid
* mvn clean install

After the project builds successfully, add the following dependency to your pom.xml

```xml
<dependency>
	<groupId>com.activeandroid</groupId>
	<artifactId>activeandroid</artifactId>
	<version>(insert latest version)</version>
</dependency>
```

## Configuring your project

Now that you have ActiveAndroid added to you project, you can begin you two step configuration process! The first thing we’ll need to do is add some global settings. ActiveAndroid will look for these in the AndroidManifest.xml file. Open the AndroidManifest.xml file located at the root directory of your project. Let’s add some configuration options.

* AA_DB_NAME (optional)
* AA_DB_VERSION (optional – defaults to 1)

The configuration strings for my project look like this

```xml
<manifest ...>
	<application android:name="com.activeandroid.app.Application" ...>

		...

		<meta-data android:name="AA_DB_NAME" android:value="Pickrand.db" />
		<meta-data android:name="AA_DB_VERSION" android:value="5" />

	</application>
</manifest>
```

Notice also, that the application name points to the ActiveAndroid application class. **This step is required** for ActiveAndroid to work. If you already point to a custom Application class, just make that class a subclass of com.activeandroid.app.Application.

If you are using a custom Application class, just extend com.activeandroid.app.Application instead of android.app.Application

```java
public class MyApplication extends com.activeandroid.app.Application { ...
```

But what if you're already doing this to utilize another library? Simply initialize and dispose ActiveAndroid in the Application class.

```java
public class MyApplication extends SomeLibraryApplication {
	@Override
	public void onCreate() {
		super.onCreate();
		ActiveAndroid.initialize(this);
	}
	@Override
	public void onTerminate() {
		super.onTerminate();
		ActiveAndroid.dispose();
	}
}
```

In our example two tables: Category and Item. In step two you will create classes for those tables. Don’t worry though, this part is easy too.

We'll go into more detail about setting up the database model later, but here are our classes.

```java
@Table(name = "Categories")
public class Category extends Model { 
	@Column(name = "Name")
	public String name;
}

@Table(name = "Items")
public class Item extends Model {
	@Column(name = "Name")
	public String name;
 
	@Column(name = "Category")
	public Category category;
}
```

That’s it for configuration. Next, let's learn about [creating your database model](Creating-your-database-model).