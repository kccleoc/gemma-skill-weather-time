---
name: Weather & Time (manual location)
description: Fetch the current weather and local time for a user-provided location.
author: Neo
tags:
  - weather
  - time
  - location
---

# Weather & Time Skill (Manual Location)

## Purpose

You have access to a live tool that fetches the current local time and weather for a location the user provides in text.

Always use it before answering any question about:

- The current time, hour, or minute in a specific place
- Today’s date, day of the week, or month in that place
- The current weather, temperature, or conditions there
- Whether it is morning, afternoon, evening, or night there

## How to Invoke the Skill

If the user already mentioned a place, extract it and call the skill.

If the user did not mention a place, ask:
“Which city or location do you want me to check?”

Pass this JSON to the skill:

```json
{
  "location": "<USER_LOCATION_STRING>"
}
```

Examples:

```json
{ "location": "Hong Kong" }
{ "location": "Taipei, Taiwan" }
{ "location": "Tokyo, Japan" }
```

## What You Receive Back

The skill returns a plain-text context string, for example:

```text
Location: Hong Kong
Current time: Wednesday, April 8 2026, 2:58 PM (HKT, UTC+8)
Time of day: afternoon
Weather: 26°C (79°F), Partly Cloudy
Feels like: 29°C (84°F)
Humidity: 74%
Wind: 18 km/h E
```

## How to Answer

- Read the context string carefully.
- Answer the user’s question directly using the data provided.
- Do NOT say you cannot access real-time data. You have the data from the skill.
- Use natural, conversational language.
- If the user asks a time-of-day concept like “is it morning?”, reason from the hour in the context.
- Mention the timezone when it is useful.

## Important Rules

- Never guess or make up a time or weather. Always wait for the skill result.
- Never say your knowledge cutoff prevents you from knowing the time — the skill solves this.
- If the skill returns an error, tell the user politely that the location may not have been recognized and suggest trying a more specific place name.
