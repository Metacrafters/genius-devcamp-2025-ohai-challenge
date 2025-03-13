# genius-devcamp-2025-ohai-challenge
Genius Devcamp Document Processing Challenge from Ohai

# Challenge
Create a program that converts images (.jpg and .png) into events, reminders, and todo items. The output of your program should be a human readable listing of the extracted events, reminders, and todo items along with a kind, helpful, and upbeat message to the user 

# Tip
Use the Genius DevCamp API to feed your system prompt with helpful guidelines on how to read different types of documents

# Requirements
## General
1. Use an LLM
2. Test with the provided documents. You can also use your own documents

## Program Input
1. user prompt (string)
2. 1 or more file pathes to the documents that will be processed (array of strings)

## Program Output
1. Human readable listing of the extracted events, reminders, and todos along with a kind, helpful, and upbeat message to the user (string)

# Submission Requirements
1. Your system prompt

## Judging Criteria
***Accuracy***
Extract all events, reminders, and todos with their relevant information.  This is the most important objective (75%)

***Performance***
The fewer the tokens the better. Don’t sacrifice accuracy for performance! (10%)

***Tone***
The AI should answer in a kind and helpful tone. (15%)

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
