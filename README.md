# ISSN 2026 Planner

A personal session planner for the **23rd Annual ISSN Conference and Expo** — June 17–19, 2026, The Westin Fort Lauderdale Beach Resort.

This is a single-file static web app: open `index.html` in any browser, no server required. Hostable as-is on GitHub Pages.

## Features

- All 46 sessions across Wed/Thu/Fri, filterable by day
- Star/favorite talks (saved locally in your browser)
- "Starred only" view to see just your picked schedule
- Search by title, speaker, sponsor, or topic
- Click any speaker name to read their bio
- **Your poster slot is highlighted in gold** (Thursday 3:00 PM, with Ian Jump)
- **Conflict warnings** flag concurrent sessions that overlap with your poster
- Sponsor and keynote badges
- Mobile-friendly layout

## File structure

```
issn-2026-planner/
├── index.html      # The entire app — HTML, CSS, JS, and session data all inline
└── README.md       # This file
```

The session data (`SESSIONS`) and speaker bios (`BIOS`) live as JS objects near the top of the `<script>` block in `index.html`. Edit them there directly.

## How to add or edit a session

Find the `SESSIONS` array in `index.html` and add an object with this shape:

```js
{
  day: "Thursday",                    // "Wednesday" | "Thursday" | "Friday"
  date: "June 18",                    // human-readable
  time: "3:00–3:30 PM",               // shown as-is
  num: "23",                          // session number or "Break"/"Lunch"/"POSTER"
  title: "Talk title",
  desc: "Description shown when expanded.",
  speakers: ["First Last"],           // names must match keys in BIOS for clickable bios
  moderator: "Moderator Name, PhD",
  room: "Las Olas I, II, V, VI",
  sponsor: "Maypro",                  // optional — shows a sponsor badge
  note: "Keynote",                    // optional — shows a generic badge
  conflict: "Conflicts with X",       // optional — shows a red warning badge
  type: "break" | "yours" | "event"   // optional — styling variant
}
```

To add a bio so the speaker's name becomes clickable, add a key to `BIOS`:

```js
"First Last": "Short bio text shown in the modal."
```

## Conventions for future edits

Read these before letting any AI agent (Cursor, etc.) make changes:

1. **Keep the app single-file.** All HTML, CSS, JS, and data live in `index.html`. This is intentional — it makes the app trivially portable, hostable, and emailable. Resist suggestions to "modernize" by splitting into separate files unless we explicitly decide to migrate.
2. **No external dependencies.** No CDN, no npm, no build step. Anyone can double-click `index.html` and it works offline.
3. **localStorage only for personal state.** Starred talks are stored under the key `issn2026_starred`. Don't introduce cookies, accounts, or remote sync.
4. **The user's poster row stays highlighted.** Look for `type: "yours"` in SESSIONS — that's the marker. The styling is in `.session.yours` CSS.
5. **Edit data, not structure, for routine updates.** New talks, time changes, speaker swaps → edit the SESSIONS array. Don't refactor the render function unless you need to add a new feature.
6. **Test locally before committing.** Double-click `index.html`, verify your change renders, then commit.
7. **Commit messages should describe the change.** "Add Galpin talk", "Fix Stout time", "Update Eldakar room" — not "Update file" or "Changes".

## Known data caveats

- Session #29 doesn't exist — the printed program skips from #28 to #30 on Friday morning. Not a missing extraction.
- The 3:00 PM Thursday slot has a known scheduling conflict: your poster (3:00–3:30 PM) overlaps with Eldakar's talk (#23, 3:00–3:15 PM) and Nelson's wearables talk (#24, 3:15–3:30 PM). Both are flagged with conflict badges.
- The Day 2 program also lists a "Poster Presenters please put your poster up at the designated easel stand" instruction at 3:30 PM, and the full poster *session* runs 5:00–6:15 PM during Happy Hour. If the 3:00 PM time on your poster row is wrong, update the `POSTER` entry in SESSIONS.

## Hosting on GitHub Pages

1. Push this repo to GitHub.
2. Repo Settings → Pages → Source → `main` branch, root folder → Save.
3. Wait 1–2 minutes for the green build check in the **Actions** tab.
4. Your app will be live at `https://<your-username>.github.io/issn-2026-planner/`.

## License / use

Personal use. Bio text and session details are reproduced from the published ISSN 2026 program.
