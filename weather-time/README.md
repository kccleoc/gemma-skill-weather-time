# Weather & Time Skill (Manual Location)

This repository provides a Gemma 4 Agent Skill that fetches the **current local time and weather** for a **user‑provided location string** (for example, “Taipei, Taiwan”). It is designed for use with Google AI Edge Gallery and does **not** require device location permissions.

---

## What this skill does

- Retrieves the current:
  - Local time (including date and day of week) for a given place
  - Time zone and UTC offset
  - Weather conditions (temperature, conditions, humidity, wind, “feels like”, etc.)
- Returns a **plain‑text context string** that the model can read and use to answer questions naturally.
- Helps the model answer questions like:
  - “What’s the weather right now in Taipei?”
  - “Is it morning or evening in Tokyo?”
  - “What’s the temperature in New York City?”
  - “What day is it today in London?”

The user always specifies the location in text; the skill never reads device GPS.

---

## Files

- `SKILL.md`  
  Human‑readable instructions that describe:
  - When to call this skill
  - How to ask the user for a location if none is provided
  - How to invoke the tool with a `location` field
  - The format of the returned context string
  - Rules for using the data safely (never guessing, always using the tool output)

- `index.html`  
  The Edge Gallery skill definition:
  - Declares the `Weather & Time (manual location)` skill metadata
  - Defines a single tool: `get_weather_and_time`
  - Specifies a JSON input schema with one required string field: `location`
  - Embeds the same usage guidance from `SKILL.md` as visible documentation

---

## Tool definition

The skill exposes one tool:

- **Name:** `get_weather_and_time`  
- **Description:** Fetches the current local time and weather for a user‑provided location string, such as a city name.  
- **Input schema:**

```json
{
  "type": "object",
  "properties": {
    "location": {
      "type": "string",
      "description": "City or location name, e.g. 'Taipei, Taiwan' or 'Tokyo, Japan'."
    }
  },
  "required": ["location"]
}
```

The model must always supply a `location` string when calling this tool.

---

## Example tool calls

Examples of valid inputs:

```json
{ "location": "Taipei, Taiwan" }
{ "location": "Tokyo, Japan" }
{ "location": "New York City, USA" }
{ "location": "London, United Kingdom" }
```

---

## Example response

The tool returns a plain‑text block, for example:

```text
Location: Tokyo, Japan
Current time: Wednesday, April 9 2026, 3:42 PM (JST, UTC+9)
Weather: 18°C (64°F), Partly Cloudy
Humidity: 62% | Wind: 12 km/h NE
Feels like: 16°C (61°F)
```

---

## How the model should use this skill

1. **Check for a location in the user’s message.**  
   - If the user already mentions a place (e.g. “in Taipei”), extract that string.  
   - If no place is given, ask a clarifying question:  
     “Which city or location are you interested in?”

2. **Call the tool with the location string** using the schema above.

3. **Read the returned context string** and answer the user’s question directly, using natural conversational language.

4. **Do not guess**:
   - Never fabricate time or weather.
   - Never claim a knowledge cutoff prevents you from knowing; rely on the tool output instead.

5. **Handle errors gracefully**:
   - If the tool fails or the location is not recognized, explain this and ask the user to try a more specific city or region name.

---

## Using this skill in Edge Gallery

1. Host this repository on GitHub (or any static hosting).
2. Use the **raw** URL of `index.html` when adding a skill by URL in Google AI Edge Gallery.
3. Ensure your Edge Gallery client version supports custom skills and the SKILL.md / `index.html` format.
