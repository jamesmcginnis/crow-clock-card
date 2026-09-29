# 🕐 Crow Clock Card

A beautiful analog clock card for [Home Assistant](https://www.home-assistant.io/) with twelve distinct clock faces, including an animated Stargate portal, and a smooth sweeping second hand. Tap the clock to open a popup with a large digital clock, a month calendar and the events from your Home Assistant calendar. You can choose the Classic look with your own colours or a liquid-glass look in light or dark. Optional AI features add a summary of your day, a spoken rundown on your speakers, questions about your calendar, a week-ahead view and quick event adding. Everything can be set up without writing any YAML.

> ✨ **AI features are optional.** Nothing AI-powered runs until you turn on AI features and choose a conversation agent in the editor (see [AI Features Setup](#-ai-features-setup-optional) below). Without an agent, the card works fully as a clock and calendar.

---

## ✨ Features

### Clock faces
Twelve faces, each with its own markers, numerals and hands:

| | | | |
|---|---|---|---|
| Classic | Minimal | Roman | Modern |
| Luxury | Skeleton | Neon | Retro |
| Sport | Art Deco | Celestial | Stargate |

- **Stargate** is animated: a slowly turning glyph ring, chevrons that light up in sequence as the seconds pass, and a ripple across the water-like portal every minute.
- **Seconds hand**: an optional smooth sweeping second hand.
- **Date**: optionally show today's date under the clock.

### Popup
Tap the clock to open it:
- **Digital clock** in 12-hour (AM/PM) or 24-hour format, with the full date.
- **Month calendar**, Monday first, with today highlighted. Use the arrows to move between months.
- **Your events**: tap any date to see the events from your chosen Home Assistant calendar, with times and locations. Today's events load when the popup opens.
- **Optional link**: a button at the bottom of the popup that opens any URL, for example `calshow://` for the iOS Calendar app.

### Appearance
- **Style**:
  - **Classic** uses your own card colour.
  - **Glass** is a frosted, see-through surface with blur, soft highlights and rounded corners, and the popup becomes a matching glass panel. Your dial and hand colours are still used.
- **Theme** for the Glass card and its popup: Auto (follows Home Assistant), Light or Dark.
- **Glass** slider, from clear to frosted.
- **Colours** for the card background, clock dial, dial text and marks, hour hand, minute hand, second hand and accent. The card background and the dial can also be set to **None** for no fill.
- **Colour presets**: Classic (default), Ocean, Berry, Graphite and Paper. One tap applies a preset, and you can then fine-tune any colour.

### AI features (optional)
You need a Home Assistant conversation agent for these. Once AI is turned on, a **⋯** button appears in the popup next to the close button:
- **Your day**: a one- or two-sentence summary above the events for whichever day you tap, for example "Three things today: the dentist at 10, then you're free until the 4pm school run." For today it focuses on what's still ahead.
- **Announce**: a spoken rundown of the selected day, played on the speakers you tick. For today it starts with a greeting and the time. Speakers are grouped by area, unavailable speakers and TVs are hidden, and nothing is ticked when Announce opens. It uses Home Assistant's text-to-speech and also works with Music Assistant speakers.
- **Ask**: ask a question about your calendar, or tap a suggestion such as "When am I free this week?". Answers only use your events for the next month, and you can send any answer to **Announce**.
- **Week ahead**: the next 7 days at a glance, with a bar for each day, any events that overlap, and a short summary. Tap a day or a clash to jump to it in the calendar.
- **Quick add**: type something like "Dentist next Tuesday at 3" and the card shows you the event to check. Nothing is saved until you tap **Add to calendar**. With no end time it books an hour, and with no time at all it adds an all-day event. This needs a calendar that accepts new events, such as a Local Calendar or Google Calendar.

Each feature has its own toggle in the editor. Nothing on the card itself mentions AI, and problems show as plain messages such as "Busy right now". Calendar text is treated as data, never as instructions, and everything is escaped before it's shown.

---

## Configuration

Add the card from the card picker, then choose a face, your calendar and your colours in the built-in visual editor. You don't need to write any YAML. The README lists every YAML option.

---

## 🤖 AI Features Setup (Optional)

AI features stay off until you turn them on and choose a conversation agent. **Google Gemini** is the recommended and best-tested agent:

### Step 1 — Enable the Generative Language API

1. Go to [console.cloud.google.com](https://console.cloud.google.com) and sign in
2. Create a new project (or select an existing one)
3. Go to **APIs & Services → Library**
4. Search for **Generative Language API** and click **Enable**

> ⚠️ Don't skip this step. An API key won't work until the Generative Language API is enabled; it will return errors straight away.

### Step 2 — Create an API Key

1. In Google Cloud Console go to **APIs & Services → Credentials**
2. Click **+ Create Credentials → API key** and copy the key

### Step 3 — Add Google Generative AI to Home Assistant

1. In Home Assistant go to **Settings → Devices & Services → + Add Integration**
2. Search for **Google Generative AI** and select it
3. Paste your API key and click Submit
4. The recommended model settings work fine. If you choose a model yourself, pick a **current Flash model**, because Google retires older models regularly (`gemini-2.0-flash` was shut down in June 2026).

### Step 4 — Configure the Card

In the card's visual editor, open **AI Features**, turn on **Enable AI features**, and choose your Google AI agent under **Conversation agent**.

### Rate limits

Free-tier limits vary by model and change over time, so check Google AI Studio for your current quota. The card only calls the agent when you open the popup (for the day summary) or use an AI feature, and it caches answers, so you're unlikely to reach the limit in normal use. If you do see a quota message, it resets the next day.

If the agent can't answer, the card shows the reason in plain English and a **Try again** button. It retries once automatically first. If the day summary can't be made, it's simply left out and your events still show.

---

## 📅 About Calendars

- Any Home Assistant calendar works for showing events, for example Local Calendar, Google Calendar or CalDAV.
- **Quick add** needs a calendar that accepts new events. If yours doesn't, Quick add says so and suggests choosing one that does.
- The popup shows up to 8 events for a day. Ask uses the next month of events, and Week ahead uses the next 7 days.
