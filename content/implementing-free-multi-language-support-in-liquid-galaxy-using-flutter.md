---
title: Implementing Free Multi-Language Support in Liquid Galaxy Using Flutter
contributor: Jaivardhan Shukla
date: February 13, 2025
---

# Implementing Free Multi-Language Support in Liquid Galaxy Using Flutter

## Introduction

This article demonstrates how to add multi-language speech functionality to Liquid Galaxy. The technology enables users to: 
- Speak commands in their regional language 
- Convert speech to text utilizing the device's native capabilities.
- Translate text into English for processing.
- Execute commands in Liquid Galaxy.
- Get voice feedback in their regional tongue.

## Prerequisites

* Flutter development environment
* Liquid Galaxy setup
* Basic understanding of *async* programming in Dart
* Device with speech recognition capabilities

## Required Dependencies

Add these to your `pubspec.yaml`:

```yaml
dependencies:
  flutter:
    sdk: flutter
  speech_to_text: ^X.X.X
  translator: ^X.X.X
  flutter_tts: ^X.X.X
```

## Implementation Steps

### 1. Voice Input Setup (Speech-to-Text)

```dart
import 'package:speech_to_text/speech_to_text.dart' as stt;

class VoiceInputHandler {
  final stt.SpeechToText _speech = stt.SpeechToText();

  Future<String> listenToVoice(String languageCode) async {
    bool available = await _speech.initialize();
    String recognizedText = '';
    
    if (available) {
      await _speech.listen(
        onResult: (result) {
          recognizedText = result.recognizedWords;
        },
        localeId: languageCode, // e.g., 'hi-IN' for Hindi
      );
    }
    return recognizedText;
  }
}
```

### 2. Translation Implementation

```dart
import 'package:translator/translator.dart';

class FreeTranslator {
  final translator = GoogleTranslator();

  Future<String> translateToEnglish(String text, String from) async {
    try {
      var translation = await translator.translate(text, 
        from: from,
        to: 'en'
      );
      return translation.text;
    } catch (e) {
      print('Translation error: $e');
      return '';
    }
  }
}
```

### 3. Text-to-Speech Implementation

```dart
import 'package:flutter_tts/flutter_tts.dart';

class TextToSpeech {
  final FlutterTts flutterTts = FlutterTts();

  Future<void> speak(String text, String languageCode) async {
    await flutterTts.setLanguage(languageCode);
    await flutterTts.speak(text);
  }
}
```

### Language Code Implementation

```dart
final Map<String, String> languageCodes = {
  'English': 'en-US',
  'Spanish': 'es-ES’,
  'French': 'fr-FR',
  'German': 'de-DE',
  'Chinese (Mandarin)': 'zh-CN',
  'Russian': 'ru-RU',
  'Hindi': 'hi-IN',
  // Add more as needed
};

```

## Error Handling

```dart
try {
  await handler.processVoiceCommand(languageCode);
} catch (e) {
  if (e is LanguageNotSupportedException) {
    // Fall back to English
    await handler.processVoiceCommand('en-US');
  }
}
```

## Limitations and Considerations

1. **Device Dependencies**
   * Speech recognition quality varies by device
   * Language support depends on installed language packs
   * Internet required for translation

2. **Performance**
   * Translation has rate limits
   * Voice recognition may be slower than cloud solutions
   * TTS quality varies by device

3. **Reliability**
   * Network dependency for translation
   * Device-specific speech recognition accuracy
   * Limited error recovery options

## Best Practices

1. Always check language availability before use
2. Implement proper error handling
3. Provide visual feedback during processing
4. Test with various accents and dialects
5. Include fallback options for unsupported languages

## Future Enhancements

* Implement offline translation capabilities
* Add support for custom commands
* Improve error handling and recovery
* Add support for more regional languages
* Implement command confirmation system

## Conclusion

This implementation provides an efficient way to add multi-language support to Liquid Galaxy. While it has some limitations compared to cloud solutions, it offers good functionality for most use cases and supports a wide range of languages.

