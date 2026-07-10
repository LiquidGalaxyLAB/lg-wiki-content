---
title: Integration of Local Database ( Using Hive )
contributor: Vivek Maurya
date: 2024-06-11T15:05:39.196+00:00
---

  
While writing an app that needs to persist and query large amounts of data on the local device,we consider using a database instead of a local file or key-value store. In general, databases provide faster inserts, updates, and queries compared to other local persistence solutions.  
  
No SQL Database - NoSQL databases (aka "not only SQL") are non-tabular databases and store data differently than relational tables. NoSQL databases come in a variety of types based on their data model. The main types are document, key-value, wide-column, and graph. They provide flexible schemas and scale easily with large amounts of data and high user loads.  
  
We can use Hive, which is a lightweight and fast NoSQL database that can be used to store data in Flutter applications.  
  
![No_SQL_Database](https://lh7-us.googleusercontent.com/docsz/AD_4nXfijejh76r7JLFGAbsNAo_uBT3r8x9TOjCAHra7QujTqUNQkYtuA_2c1TE9T29rnaBc98-cqcp85YL5FAZ4TiWQVHZluwj_g99Kw3tEB1K_1YdV7F8sH78rPUc-Db9_lr-m7kvD5KzjT1Xus64hIntCbmZ3?key=z-Vc2n5DI5rzjFwO_dKKZQ "No_SQL_Database")  

* * *

  
_**Using Hive Database :**_  
  
## Initializing Hive
Initializing Hive with a valid directory in app files or we can also provide a subdirectory:

```dart
await Hive.initFlutter();
```

  
## Opening a Box
All of the data is stored in boxes.\\

```dart
var box = await Hive.openBox('testBox');
```

  
## Read & Write
Hive supports all primitive types, List, Map, DateTime, BigInt and Uint8List.

```dart
import 'package:hive/hive.dart';

void main() async {
  //Hive.init('somePath') -> not needed in browser

  var box = await Hive.openBox('testBox');

  box.put('name', 'David');
  
  print('Name: ${box.get('name')}');
}
```
