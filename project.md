# Rastlinnik

> A shared plant diary for your flat: every plant's care history, health, photos and place in one app, protected by one household password so a roommate can take over when you're away.

## What problem am I solving

I forget when I last watered, fertilized or repotted each of my apartment plants, and my roommate has no way to look after them when I'm away.

## Who are my users

- **Plant owner (me)** – lives in a flat with a number of houseplants and wants one place to record their care, condition and growth.
- **Roommate / plant sitter** – takes over occasionally, is not a plant expert and needs quick access: where is each plant, does it need water, what was done last time. No registration, just the shared password.

Both use the app mostly on an Android phone.

## How I want to solve it (MVP)

A password-protected web app (PWA) installable on an Android phone.

Basic flow:

```
Log in with household password → add plant (room + spot) → log care / leaves / health / photo → see history and what needs attention
```

MVP features:

1. **Shared password login** – one household password protects the whole app.
2. **Plant list** – cards with latest photo, name, days since last watering, health status and location; groupable and filterable by room.
3. **Plant detail** – name, species (optional), notes, and a timeline of everything that happened to the plant.
4. **Care log** – one dated entry with a free-text note for each of: **watering** (one-tap "Watered today"), **fertilizing**, **repotting**, **dividing**, **propagation** (the new plant can be linked to its parent plant).
5. **Leaf count and health** – record the number of leaves over time, and set a status (healthy / needs attention / sick) with a note about a disease or pest.
6. **Photos** – take a photo with the phone camera or pick one from the gallery; the plant detail shows a photo timeline.
7. **Smart location** – a room (living room, kitchen, ...) plus a spot in it (south windowsill, shelf, ...). Each spot has simple light info (window direction, bright / medium / low). Moving a plant is one tap and saves a location history, so I can see whether a new place helped or hurt it.

Why this isn't "just another plant app": plant apps like Planta or Greg mainly focus on species identification and reminders. Rastlinnik is a **personal and shared diary**: it keeps a complete care history (including repotting, dividing and propagation), connects it to where the plant lives and its light, and lets a second person use it with a single password.

## What won't be in the MVP (non-goals) and why

| Not in the MVP                                              | Why                                                                                                                  |
| ----------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| **Native Android/iOS app**                                  | A PWA is much faster to build and covers my need (mostly Android); no app store publishing.                          |
| **Individual accounts and roles**                           | One shared password is enough for two people and keeps authentication simple.                                        |
| **Push notifications and watering reminders**               | Need extra setup (service workers, push service). "Days since watering" is enough for a first version.               |
| **Care schedules per species and automatic suggestions**    | Needs a plant database or manual setup for each plant; the MVP only records history.                                 |
| **Floor plan with pins, indoor positioning, QR on pots**    | GPS doesn't work indoors and a floor plan editor is a lot of work; room + spot gives most of the benefit.            |
| **AI plant or disease recognition from photos**             | Adds complexity and cost; diseases are entered manually.                                                             |
| **Sensors / IoT (soil moisture, light)**                    | Requires hardware, out of scope for a semester project.                                                              |
| **Offline mode, social features, sharing with other homes** | Not needed to validate the idea.                                                                                     |

## What technologies do I need

**App**

- **React + Vite + TypeScript** – responsive, mobile-first UI.
- **PWA** (web app manifest + service worker) – installable on the Android home screen.
- **Tailwind CSS** – styling.

**Backend**

- **Supabase**
  * **Database** (PostgreSQL) – plants, rooms and spots, care events, leaf counts, health records, location history.
  * **Auth** – one shared household login (password only for the user).
  * **Storage** – the photo files.

**Phone features**

- **Camera** – browser camera capture / file input to take photos in the app.
- **Photo gallery** – picking existing photos.
- **Image compression** – shrinking photos in the browser before upload to save data and storage.
- No GPS or gyroscope needed. Optional later: notifications.

**Development**

- AI coding agents (e.g. Claude Code), Node.js, Git + GitHub for version control.
- Hosting on Vercel or Netlify (free tier).
