---
title: Adding Semantics in Flutter Apps to enhance Accessibility
contributor: Aayush Kumar
date: March 17, 2025
---

# Adding Semantics in Flutter Apps

Semantics in Flutter apps add meaning to UI elements, enabling accessibility features like screen readers to interpret and convey information to users with disabilities.

## Some Key Concepts:
- **Semantic Node**: A node in the semantic tree that represents a piece of user interface.
- **Semantic Properties**: Attributes that describe the meaning, function, or state of a widget.
- **Semantic Widgets**: A Flutter widget used to annotate the widget tree with semantic information.

## 1. Identify the Widget Needing Semantics
Determine which widgets convey important information or enable interaction. Focus on:

- **Interactive elements**: Buttons, text fields, sliders, switches.
- **Informative widgets**: Images with descriptions, dynamic text.
- **Avoid semantics** on decorative elements, unless they add functional meaning.

## 2. Implementing Semantics in an App

### A. Adding Basic Semantics
Use the `Semantics` widget to provide labels and hints to interactive elements:

```dart
Semantics(
  label: 'Submit Button',
  hint: 'Double tap to submit the form',
  child: ElevatedButton(
    onPressed: () {
    //Submit form logic
},
    child: Text('Submit'),
  ),
)
```

Here, the `ElevatedButton` is wrapped with `Semantics`, offering a meaningful label and hint to screen readers.
 
### B. Adding Custom Semantics Actions
Custom semantic actions enable screen readers to recognize and perform specific user-defined actions:

```dart
Semantics(
  customSemanticsActions: {
    CustomSemanticsAction( label: 'Custom action' ) : () {
      // Custom action logic
}
  child: MyCustomWidget( ) ,
)
```

### C.  Excluding Decorative Elements
Use `ExcludeSemantics` to remove unnecessary elements from the accessibility tree:

```dart
import 'package:flutter/material.dart';

Widget buildExcludedSemanticsImage() {
  return Column(
    mainAxisAlignment: MainAxisAlignment.center,
    children: [
      const Text(
        'This image is visible but ignored by screen readers:',
      ),
      const SizedBox(height: 10),
      const ExcludeSemantics(
        excluding: true,
        child: Image.asset('assets/decorative_image.png'),
      ),
    ],
  );
}
```

This prevents screen readers from announcing purely decorative elements.

### D. Merging Semantics for Better Understanding
When multiple widgets represent a single logical element, use `MergeSemantics`:

```dart
MergeSemantics(
  child: Column(
    children: [
      Text('Username'),
      TextField(),
    ],
  ),
)
```

This example groups the `Text` label and `TextField` into a single logical element, improving accessibility for screen readers.

## 3. Use Key Semantics Properties
- `label`: A concise description of the widget's purpose.
- `hint`: Provides additional context or instructions.
- `value`: Represents the current value of the widget (e.g., text field content).
- `button`: Indicates that the widget acts like a button.
- `onTap`, `onLongPress`, etc.: Define actions associated with the widget.
- `checked`: For checkboxes or radio buttons, indicates their state.
- `selected`: Indicates if the widget is currently selected.
- `enabled`: Specifies whether the widget is interactive.
- `hidden`: Hides the widget from accessibility services.

### Example:

#### 1. Creating a Custom Semantic:

```dart
import 'package:flutter/material.dart';

typedef VotdCallback = void Function();

Widget _buildSemanticButton({
  required VoidCallback onPressed,
  required IconData icon,
  String? label,
  String? hint,
}) {
  return Semantics(
    button: true,
    enabled: true,
    label: label,
    hint: hint,
    onTap: onPressed,
    child: Tooltip(
      message: label ?? '', // Handle null label
      child: IconButton(
        onPressed: onPressed,
        icon: Icon(icon),
        tooltip: label, 
      ),
    ),
  );
}
```

#### 2. Using the Semantic Button Widget:

```dart
import 'package:flutter/material.dart';

class SemanticButtonExample extends StatefulWidget {
  const SemanticButtonExample({Key? key}) : super(key: key);

  @override
  State<SemanticButtonExample> createState() => _SemanticButtonExampleState();
}

class _SemanticButtonExampleState extends State<SemanticButtonExample> {
  void _editItem(int index) {
    // Your edit item logic here
    print('Editing item $index');
  }

  Widget _buildSemanticButton({
    required VoidCallback onPressed,
    required IconData icon,
    String? label,
    String? hint,
  }) {
    return Semantics(
      button: true,
      enabled: true,
      label: label,
      hint: hint,
      onTap: onPressed,
      child: Tooltip(
        message: label ?? '',
        child: IconButton(
          onPressed: onPressed,
          icon: Icon(icon),
          tooltip: label,
        ),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Semantic Button Example')),
      body: Center(
        child: _buildSemanticButton(
          onPressed: () => _editItem(1),
          icon: Icons.edit,
          label: 'Edit item 1',
          hint: 'Edit the 1st item in the shopping list',
        ),
      ),
    );
  }
}
```

## Additional Tips
- **Use meaningful labels**: Avoid redundant words like "image of" or "button for" as screen readers already announce the widget type.
- **Test accessibility**: Use Flutter’s accessibility tools or screen readers to verify semantics.
- **Combine multiple semantics**: For complex widgets, structure semantics to cover all elements effectively.

