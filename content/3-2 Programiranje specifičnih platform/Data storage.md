### SharedPreferences
Small storage for ==key-value pairs== of primitive types, need to know data type when accessing
App specific: R/W access, removed on app uninstall
Usecases: user preferences $\rightarrow$ `PreferenceFragmentCompat` connects XML-defined layout of preferences with values from storage
### DataStore
Modern replacement for SharedPreferences - async operation, type safety
### File storage
Java File API
Access: `openFileOutput()`/`openFileInput()`: open file for writing / reading
#### App-specific files
Permissions not needed for access
App specific: removed on app uninstall
##### Internal files
Encrypted
Access: `getFilesDir()`/`getCacheDir()`
##### External files
Not encrypted by default
Access: `getExternalFilesDir()`/`getExternalCacheDir()`
#### Shared files
Accessible by all aplications: remain when apps uninstalled
Types: Media / Documents / Datasets
Deprecated for MediaStore and Storage Access Framework
### SQLite database
==Non-concurrent, single file== relational database library
App specific: removed on app uninstall
Access:
- `SQLiteOpenHelper`: manage schema, `SQLiteDatabase`: queries
- Room ORM