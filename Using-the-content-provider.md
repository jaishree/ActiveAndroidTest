**Note**
Issue [#83](https://github.com/pardom/ActiveAndroid/issues/83) must be fixed (column "Id" renamed to "_id") before the following will work:

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