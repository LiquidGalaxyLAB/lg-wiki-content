---
title: Creating and modifying tables in a SQFlite database\:
contributor: Davit Mas
date: 2024-06-13T16:01:33.443+00:00
---

\
If you have an existent database in your flutter project, you are most likely going to need to be able to add and modify tables to the database.\
\
***Table creation:***\
 This is the most essential of steps, as it is required to do any operation on a database. The table is the structure where all of the data is saved, with all of its elements. You will need to follow a series of steps:\
\
**1 - Creation of the database file:** Although this step is optional, it’s going to be useful in keeping your code in a tidy way. This file’s name should be something along databasename_db.dart\
\
**2 - Importing the database service and your models:** In order to make the database work, you’ll need to have the model which you will be saving as well as your database services class in order to make it work.\
\
**3 - Create a database class:** This class should have only your tables’ names, looking something like this:
```dart
class myDB {
 final tableName = 'myTable';
```
\
**4 - Add a create table function:** This function will only be executed once per table, and it uses quite a lot of raw code. The function needs to include the different attributes that your model has, together with their type and other requirements for them. It should look something like this:
```dart
Future<void> createTable(Database database) async {
 await database.execute("""CREATE TABLE IF NOT EXISTS $tableName (
   "attribute1"  TEXT NOT NULL,
   "attribute2" TEXT NOT NULL,
   "attribute3" INTEGER,
   PRIMARY KEY ("attribute1")
 );""");
}
```
\
**5 - Call this function from the database service:** The createTable function should be called from the DBService when it is initialized. It should look like this:
```dart
 Future<Database> _initialize() async {
   final path = await fullPath;
   var database = await openDatabase(path,
       version: 1, onCreate: create, singleInstance: true);
   return database;
 }

 Future<void> create(Database database, int version) async {
   yourDB.create() //you must have created a db class
 }
}
```
\
**Modifying a table’s content:** The functions that will be explained from now are meant to be called from the actual code instead of main. These are the functions that will add, update and delete data from your table.\
\
**Inserting data:** The following function allows you to add data in the database:
```dart
Future<int> insertDB(
   {required String attribute1,
   required String attribute2,
   int attribute3,
   }) async {
 final database = await DataBaseService().database;
 return await database.rawInsert(
   '''INSERT INTO $tableName (attribute1, attribute2,
   attribute3) VALUES (?, ?, ?) ''',
   [attribute1, attribute2, attribute3],
 );
}
```
\
**Fetching data:** The following function allows you to get all of the data in the database. You can also insert some requirements to only get the data you’re interested in. One without conditions looks like this:
```dart
Future<List<Crop>> fetchAll() async {
 final database = await DataBaseService().database;
 final crops = await database
     .rawQuery('''SELECT * FROM $tableName ORDER BY attribute1''');
 return crops.map((crop) => Model.fromSqfliteDatabase(crop)).toList();
}
```
\
When ever you execute another function, such as the insert one, you should call this one after, in order to refresh, even if you don’t use the return value for anything.\
\
**Updating data:** This function is used to get an existent data in the table and change it, either completely or just partly. It should look like this. The parameters of the function should correspond to the attributes of the specific row we want to update.
```dart
Future<int> updateData(
   {required String attribute1,
   String attribute2,
  int attribute3}) async {
 final database = await DataBaseService().database;
 return await database.update(
   tableName,
   {
     if (attribute1 != null) 'attribute1': attribute1,
     if (attribute2 != null) 'attribute2': attribute2,
     if (attribute3 != null) 'attribute3': attribute3,
   },
   where: 'attribute1 = ?',
   conflictAlgorithm: ConflictAlgorithm.rollback,
   whereArgs: [attribute1],
 );
}
```
\
**Deleting crops:** The last function that we will look at is the one that deletes a row given its primary key. It looks like this:
```dart
Future<void> deleteData(String attribute1) async {
 final database = await DataBaseService().database;
 await database
     .rawDelete('''DELETE FROM $tableName WHERE attribute1 = ?''', [attribute1]);
}
```
\
**Conclusion:** By following these steps, your database is now usable and can be used to actually store data, as it’s meant to. SQFlite simplifies database integration in Flutter, as you can now call a single function and allow yourself to have data stored permanently locally.
