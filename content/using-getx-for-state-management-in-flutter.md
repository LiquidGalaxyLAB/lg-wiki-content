---
title: "Using GetX for state management in Flutter\:"
contributor: Aritra Biswas
date: 2024-06-05T13:06:54.417+00:00
---

GetX is an extremely popular framework combining features like simple state-management, route management, dependency injection, and other simple changes into one package. Now, you might ask, what is state management? Why should we do it? 
State management is a good practice for app development, especially when our app needs to share data and states between many different screens. State management packages trivialize this task, separating the data and working code from its UI.\
\
\________________________________________________________________________________________________________________
## **Setting Up GetX** 
\
First, create your Flutter project and open the pubspec.yaml file.\
Add these under dependencies:\
	get: ^4.6.6\
	get_storage: ^2.1.1\
Run the flutter pub get command.\
Now, you should have access to the GetX package.

\________________________________________________________________________________________________________________
## **Using GetX for State-management** 
\
 **Update the MaterialApp widget.**\
Use the GetMaterialApp instead of the MaterialApp widget in your main.dart file. This gives access to all GetX properties across the application.\
\
 **Add the GetX controller.**\
The GetX Controller class is the component that separates the UI and the business logic. It controls the state of the UI, and when we wrap a widget with its observer, it only rebuilds that particular widget in case of a change in state.\
\
We add a new dart file to store our controller, say data_controller, which extends the GetxController:

```javascript
class DataController extends GetxController {}
```
\
Next, we add a few parameters to this class with the .obs at the end of the value. This makes the variable observable. Then, when the variable changes, other parts will change accordingly.\
\
```javascript
final data = "Data1".obs;
final dataList = ["Data0","Data1","Data2","Data3","Data4","Data5"].obs;
final currentIndex = 0.obs;
```
\
Now, we create some methods to update these parameters as required:

```javascript
updateData(String d)
{
 data(d);
}
buttonPress()
{
 currentIndex((currentIndex.value+1)>dataList.value.length-1?0:currentIndex.value+1);
 updateData(dataList.value[currentIndex.value]);
}
```
\
Now, we instantiate our controller in the main file.
```javascript
final dataController= Get.put(DataController());
```
After instantiating, we need to wrap the widget, which needs to be rebuilt due to changes in our controller values, in an Obx() widget:
```javascript
Obx( () => OurWidget())
```
\
Now, we can use our controller as needed, and only the widget wrapped in our Obx() widget gets rebuilt with state changes.\
\
```javascript
Obx( () =>
   Row(

   mainAxisAlignment: MainAxisAlignment.center,
   children: <Widget>[
     Text(
       "${dataController.currentIndex.value.toString()}.",
       style: TextStyle(fontSize: 25.0),
     ),
     SizedBox(width: 25.0,),
     Text(
       dataController.data.value.toString(),
       style: Theme.of(context).textTheme.headlineMedium,
     ),
   ],
 ),
),


floatingActionButton: FloatingActionButton(
 onPressed: (){dataController.buttonPress();},
 tooltip: 'Increment',
 child: const Icon(Icons.move_down),
),
```
\
That was a simple yet effective way to leverage the GetX package for state management of your Flutter Apps. For a simple project demonstrating this usage, check out: [AritraBiswas9788/GetXDemo (github.com)](https://github.com/AritraBiswas9788/GetXDemo).\
\
\________________________________________________________________________________________________________________

## **Making POST/GET requests using GetX:**
\
An extremely useful functionality for GetX is its GetConnect class, which allows us to make HTTP/ HTTPS requests extremely easily. API endpoint requests are an extremely important part of most modern apps as they rely on these to fetch data for the app to use. This makes GetX the perfect package to rely on for such requests since it will fetch the data as well as handle its processing.\
\
First we create a getConnect() reference:
```javascript
final _connect = GetConnect();
```
\
Now we can use this reference to make network requests from within the app using .get() and .post() functions.\
To request data from an API endpoint, we use:
```javascript
void _sendGetRequest() async {
    final response =
        await _connect.get('https://jsonplaceholder.typicode.com/posts/1');
print(response.body);   
}
```
\
To send data to an API endpoint, we can use:
```javascript
void _sendPostRequest() async {
    final response = await _connect.post(
      'https://jsonplaceholder.typicode.com/posts',
      {
        'title': 'one two three',
        'body': 'four five six seven',
        'userId': 1,
      },
    );
      print(response.body);
}
```
To upload multiple files to an API endpoint, we first create a FormData with MultiPartFiles containing the files we want to load.\
\
To create this, we use: 
```javascript
final FormData _formData = FormData({
      'file1': MultipartFile(File('path to file1'), filename: 'pic.jpg'),
      'file2': MultipartFile(File('path to file 2'), filename: 'pic.png'),
      'file3': MultipartFile(File('path to file 3'), filename: 'pic.gif'),
      'otherData': {/* other data */}
});
```
\
To Creating this FormData instance will allow us to upload multiple Files with a single POST request.\
\
This is done as follows:
```javascript
try {
      final Response res =
          await _connect.post('your API URL here', _formData, headers: {
        /* headers information like Authorization, Cookie, etc */
      });

      // Do something with the response
      print(res.body);
} catch (err) {
      // Handle errors
      print(err);
}
```
\
\________________________________________________________________________________________________________________
## **Quality of Life Functionalities from GetX:**
\
GetX also provides many functions that make general code much more manageable. Some of these are:

1. ### **Route Navigation**
\
Screen Navigation is simple with Get.to()

```javascript
Get.to(Home());
```
\
Going back to the previous screen:
```javascript
Get.back();
```
\
Named route navigation while handling Drawers and Dialog boxes:
```javascript
// for named routes
Get.toNamed('/second'),
// to close, then navigate to named route
Get.offAndToNamed('/second'),
```

2. ### **Simple Useful Widgets:**
\
**Snackbars-**
```javascript
Get.snackbar(
   'title',
   'message',
   snackPosition: SnackPosition.BOTTOM,
colorText: Colors.white,
backgroundColor: Colors.black,
borderColor: Colors.white);
```
\
**Dialogs -**
```javascript
Get.defaultDialog(
   radius: 10.0,
   contentPadding: const EdgeInsets.all(20.0),
   title: 'title',
   middleText: 'content',
   textConfirm: 'Okay',
   confirm: OutlinedButton.icon(
     onPressed: () => Get.back(),
     icon: const Icon(
       Icons.check,
       color: Colors.blue,),
     label: const Text('Okay',
       style: TextStyle(color: Colors.blue),
     ),   ),
 cancel: OutlinedButton.icon(
     onPressed: (){},
     icon: Icon(),
     label: Text(),),);
```
\
**Bottom sheets**
```javascript
Get.bottomSheet(
   Container(
 height: 150,
 color: AppColors.spaceBlue,
 child: Center(
     child: Text(
   'Count has reached ${obxCount.value.toString()}',
   style: const TextStyle(fontSize: 28.0, color: Colors.white),
 )),
));
```
\
\________________________________________________________________________________________________________________
## **Conclusion** 
\
There are many state-management packages available, like GetX, BLoC, Redux, Provider, etc. However, even among these, GetX stands out as an all-encompassing micro-framework that provides a lot of functionality to our app-building experience.


