# genius-devcamp-2025-ohai-challenge
Genius Devcamp Document Processing Challenge from Ohai

# Challenge
Create a program that converts images into events, reminders, and todo items. The output of your program should be a human readable listing of the extracted events, reminders, and todo items along with a kind, helpful, and upbeat message to the user 

# Tip
Use the Genius DevCamp API to feed your system prompt with helpful guidelines on how to read different types of documents

# Requirements
## General
1. Use an LLM
2. Support .png and .jpg formats
3. Test with the provided documents. You can also use your own documents
4. Respect any additional information that the user gives in their prompt. i.e. "Ignore events that occur on Wednesdays"

## Program Input
1. user prompt (string)
2. 1 or more file pathes to the documents that will be processed (array of strings)

## Program Output
1. Human readable listing of the extracted events, reminders, and todos along with a kind, helpful, and upbeat message to the user (string)
Json in the following format


2. The following json

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "properties": {
    "response": {
      "type": "string",
      "description": "This is the response to the user."
    },
    "events": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "startTime": {
            "type": "string",
            "format": "date-time",
            "description": "Event start time in ISO 8601 format."
          },
          "endTime": {
            "type": "string",
            "format": "date-time",
            "description": "Event end time in ISO 8601 format."
          },
          "all_day": {
            "type": "boolean",
            "description": "Indicates if the event lasts all day."
          },
          "title": {
            "type": "string",
            "description": "Name of the event."
          },
          "description": {
            "type": "string",
            "description": "Optional description of the event.",
            "nullable": true
          },
          "location": {
            "type": "string",
            "description": "Optional location of the event.",
            "nullable": true
          },
          "rrules": {
            "type": "array",
            "items": {
              "type": "string"
            },
            "description": "Optional array of recurrence rules in RFC5545 format.",
            "nullable": true
          }
        },
        "required": ["startTime", "endTime", "all_day", "title"]
      }
    },
    "Reminders": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "time": {
            "type": "string",
            "format": "date-time",
            "description": "Reminder time in ISO 8601 format."
          },
          "title": {
            "type": "string",
            "description": "Title of the reminder."
          },
          "rrules": {
            "type": "array",
            "items": {
              "type": "string"
            },
            "description": "Optional array of recurrence rules in RFC5545 format.",
            "nullable": true
          }
        },
        "required": ["time", "title"]
      }
    },
    "todos": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "title": {
            "type": "string",
            "description": "Title of the to-do item."
          }
        },
        "required": ["title"]
      }
    }
  },
  "required": ["response", "events", "Reminders", "todos"]
}
```


# Submission Requirements
1. Your system prompt

## Judging Criteria
***Accuracy***
Extract all events, reminders, and todos with their relevant information.  This is the most important objective 

***Performance***
The fewer the tokens the better. Don’t sacrifice accuracy for performance!  We will use [this](https://platform.openai.com/tokenizer) counter  

***Tone***
The AI should answer in a kind and helpful tone. 

# Definitions
## Event
Entity that appears on a user’s calendar that has a start and end time, or is taking place all day. Can reoccur.  If the entity in the document specifically mentions a calendar but no end time is provided, assume 1 hour duration.

***Required***
* Title
* Start Time / End Time (or all day)

***Optional***
* Description
* Location
* RRules (as specified by RFC5545)

***Examples***
* Birthday
* Work Meeting from 2-3 pm

## Reminder
Entity containing a message for a user that has a specific start time, but not end time and not all day. Can reoccur.

**Required**
* Title
* Start Time (no end time)
* Message to the user

**Optional**
* RRules (as specified by RFC5545)

**Examples**
* Water plants at 3pm

## Todo Item
Entity that requires something to be done but not at a specific time. Cannot reoccur

***Required***
* Title

***Examples***
* Do 10 Pushups
* Grocery list
