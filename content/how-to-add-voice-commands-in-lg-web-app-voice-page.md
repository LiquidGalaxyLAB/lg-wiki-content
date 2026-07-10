---
title: How to Add Voice Commands in LG Web App Voice Page
contributor: Vedang Lokhande
date: 2025-03-04T05:09:05.741+00:00
---

# How to Add Voice Commands in LG Web App Voice Page

This guide explains how to implement voice command functionality in the LG Web App, enhancing the user experience with speech recognition. The implementation involves changes in both the frontend and backend of the application.

## Frontend Implementation

### Modifying `js/components/voice.js`

1. **Language Selection for Speech Recognition**
   - The voice recognition system can support multiple languages by listening to the `change` event on the language selector dropdown.

```js
const languageSelect = this.shadowRoot.getElementById("languageSelect");
languageSelect.addEventListener("change", (event) => {
  switch(event.target.value) {
    case "en":
      recognition.lang = "en";
      break;
    case "hi":
      recognition.lang = "hi";
      break;
    case "es":
      recognition.lang = "es";
      break;
    default:
      recognition.lang = "en";
  }
  console.log("Speech recognition language set to:", recognition.lang);
});
```

2. **Speech Recognition Configuration**
   - The Web Speech API is used to configure the speech recognition service.

```js
const recognition = new SpeechRecognition();
let isRecognizing = false;
recognition.lang = languageSelect.value;
recognition.interimResults = false;
recognition.maxAlternatives = 1;
recognition.continuous = false;

const updateRecognitionLanguage = () => {
  recognition.lang = languageSelect.value;
  console.log("Speech recognition language updated to:", recognition.lang);
};

languageSelect.addEventListener("change", updateRecognitionLanguage);
updateRecognitionLanguage();
```

3. **Microphone Button Interaction**
   - Clicking the microphone button starts and stops speech recognition.

```js
micButton.addEventListener("click", () => {
  if (isRecognizing) {
    messageEl.textContent = "";
    isRecognizing = false;
    recognition.stop();
    removeAnimations();
  } else {
    messageEl.textContent = "Start Speaking...";
    recognition.start();
    isRecognizing = true;
    micButton.classList.add("ripple");
    voiceAnimation.classList.add("animate");
  }
});
```

4. **Speech Recognition Result Handling**

```js
recognition.onresult = (event) => {
  const transcript = event.results[0][0].transcript.trim();
  const selectedLanguage = languageSelect.value;
  speech(transcript.toLowerCase(), selectedLanguage);
  isRecognizing = false;
  messageEl.textContent = transcript;
  removeAnimations();
};
```

### Adding New Voice Commands

New voice commands can be added in `js/utils/speech.js`:

```js
export const speech = async (words, selectedLanguage) => {
  let translatedWords = words;
  const lowerWords = translatedWords.toLowerCase();
  switch (true) {
    case lowerWords.includes("clean") && lowerWords.includes("logos"):
      await cleanlogo();
      break;
    case lowerWords.includes("clean") && lowerWords.includes("balloon"):
      await cleanballoon();
      break;
  }
};
```

## Backend Implementation

### Service Layer

Modify the `src/services/lgConnectionService.js` to define the backend logic for new commands:

```js
export const goToCityService = async (ip, port, username, password, cityName) => {
  const client = new Client();
  try {
    // Add backend logic here
  } catch (error) {
    console.error(error);
  }
};
```

### Controller Layer

In `src/controllers/lgConnection.controllers.js`, handle API requests:

```js
goToCity = async (req, res) => {
  const { ip, port, username, password, cityName } = req.body;
  try {
    const response = await goToCityService(ip, port, username, password, cityName);
    res.status(200).json(response);
  } catch (error) {
    res.status(500).send("Error processing command");
  }
};
```

### Routing Layer

Add the route in `src/routers/lgConnection.router.js`:

```js
import { goToCity } from "../controllers/lgConnection.controllers.js";
router.post("/goToCity", goToCity);
```

By following this guide, developers can easily implement new voice commands into the LG Web App while supporting multiple languages and enhancing user experience with speech recognition.


