---
title: Speech To Text in Flutter
contributor: Vivek Maurya
date: 2024-06-11T15:01:50.856+00:00
---

Speech-to-text functionality in Flutter can be implemented using various plugins that leverage the underlying native capabilities of the device.\
\
By using this functionality we can convert short phrases or voice commands to text form.\
\
Flutter, being a versatile UI toolkit, allows developers to integrate speech-to-text features seamlessly into their applications.\
\
``` ```
***
\
***How to implement speech-to-text functionality in Flutter:***\
\
**Adding required dependencies:**
```dart
dependencies:
  speech_to_text: ^6.6.1
```
\
**Add the required permission to <project root>/android/app/src/main/AndroidManifest.xml for android :**
```dart
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.INTERNET"/>
<queries>
    <intent>
        <action android:name="android.speech.RecognitionService" />
    </intent>
</queries>
```
\
**Start Listening :**
```dart
final SpeechToText _speechToText = SpeechToText();
bool _speechEnabled = false;
String _lastWords = "";

final TextEditingController _textController = TextEditingController();
```
\
Added a SpeechToText object, a boolean variable to check if SpeechToText is listening or not, a String variable to get the converted text and a TextEditingController for the TextField which will show the converted text in it.\
\
**Write init, start, stop and result functions**
```terminal
void _initSpeech() async {
    _speechEnabled = await _speechToText.initialize();
  }

  /// Each time to start a speech recognition session
  void _startListening() async {
    await _speechToText.listen(
      onResult: _onSpeechResult,
      listenFor: const Duration(seconds: 30),
      localeId: "en_En",
      cancelOnError: false,
      partialResults: false,
      listenMode: ListenMode.confirmation,
    );
    setState(() {});
  }

  /// Manually stop the active speech recognition session
  /// Note that there are also timeouts that each platform enforces
  /// and the SpeechToText plugin supports setting timeouts on the
  /// listen method.
  void _stopListening() async {
    await _speechToText.stop();
    setState(() {});
  }

  /// This is the callback that the SpeechToText plugin calls when
  /// the platform returns recognized words.
  void _onSpeechResult(SpeechRecognitionResult result) {
    setState(() {
      _lastWords = "$_lastWords${result.recognizedWords} ";
      _textController.text = _lastWords;
    });
  }
```
\
→ _initSpeech() : to initialise\
→ _speechToText which will return a boolean value. If it starts listening without any error it will return true so _speechEnabled will be true.\
\
→ _startListening() : to start listening.
 In this function we will call _onSpeechResult function and we can determine listening duration, language and if we want to get the converted text partially or after finishing speech we have to set it to false.\
\
→ _stopListening() : to stop listening.\
	In this function we have used _speechToText.stop() that will immediately stop the listening service if called upon.\
\
→ _onSpeechResult() : to get the converted text. In this function we will append the new converted text to the texts that were converted before so we won’t lose these texts when we want to speak more than one time.\
\
**Calling these functions :**\
\
In initState we will check if it started listening or not. If not we will call _initSpeech() function to initialize _speechToText() object.
```dart
 @override
  void initState() {
    super.initState();
    if (!_speechEnabled) {
      _initSpeech();
    }
  }
```
\
And on clicking on the microphone button in UI (which we can add with on pressed set on _startListening), _startListening() will be called and We can start speaking.\

