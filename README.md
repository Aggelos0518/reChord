# reChord

**Movies that sound like you.**

The name plays on *chord* (music) and *record* (film), and the logo is a clapperboard whose clapper is a guitar neck.

reChord is a mobile app that connects to your Spotify account, measures how your music *feels* (energy, mood, atmosphere, the hours you listen) and recommends films with the same emotional signature. It also forecasts how your music will feel in the coming days, so the right films are ready before you ask.

This repository contains the **interactive mockup**: a clickable preview that looks and behaves like the real app, but does not actually work yet.

---

## Why it's new

Most recommenders stay inside one domain: Netflix recommends films from the films you watched, Spotify recommends songs from the songs you played. reChord is a **cross-domain recommender**. It uses your music, which you already have years of data about, to answer "what should I watch tonight?", and it explains every pick in terms of your own listening.

## The two intelligent features

Both are **not implemented** in this mockup. Every recommendation, match score and forecast you see is hard-coded sample data. They will be built during the semester.

### 1. Recommender system: films from your music

- Builds a *Sound DNA* from your listening: energy, mood, atmosphere, genres, peak hours.
- Recommends films whose tone, pacing and soundtrack match that profile, with a match score and a plain-language reason.
- Picks a film for the song you are playing right now.
- Learns from feedback: saves, passes and ratings in the swipe deck and on film pages.
- Lets you steer tonight's list with the Tune mixer (energy, mood, atmosphere, familiar ↔ discover).

### 2. Predictive model: Mood Forecast

- Predicts how your music will feel over the next 7 days and hour by hour each evening, like a weather forecast.
- Shows a confidence level and the reasons behind each forecast (day of week, recent trend, time of day).
- Suggests the best time to start a film and has films ready for each forecast mood.
- Forecasts next month's mood trend on the profile page.

## Where the models plug in

All screens get their data from a single object in `index.html` called **`MockAPI`**. Each function currently returns sample data from `MOCK` and is marked `TODO`:

| Function | Feature | Returns |
| --- | --- | --- |
| `MockAPI.forYou()` | Recommender | Top match and the themed lists on For You |
| `MockAPI.pickForTrack(track)` | Recommender | Best film for the song playing now |
| `MockAPI.tonight()` | Recommender | Films for the swipe deck |
| `MockAPI.forMix(mix)` | Recommender | Ranking for a Tune mix (mock: closest preset's fixed list) |
| `MockAPI.match(id)` | Recommender | Match score for one film |
| `MockAPI.feedback(id, kind)` | Recommender | Receives saves, passes and ratings (mock: only counts them) |
| `MockAPI.forecast()` | Predictive model | 7-day mood forecast with hourly curves and confidence |

Replacing the body of these functions with calls to real models is enough for the screens to show real results.

## Screens

| Screen | What it shows |
| --- | --- |
| Welcome | Animated poster wall, pitch, "Connect Spotify" |
| Connect | Exactly what reChord reads, and what it never does |
| Analysis | Animated audio visualiser while the library is "analysed" |
| Sound DNA | Persona, radar of sound features, top artists, genre mix, listening clock |
| Music → film | How each music trait maps to a film trait |
| For You | Pick for the song playing now, top match, mood forecast, themed lists |
| Mood forecast | Tonight's forecast, hourly chart with uncertainty, reasons, films ready, next 7 days |
| Tonight | Swipe deck: right to save, left to pass |
| Tune | Mixing-console faders and crossfader |
| Film detail | Match score, why it's for you, you-vs-film comparison, linked artists, a mood-setting mix |
| Saved | Watchlist |
| Profile | Sound DNA, mood trend with next month's forecast, settings, how it works |

## Run it

No build step and no dependencies.

- Open `index.html` in any modern browser, **or**
- Enable GitHub Pages for this repo (Settings → Pages → Deploy from branch → `main` / root) and open the published URL on your phone.

On a desktop the app appears inside a phone frame, with a side panel to jump between screens. At phone width it runs full-screen.

## Project structure

```
index.html   the whole mockup: markup, styles, sample data (MOCK) and MockAPI
README.md    this file
```

Film posters are generated in CSS (no copyrighted artwork is used). Artist and film names are used only as sample data.

## Notes for building the real thing

- **Listening data:** Spotify Web API (top artists, top tracks, recently played) via OAuth. Since November 2024, Spotify restricts the *Audio Features*, *Audio Analysis* and *Recommendations* endpoints for new apps, so sound features will need another source.
- **Film data:** TMDB for metadata, keywords and soundtrack information.

---

*reChord is a student project and is not affiliated with Spotify.*
