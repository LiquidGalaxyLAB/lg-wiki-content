---
title: Automated Testing Strategies for Liquid Galaxy Applications
contributor: Rajat Kriplani
date: February 11, 2025
---

Automated testing is essential for ensuring reliability in Liquid Galaxy applications, given their dependency on SSH communication and KML interactions. This guide outlines basic testing approaches using Flutter's testing tools.

---

## **1. Unit Testing with `flutter_test`**

- **Setup:**  
  Add `flutter_test` to your `pubspec.yaml` under `dev_dependencies`:

  ```yaml
  dev_dependencies:
    flutter_test:
      sdk: flutter
  ```

- **Write Tests:**  
  Create tests in the `test/` folder. For example:

  ```dart
  import 'package:flutter_test/flutter_test.dart';
  import 'package:my_app/my_component.dart';

  void main() {
    test('Component returns expected value', () {
      final component = MyComponent();
      final result = component.someFunction();
      expect(result, expectedValue);
    });
  }
  ```

---

## **2. Mocking SSH Dependencies**

### **Using Mockito**

- **Dependencies:**  
  Add `mockito` and `build_runner` to your `dev_dependencies`:

  ```yaml
  dev_dependencies:
    mockito: ^5.0.0
    build_runner: ^2.0.0
  ```

- **Define & Generate:**  
  Create an abstract SSH service interface and annotate it for mock generation:

  ```dart
  abstract class SSHService {
    Future<String> executeCommand(String command);
  }
  ```

  Then run:
  
  ```bash
  flutter pub run build_runner build
  ```

- **Example Test:**

  ```dart
  import 'package:flutter_test/flutter_test.dart';
  import 'package:mockito/mockito.dart';
  import 'package:my_app/ssh_service.dart';
  import 'ssh_service_test.mocks.dart';

  void main() {
    test('SSH command execution returns expected result', () async {
      var mockSSH = MockSSHService();
      when(mockSSH.executeCommand('ls'))
          .thenAnswer((_) async => 'file1\nfile2\n');

      final result = await mockSSH.executeCommand('ls');
      expect(result, 'file1\nfile2\n');
    });
  }
  ```

### **Alternative(recommended for simpler setup): Using `mocktail`**

- **Setup:**  
  Add `mocktail` to your `pubspec.yaml`:

  ```yaml
  dev_dependencies:
    mocktail: ^0.3.0
  ```

- **Example Test:**

  ```dart
  import 'package:flutter_test/flutter_test.dart';
  import 'package:mocktail/mocktail.dart';
  import 'package:my_app/ssh_service.dart';

  class MockSSHService extends Mock implements SSHService {}

  void main() {
    test('Mocktail example: SSH command execution', () async {
      final sshService = MockSSHService();
      when(() => sshService.executeCommand('ls'))
          .thenAnswer((_) async => 'file1\nfile2\n');

      final result = await sshService.executeCommand('ls');
      expect(result, 'file1\nfile2\n');
    });
  }
  ```

---

Note: In actual usage, adapt test cases according to your specific Liquid Galaxy application needs and features.
