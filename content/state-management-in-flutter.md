---
title: State management in Flutter
contributor: Peter Atef
date: 2024-06-12T12:40:29.942+00:00
---

  
_**Introduction**_  
  
As you explore Flutter, there comes a time when you need to share the application state (data) between screens, across your app. There are many approaches you can take and many questions to think about.  
  
State management is a pivotal aspect of developing robust and responsive Flutter applications. Flutter, known for its flexibility and productivity, offers a variety of options for managing application state. Understanding these state management techniques is essential for creating efficient, maintainable, and feature-rich Flutter applications.  
  

* * *

  
_**Why State Management Matters:**_  
State management is at the core of any interactive application. It involves tracking and handling the data that represents the current state of your app, including user input, network responses, and changes in the user interface.  
  
**Effective state management is crucial for the following reasons:**  
  
1 - Responsive User Interfaces: Proper state management ensures that your app responds quickly to user interactions, providing a smooth and seamless experience.  
2 - Code Organization: Managing state systematically helps organize your codebase, making it more maintainable and less error-prone.  
3 - Sharing Data: State management enables different parts of your app to access and update shared data, ensuring consistency throughout your application.  
4 - Testing: Well-structured state management facilitates unit testing, making it easier to verify the correctness of your code.  
  

* * *

  
_**State Management Techniques:**_  
Flutter offers several state management techniques, each with its own strengths and use cases:  
  
## Local State (SetState):
  
→ Use Case: For small, simple apps or when managing UI-specific state within a single widget.  
→ Example:

```dart
int _counter = 0;


void _incrementCounter() {
 setState(() {
   _counter++;
 });
}
```

  
## InheritedWidget:
  
→ Use Case: For sharing data down the widget tree without rebuilding the entire tree. → Example:

```dart
class MyInheritedWidget extends InheritedWidget {
 final int data;
 MyInheritedWidget({Key key, this.data, Widget child}) : super(key: key, child: child);


 @override
 bool updateShouldNotify(MyInheritedWidget oldWidget) {
   return data != oldWidget.data;
 }
}
```

  
## Provider (and Riverpod):
  
→ Use Case: For a straightforward, scalable solution to manage state and dependency injection.  
→ Example:

```dart
final counterProvider = StateProvider<int>((ref) => 0);


void incrementCounter() {
 final counter = ref.read(counterProvider);
 counter.state++;
}
```

  
## Redux (and Flutter-Redux):
  
→ Use Case: For managing complex application states, especially when dealing with a large amount of shared data.  
→ Example:

```dart
int counterReducer(int state, action) {
 if (action == Actions.increment) {
   return state + 1;
 }
 return state;
}
```

  
## GetX:
  
→ Use Case: For a simple, reactive state management solution that includes state, dependencies, and routing.  
→ Example:

```dart
var count = 0.obs;


void increment() {
 count++;
}
```

  
## BLoC (Business Logic Component):
  
→ Use Case: For managing the state of an app by separating business logic from the UI layer.  
→ Example:

```dart
class CounterBloc {
 final _counter = BehaviorSubject<int>.seeded(0);
 Stream<int> get counter => _counter.stream;
 void increment() => _counter.sink.add(_counter.value + 1);
}
```

  
## When to Choose Each State Management Solution:
  
→ SetState: Ideal for small apps, quick prototyping, or managing simple UI-specific states within a single widget.  
→ InheritedWidget: Suitable for passing data down the widget tree without needing external packages.  
→ Provider (and Riverpod): A scalable solution that works well for most Flutter apps, balancing simplicity and power.  
→ Redux (and Flutter-Redux): Best suited for complex applications with extensive state management needs.  
→ GetX: Perfect for those who prefer a more reactive, simple, and versatile state management solution.  
→ BLoC: Recommended for larger apps where business logic needs separation from the UI and a more predictable and testable architecture is desired.  
  

* * *

  
_**What is the difference between code architecture and state management?**_  
State management is a way to manage the data through the application but the code architecture is a development concept that is applied during the implementation phase to help the developers maintain the code easily and also help them to add features based on customer’s requirements.  
  
## Architecture Example (compatible with Bloc design pattern):
  
