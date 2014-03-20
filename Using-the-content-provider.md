**Note**
You must override the default identity column as specified here (https://github.com/pardom/ActiveAndroid/pull/132) before the following will work:

```java
	mySpinner.setAdapter(new SimpleCursorAdapter(getActivity(),
		android.R.layout.simple_expandable_list_item_1,
		null,
		new String[] { "MyProperty" },
		new int[] { android.R.id.text1 },
		0));
	
	getActivity().getSupportLoaderManager().initLoader(0, null, new LoaderCallbacks<Cursor>() {
		@Override
		public Loader<Cursor> onCreateLoader(int arg0, Bundle cursor) {
			return new CursorLoader(getActivity(),
				ContentProvider.createUri(MyEntityClass.class, null),
				null, null, null, null
			);
		}
		
		@Override
		public void onLoadFinished(Loader<Cursor> arg0, Cursor cursor) {
			((SimpleCursorAdapter)mySpinner.getAdapter()).swapCursor(cursor);
		}
		
		@Override
		public void onLoaderReset(Loader<Cursor> arg0) {
			((SimpleCursorAdapter)mySpinner.getAdapter()).swapCursor(null);
		}
	});
```

You must also have the following `provider` in your `AndroidManifest.xml`:
```
<application ...>
    <provider android:authorities="com.example" android:exported="false" android:name="com.activeandroid.content.ContentProvider" />
    ...
</application>
```