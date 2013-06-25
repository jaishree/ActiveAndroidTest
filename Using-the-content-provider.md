**Note**
Issue #83 must be fixed (column "Id" renamed to "_id") before the following will work:

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
				((SimpleCursorAdapter)c.selector.getAdapter()).swapCursor(cursor);
			}
			
			@Override
			public void onLoaderReset(Loader<Cursor> arg0) {
				((SimpleCursorAdapter)c.selector.getAdapter()).swapCursor(null);
			}
		});