![Architecture Example](https://lh7-us.googleusercontent.com/docsz/AD_4nXc39CD86nsWaBaIk9jYByPHYiN-DY9D9E9N5bQtnpb8aB12lOWhqTjmtxgKxinqRmHfm3p8LHPSu-egmyLyvcmsUCkyHF02jQVfRITRzOtyqrgEdmcmbtUGhfMUOHRCoNkJ4Y2xRgROCN3ijEBNKvTO8eIl?key=eXYxpY5rbSPIPtG3SWVZIQ "Architecture Example")  
## Architecture Layers:
1 - Presentation layers  
2 - Business layer  
3 - Data  
→ Repository  
→ Data Provider  
  
## Data Layer:
The data layer’s responsibility is to retrieve/manipulate data from one or more sources.  
  
The data layer can be split into two parts:  
→ Repository  
→ Data Provider  
  
This layer is the lowest level of the application and interacts with databases, network requests, and other asynchronous data sources.  
  
## Data Provider
The data provider’s responsibility is to provide raw data. The data provider should be generic and versatile. The data provider will usually expose simple APIs to perform CRUD operations. We might have a createData, readData, updateData, and deleteData method as part of our data layer.  
  
![Data Provider](https://lh7-us.googleusercontent.com/docsz/AD_4nXd33Jey6r-YgCI8K_dZQQmrmYoDOJZIlG7WBCtcC6b2Nerhd64oOgNJSglafSoBHFalykojjubiA4SolM0U2FTEss10K5sOXzVTJW5QHPkLeD7BYX1nhgtz8KkiURxlgUtyV6A2MMEPhSl265KHQWmxzk2j?key=eXYxpY5rbSPIPtG3SWVZIQ "Data Provider")  
## Repository
The repository layer is a wrapper around one or more data providers with which the Bloc Layer communicates.  
  
![Repository ](https://lh7-us.googleusercontent.com/docsz/AD_4nXdWYcOcgj7l30kJqacHgw3Anc6brCTvX824gTn4j6lTTgxhC5i9cJ2a0EnXysfmMxgCRZrgTkLLJfMvUlTDab-DxC9zIFFSQJtNTnSR4T6iQlWn8HhpZQzBcUIN8XRJAQJ5nRcakzdImc4RnW6Us40U01by?key=eXYxpY5rbSPIPtG3SWVZIQ "Repository ")  
As you can see, our repository layer can interact with multiple data providers and perform transformations on the data before handing the result to the business logic Layer.  
  
## Business Logic Layer
The business logic layer’s responsibility is to respond to input from the presentation layer with new states. This layer can depend on one or more repositories to retrieve data needed to build up the application state.  
  
Think of the business logic layer as the bridge between the user interface (presentation layer) and the data layer. The business logic layer is notified of events/actions from the presentation layer and then communicates with repository in order to build a new state for the presentation layer to consume.  
  
![Business Logic Layer](https://lh7-us.googleusercontent.com/docsz/AD_4nXeyvhJXOud4Fm6-41Cmo4tMeTSf8uLdZDSSyw98dJ1vRv3fK_QXQ9ELgoZz-yQ5ahFd5gMXG3IYmaavWoQcoTgJSCIF6qxFgWanNavJZI8HPs6MslfMcQ3jS-RoKnjYlYe75IzLvyhYfSlFCCQlrkk-MX5B?key=eXYxpY5rbSPIPtG3SWVZIQ "Business Logic Layer")  
## Presentation Layer
The presentation layer’s responsibility is to figure out how to render itself based on one or more bloc states. In addition, it should handle user input and application lifecycle events.  
  
Most applications flows will start with a “AppStart” event which triggers the application to fetch some data to present to the user.  
  
In this scenario, the presentation layer would add an “AppStart” event.  
  
In addition, the presentation layer will have to figure out what to render on the screen based on the state from the bloc layer.  
  
![Presentation Layer](https://lh7-us.googleusercontent.com/docsz/AD_4nXfVzBPM2iXhPEk5FmbN4p_6AM50GWF6UnNA331Rgc85YZf1Y8vU4FUxBt-cuq5hwFHa0bhdLoIvuTYRIFJ5X18X404NvzRwRfeY4HrhdvkAFMVOuHgZPtxHWRcskLlWUh2PGYS9GWxgIX9_Dm95nt7TWRrL?key=eXYxpY5rbSPIPtG3SWVZIQ "Presentation Layer")  

* * *

  
_**References**_  
  
1.[Flutter documentation](https://docs.flutter.dev/data-and-backend/state-mgmt/intro)  
2.[Flutter Architecture](https://bloclibrary.dev/architecture/)
