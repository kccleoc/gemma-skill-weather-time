# Weather & Time Skill

This repository provides a Gemma 4 Agent Skill that fetches the **current local time and weather** based on the user’s device location. It is designed for use with Google AI Edge Gallery.

---

## What this skill does

- Retrieves the user’s current:
  - Local time (including date and day of week)
  - Time zone and UTC offset
  - Weather conditions (temperature, conditions, humidity, wind, “feels like”, etc.)
- Returns a **plain‑text context string** that the model can read and use to answer questions naturally.
- Helps the model answer questions like:
  - “What’s the weather right now?”
  - “Is it morning or evening here?”
  - “What’s the temperature outside?”
  - “What day is it today?”

---

## Files

- `SKILL.md`  
  Human‑readable instructions that describe:
  - When to call this skill
  - How to invoke it (no parameters)
  - The format of the returned context string
  - Rules for using the data safely (never guessing, always using the tool output)

- `index.html`  
  The actual Edge Gallery skill definition:
  - Declares the `Weather & Time` skill metadata
  - Defines a single tool: `get_weather_and_time`
  - Specifies an empty JSON input schema (the tool takes no parameters)
  - Embeds the same usage guidance from `SKILL.md` as visible documentation

---

## Tool definition

The skill exposes one tool:

- **Name:** `get_weather_and_time`  
- **Description:** Fetches the current local time and weather for the user’s device location.  
- **Input schema:**  
  - Type: `object`  
  - Properties: none  
  - Required: `[]` (no fields)  

Call it with an empty JSON object:

```json
{}
```

The host app is responsible for resolving the user’s location and returning the context string.

---

## Example response

The tool returns a plain‑text block, for example:

```text
Current time: Wednesday, April 9 2026, 3:42 PM (JST, UTC+9)
Location: Tokyo, Japan
Weather: 18°C (64°F), Partly Cloudy
Humidity: 62% | Wind: 12 km/h NE
Feels like: 16°C (61°F)
```

---

## How the model should use this skill

1. **Always call the tool first** for any question about:
   - Current time, hour, or minute
   - Today’s date, day of the week, or month
   - Current weather or temperature
   - Time‑of‑day concepts (morning, afternoon, evening, night)

2. **Read the returned context string** and answer the user’s question directly, using natural conversational language.

3. **Do not guess**:
   - Never fabricate time or weather.
   - Never claim a knowledge cutoff prevents you from knowing; rely on the tool output instead.

4. **Handle errors gracefully**:
   - If the tool fails or returns an error, explain that location access may be required and suggest enabling it.

---

## Using this skill in Edge Gallery

1. Host this repository on GitHub (or any static hosting).
2. Use the **raw** URL of `index.html` when adding a skill by URL in Google AI Edge Gallery.
3. Ensure your Edge Gallery client version supports custom skills and the SKILL.md/index.html format.
