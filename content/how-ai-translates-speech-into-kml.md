---
title: How AI translates Speech into KML
contributor: Saumya Bhattacharya
date: February 12, 2026
---

## How AI translates Speech into KML
-------------------------------------

Modern AI systems are no longer confined to answering questions, they can control environments as well.Imagine standing before a Liquid Galaxy and saying, “Take me to the Eiffel Tower” and instantly, the screens glide across the globe and zoom into Paris. While this might feel like magic, it is actually a pipeline of Natural Language Processing and dynamic code generation. The complete translation pipeline consists of six interconnected stages that transform user intent into visual output:

![AI Speech to KML pipeline](https://raw.githubusercontent.com/Saumya-28/lg_wiki_images/refs/heads/main/Ai_speech_to_kml_img1.png)

The speech capture phase uses the speech\_to\_text Flutter package which provides a cross-platform interface to native speech recognition APIs (iOS Speech Framework, Android Speech Recognizer).

```dart
// Initialize and start speech recognition
SpeechToText _speechToText = SpeechToText();

Future<void> startListening() async {
  await _speechToText.initialize();
  await _speechToText.listen(
    onResult: (result) {
      if (result.finalResult) {
        processWithAI(result.recognizedWords);
      }
    },
  );
}
```

The integration with Gemini is accomplished through Google's official google\_generative\_ai package, which provides a Dart-native interface to the Gemini API.

We use Google Gemini API with two-stage prompting: the first prompt generates the response shown to the user and second for extracting locations for visualization:

![AI Speech ](https://raw.githubusercontent.com/Saumya-28/lg_wiki_images/refs/heads/main/AI_speech_to_kml_img3.png)

```dart
// Google Gemini API with two-stage prompting

final model = GenerativeModel(model: 'gemini-pro', apiKey: apiKey);

// Stage 1: Generate conversational response
Future<String> generateResponse(String query) async {
  final response = await model.generateContent([Content.text(query)]);
  return response.text ?? '';
}

// Stage 2: Extract geographic entities
Future<List<String>> extractLocations(String query) async {
  final prompt = "Extract geographic locations from: \"$query\"";
  final response = await model.generateContent([Content.text(prompt)]);
  return response.text?.split(',').map((e) => e.trim()).toList() ?? [];
}
```

With a validated list of locations in, the system now orchestrates the actual navigation sequence. For each location in the list, an SSH command is constructed and transmitted to the Liquid Galaxy system. The locatePlace function is called with each location string, which generates the appropriate search command in KML format.This involves several critical steps: splitting the response into individual location entries, trimming whitespace, removing duplicates, and lastly validating that each entry is suitable for use with Google Earth's search functionality.

​​// KML Generation

```dart
class KMLMakers {
  static String lookAtLinear(double lat, double lng, double zoom, double tilt, double bearing) =>
      '<LookAt><longitude>$lng</longitude><latitude>$lat</latitude>'
      '<range>$zoom</range><tilt>$tilt</tilt><heading>$bearing</heading></LookAt>';
}

class BalloonMakers {
  static String dashboardBalloon({String cityName = "Unknown"}) =>
      '''<kml><Document><Style id="info">
      <BalloonStyle><text><h1>$cityName</h1></text></BalloonStyle>
      </Style><Placemark><styleUrl>#info</styleUrl></Placemark></Document></kml>''';
}
```

Post this process,the LG system runs Google Earth in a special query mode where commands can be sent via the /tmp/query.txt file- this file is monitored continuously by Google Earth through a file watching mechanism. Any change to this file, whether new content or modification of existing content, triggers Google Earth to read the file, parse its contents, and execute the command. This file-based communication pattern is simple but effective, requiring no complex inter-process communication protocols. The command format follows Google Earth's query syntax conventions. Commands begin with a keyword (like "search=", "flytoview=", "planet=", or "playtour=") followed by the relevant data. This syntax is processed by Google Earth's command parser, which routes each command type to the appropriate subsystem for execution.

```dart
// SSH Command Transmission

// Establish connection
Future<bool> connectToLG() async {
  final socket = await SSHSocket.connect(ipAddress, port);
  _sshClient = SSHClient(socket, username: username, onPasswordRequest: () => password);
  return true;
}

// Execute navigation
Future<void> flyTo(double lat, double lng, double zoom, double tilt, double bearing) async {
  final kml = KMLMakers.lookAtLinear(lat, lng, zoom, tilt, bearing);
  await _sshClient?.run('echo "flytoview=$kml" > /tmp/query.txt');
}

// Render on slave screens
Future<void> renderInSlave(int slaveNo, String kml) async {
  await _sshClient?.run("echo '$kml' > /var/www/html/kml/slave_$slaveNo.kml");
}
```

When a search command is written to this file, Google Earth automatically searches for the location and navigates to it. Finally, the communication between the Flutter application and the Liquid Galaxy rigs occurs over standard SSH protocol on TCP port 22. Commands are transmitted as shell script executions that modify specific files in the /tmp/ and /var/www/html/kml/ directories. Google Earth running on the LG rigs continuously monitors these locations for changes and immediately renders any new or updated KML content, creating the illusion of real-time responsiveness to user commands.
