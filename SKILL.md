-----

## name: weather-and-time
description: Provides the current local date, time, and weather conditions for the user’s location. Use this skill whenever the user asks what time it is, what day it is, what the weather is like, if it is hot or cold, or any question that requires knowing the current time or weather.

# Weather & Time Skill

## Purpose

You have access to a live tool that fetches the user’s current local time and weather. Always use it before answering any question about:

- The current time, hour, or minute
- Today’s date, day of the week, or month
- The current weather, temperature, or conditions
- Whether it is morning, afternoon, evening, or night

## How to Invoke the Skill

Call the skill with no parameters. The app will automatically detect the device location.

Pass this exact JSON to the skill:

```json
{}
```

## What You Receive Back

The skill returns a plain-text context string, for example:

```
Current time: Wednesday, April 9 2026, 3:42 PM (JST, UTC+9)
Location: Tokyo, Japan
Weather: 18°C (64°F), Partly Cloudy
Humidity: 62% | Wind: 12 km/h NE
Feels like: 16°C (61°F)
```

## How to Answer

- Read the context string carefully.
- Answer the user’s question directly using the data provided.
- Do NOT say you cannot access real-time data. You have the data from the skill.
- Use natural, conversational language. For example:
  - “It’s 3:42 PM on Wednesday, April 9th.”
  - “It’s 18°C and partly cloudy in your area right now.”
  - “Good afternoon! It’s currently mid-afternoon and a bit chilly at 18°C.”
- If the user asks a time-of-day concept like “is it morning?”, reason from the hour in the context.
- Always mention the timezone if the user might be curious.

## Important Rules

- Never guess or make up a time or weather. Always wait for the skill result.
- Never say your knowledge cutoff prevents you from knowing the time — the skill solves this.
- If the skill returns an error, tell the user politely that location access may be needed and suggest enabling it.
