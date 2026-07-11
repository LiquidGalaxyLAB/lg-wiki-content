---
title: Connection in an API in a Flutter App
contributor: Davit Mas
date: June 14, 2024
---
## Overview
\
***Connection to an API:*** While doing a Flutter app, you may encounter the need for creating an API or accessing one. Luckily, Flutter has you covered. There are two types of API’s you will encounter, those being remote ones and local ones. Here’s how you can establish connection to both of them:\
\
***Remote API Connectivity:*** First of all, you will need in mind that, in order to connect to any API, you need to use the http library. So, once you’ve added it to pubspec and imported it, you can easily make requests to an external API via the GET, POST, PUT and DELETE requests.\
\
Here’s an example of a GET request:
```dart
Future<void> fetchData() async {
 final response = await http.get(Uri.parse('https://api.example.com/data'));
 if (response.statusCode == 200) {
   // Data successfully fetched
   print(response.body);
 } else {
   // Request failed
   print('Failed to fetch data: ${response.statusCode}');
 }
}
```
\
***Local API Connectivity:*** Keeping in mind what has been said about the Remote API Connectivity, that being the need for the http library, we can already set up connectivity, with some extra steps.\
\
**1 - Setup localhost:** Make sure that your local API is running and on the correct address. ‘This will mostly be [http://localhost:port’](liquidgalaxylab@gmail.com)\
**2 - Network permissions:** Make sure that your app has the necessary permissions to access the API, especially if you’re testing on physical devices.\
**3 - API request:** Once you’re sure everything is running accordingly, you can proceed as you did in remote API’s. Here’s an example of a local GET request:
```dart
Future<void> fetchData() async {
 final response = await http.get(Uri.parse(‘localhost:8000/data'));
 if (response.statusCode == 200) {
   // Data successfully fetched
   print(response.body);
 } else {
   // Request failed
   print('Failed to fetch data: ${response.statusCode}');
 }
}
```
\
**Conclusion:** With everything shown here, you can now easily make calls to API and get much needed data for your app.

