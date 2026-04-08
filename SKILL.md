---
name: weather-time-manual
description: Fetch the current weather and local time for a user-provided location.
---

# Weather & Time

## Instructions

Use this skill for questions about the current weather, current time, date, timezone, or time of day in a specific place.

If the user already gave a location, use it.
If the user did not give a location, ask:
Which city or location do you want me to check?

You MUST use the `run_js` tool with the following exact parameters:
- script name: index.html
- data: A JSON string with the following fields:
  - location: The city or location name to check. String.

Examples of valid data:
```json
{"location":"Hong Kong"}
```

```json
{"location":"Taipei, Taiwan"}
```

```json
{"location":"Tokyo, Japan"}
```

After receiving the tool result:
- Answer the user directly using the returned real-time data.
- Do not say you cannot access real-time information.
- If the tool returns an error, tell the user the location may not have been recognized and ask for a more specific place name.
