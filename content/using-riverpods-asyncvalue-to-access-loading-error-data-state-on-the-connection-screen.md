---
title: Using riverpod’s AsyncValue to access loading, error, data state on the connection screen.
contributor: Shahzeel Ansari
date: 2024-06-13T14:26:18.976+00:00
---

  
Riverpod offers AsyncValue class which has three states which are loading, error and data. Which can be accessed by AsyncData,ASyncValue.loading(),AsyncValue.error(),  
  
Dependencies: flutter\_riverpod, riverpod\_annotation, riverpod\_generator, build\_runner  
  
## Code:

```terminal
@Riverpod(keepAlive: true)

/// [keepAlive] is set to true to cache the data for the current session
class ConnectToLG extends _$ConnectToLG {
  @override
  //build method which returns initial value of the provider
  Future<bool> build() async {
    return false;
  }


  Future<bool> connect(
      String userName, String host, int port, String password) async {
    try {
      //extract loading state while performing asynchronous tasks
      state = const AsyncValue.loading();
      ref.read(clientProvider.notifier).state = SSHClient(
          await SSHSocket.connect(host, port,
              timeout: const Duration(seconds: 5)),
          username: userName,
          onPasswordRequest: () => password,
          );


      ///update the [state] if result is true
      //this sets the return value to true which was initially false
      state = const AsyncData(true);
      ref.read(isConnectedProvider.notifier).setState(true);
      return true;
    } on SocketException catch (e) {
      ///return state as false on error
      state = const AsyncValue.data(false);
      ref.read(isConnectedProvider.notifier).setState(false);
      return false;
    }
  }
}
```

  
Presentation side: Watch the provider

```dart
final connectToLgProvider = ref.watch(connectToLGProvider);
```

  
Now access the states using .when()

```dart
Center(
    child: connectToLgProvider.when(
        data: (data) => Text( isConnected ? 
     'Disconnect' : 'Connect'),
error: (e, stc) => Text(e.toString()),loading:()=>CircularProgressIndicator(color:Colors.white)
```

  
![task_3_gif](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEioaOwysPwacZ6CHDdivLUvwvc6sXgxd3MVK7QF0aRk2i6ndAXq6BHH32MIJysgl2aN9tKvkk9Rp2p1OnD2cv_iBSELsAmKUzqyUXs54KceDE8ZU8BoE9qKA0JZDKcAtfZGMxk2RUY8Nxm6wQbn-pHb44dcHCWiTIHI3YwEZZZOhJkdc0_UK7uKxpbwwR6x/s320/task_3_gif.gif "task_3_gif")
