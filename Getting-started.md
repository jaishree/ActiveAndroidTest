Let’s get started with ActiveAndroid. The first thing you need to do, if you haven’t already done so, is [download the ActiveAndroid library.](https://github.com/pardom/ActiveAndroid/archive/master.zip) or the latest stable [ActiveAndroid jar file](https://github.com/pardom/ActiveAndroid/downloads). If you downloaded the library and not the jar, you'll have to build the jar file by running `ant` in the root folder. Your ActiveAndroid.jar, which is what we need, will be in the `dist` folder.


## Adding The JAR

Now that you have the ActiveAndroid library you can **add it to your project’s build path**. If you’re using Eclipse:

1. If you haven’t done so already, create an Android project.
2. Copy ActiveAndroid.jar to the _libs_-folder of your new project.
2. Right click on your project and select _Build Path > Configure Build Path…_
3. Click the _Add External Jars…_ button and choose the ActiveAndroid jar file.

If you're using Android Studio:

1. If you haven’t done so already, create an Android project.
2. Drag the jar to the libs folder of project. 
3. Right click on the jar, and select "Add as a Library…"

## Installing From Maven

First, clone the source from Git and install the package to your local repository:  
**Note: Maven 3.1.1 or later is required**

1. `git clone https://github.com/pardom/ActiveAndroid.git`
2. `cd ActiveAndroid`
3. `mvn clean install`

After the project builds successfully, add the following dependency to your `pom.xml`

```xml
<dependency>
	<groupId>com.activeandroid</groupId>
	<artifactId>activeandroid</artifactId>
	<version>(insert latest version)</version>
</dependency>
```

## Installing with Gradle

Modify your build.gradle to include:

    repositories {
        mavenCentral()
        maven { url "https://oss.sonatype.org/content/repositories/snapshots/" }
    }
    
    compile 'com.michaelpardo:activeandroid:3.1.0-SNAPSHOT'

## Configuring Your Project

Now that you have ActiveAndroid added to you project, you can begin your two-step configuration process! The first thing we’ll need to do is add some global settings. ActiveAndroid will look for these in the AndroidManifest.xml file. Open the AndroidManifest.xml file located at the root directory of your project. Let’s add some configuration options.

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

Notice also that the application name points to the ActiveAndroid application class. **This step is required** for ActiveAndroid to work. If you already point to a custom Application class, just make that class a subclass of com.activeandroid.app.Application.

If you are using a custom Application class, just extend com.activeandroid.app.Application instead of android.app.Application

```java
public class MyApplication extends com.activeandroid.app.Application { ...
```

But what if you're already doing this to utilize another library? Simply initialize ActiveAndroid in the Application class. You may call ```ActiveAndroid.dispose();``` if you want to reset the framework for debugging purposes. (Don’t forget to call initialize again.)

```java
public class MyApplication extends SomeLibraryApplication {
	@Override
	public void onCreate() {
		super.onCreate();
		ActiveAndroid.initialize(this);
	}
}
```

If you want to build a database dynamically.You can use the configuration class.

```java
public class MyApplication extends SomeLibraryApplication {
	@Override
	public void onCreate() {
		super.onCreate();
                Configuration dbConfiguration = new Configuration.Builder(this).setDatabaseName("xxxx.db").create();
		ActiveAndroid.initialize(dbConfiguration);
	}
}
```

In our example we have two tables: Category and Item.  
In step two you will create classes for those tables.  
Don’t worry though, this part is easy too.

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