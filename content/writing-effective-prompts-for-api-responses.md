---
title: Writing Effective Prompts for API Responses
contributor: Rohit Kumar
date: March 4, 2025
---

# Introduction

Well-structured prompts help APIs generate accurate JSON responses. A clear prompt ensures correct formatting and meaningful data.

## Key Elements of a Good Prompt

- **Clear Instructions** – Define what data is needed.
- **Expected Output Format** – Specify JSON structure.
- **Detailed Descriptions** – Guide content generation.
- **Consistency** – Use fixed attribute names.

## Example Prompt

Create an interlinked story about ten different cities. Provide the response in structured JSON format:

```json
{
  "Title": "Story title",
  "Places": [
    {
      "Name": "Place name",
      "Description": "Detailed description",
      "Address": "Full address",
      "City": "City name"
    }
  ]
}
```

Ensure JSON attribute names match exactly. No Markdown is needed.

## A Prompt in Action

Removing various unwanted elements and cleaning the response.

## Why This Works

- **Clear Formatting** – Defines structure.
- **Rich Content** – Encourages detailed responses.
- **Consistency** – Ensures correct attributes for easy parsing.

## Best Practices

- Be specific.
- Define JSON output clearly.
- Provide length expectations.
- Use examples when possible.


