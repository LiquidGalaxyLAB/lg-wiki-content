---
title: Creating and initializing a SQFlite database
contributor: Davit Mas
date: 2024-06-13T15:50:17.851+00:00
---
## Overview
SQFlite is a powerful plugin for integrating a SQLite database into Flutter applications. With SQFlite, a developer can efficiently store and manage data locally on a user’s device.  
  
_**Getting Started**_  
Before diving into the implementation, ensure that you have Flutter installed and a Flutter project set up.  
  
**1 - Add SQFlite dependency:** Start by adding SQFlite dependency in your ‘pubspec.yaml’ file. It should look something like this:  
  
![Add SQFlite dependency](https://lh7-us.googleusercontent.com/docsz/AD_4nXf8ZahEzByBpABEKytYkBKJ_BzVtYJaACgul6PWZmZzO4qG0LWumCzUNYovZ17x6BAKcdoME3E_BcxI8SoJXBKiAgG8MmGmi4w_Sxcqw3LL30sUWp81QFX7P0-_Gxax23A_nP_EBmWx9SPCB_o9oLPOZVgL?key=2EBtkbpklIlojwTog9jp-g "Add SQFlite dependency")  
**2 - Run ‘flutter pub get’:** After adding the dependencies, run ‘flutter pub get’ in your terminal or Android Studio to download and install the package.  
  
_**Creating the Database**_  
Now let’s create a SQLite database by using SQFlite in your application. Firstly, you need to import the SQFlite package into the file where you’ll define the database. Import the path package as well. Use the line

```dart
import 'package:path/path.dart';
import 'package:sqflite/sqflite.dart';
```

  
Next, create a DataBaseService class with 4 functions. It should look something like this:

```dart
class DataBaseService {
 Database? _database;


 Future<Database> get database async {
   if (_database != null) {
     return _database!;
   }
   _database = await _initialize();
   return _database!;
 }


 Future<String> get fullPath async {
   const name = 'yourdbname.db';
   final path = await getDatabasesPath();
   return join(path, name);
 }


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

  
This database service will work in complementarity with your own DB class, which is shown in the following entry: _link to following entry_  
  
Finally, you will need to ensure the DBService exists in main. It should look like this:

```dart
Future<void> main() async {
 sqfliteFfiInit();
 databaseFactory = databaseFactoryFfi;


 WidgetsFlutterBinding.ensureInitialized();
 final dbService = DataBaseService();
 Database database = await dbService.database;
}
```

  
_**Conclusion:**_  
These have been the steps to create and initialize a database to your flutter project. Even though this database is still empty. In _link to entry_ you’ll find how to create the different tables and setting the database operations and functions to make them callable from your main app.
