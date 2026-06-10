# Handoff — Marginalia language UX (for next chat)

> **STATUS 2026-06-06 (afternoon) — MOSTLY DONE.** Implemented in commits
> `d6969ab` + `9ee5120`:
> - ✅ **Dropdown bug fixed** (ask #1) — explicit dark-popup colors on the
>   `<option>`s; "Your language" is readable.
> - ✅ **Labels added** (ask #3) — "Your language" (the UI/AI selector) and
>   "Read in:" (the source-text buttons), wired through i18n in all 6 locales so
>   they flip with the UI. "Read in:" only shows when a reading has 2+ editions.
> - ✅ **Spanish + Chinese Cave text added** (ask #2) — translated from Sheehan's
>   English, honestly labeled; the Cave now offers en/el/es/zh under "Read in:".
> - ✅ **Cooperation, not merger** — setting "Your language" now auto-follows the
>   text edition if the reading has one (reader can still hand-pick another).
> - ⤳ **Decided NOT to trim `UI_LANGS`** to en/es/el/zh — kept all 6, since the
>   two selectors are independent + clearly labeled, and trimming would drop
>   Hindi AI-help on Gandhi/Confucius. (Supersedes ask #2's trim recommendation.)
> - ⏭ **Still open:** es/zh editions for the *other four* readings (Gandhi,
>   Confucius, Bryant, Ibsen) — deferred to after the talk; not demoed live.
>   Open question below re Ancient vs Modern Greek: **left as-is** (Modern Greek).
>
> The rest of this file is the original plan, kept for context.

---

Context: prepping the Cincy AI Week talk. Marginalia is the Tauri/static
"Close Reader" app; the web frontend is `close-reader.html` (single ~4950-line
file). We're NOT implementing this yet — this captures the investigation and the
plan so the next session can move fast.

**To bring up the show / Marginalia to test changes:** run `start-demo.command`
(in `cincy-ai-week-2026/`) — it serves everything at `:8000` and opens the deck;
Marginalia is reachable at `http://localhost:8000/marginalia/close-reader.html`.
Full launch + OBS-recording + transcription procedure is in
`summer-2026/REHEARSAL.md`. (Note: Tailscale remote-transcription is shelved —
ToddGPT-Fedora is a FERPA box, no inbound SSH.)

## The two language systems (this is the source of the confusion)

1. **Interface + AI language** — the dropdown top-right (`#uiLangSelect`,
   `index`/`close-reader.html` line ~687, `onchange="setUiLang(...)"`). Its
   options come from `UI_LANGS` (line ~3476):
   `en, es, el, zh, hi, no` (English, Español, Ελληνικά, 中文, हिन्दी, Norsk).
   Setting it re-skins the whole UI **and** sets the AI's language. Rendered at
   line ~3672.
2. **Text translation** — the buttons *under the document title*
   (`.lang-btn`, built at lines ~4181–4183 from each reading's `languages`
   object; `switchLang()`; translation check at ~4301). These are per-reading.

The Allegory of the Cave reading currently offers only **English (Sheehan)** +
**Ελληνικά** (a *Modern* Greek pedagogical rendering — the big `TEXTS.el` blob at
line ~1214, wired in at ~1232). Other readings already carry es/zh/hi editions.

## Asks from Todd (in priority order)

1. **BUG — dropdown unreadable.** `#uiLangSelect` / `.ui-lang-select` renders
   near-white text on a near-white background. **Find the `.ui-lang-select` CSS
   rule and set explicit `color`/`background` on the select AND its `<option>`s**
   (options often need their own color on Linux/Chromium). Small, do first.

2. **Limit + align the languages.** Todd wants the Cave's offered languages to be
   **English · Español · Ελληνικά · 中文** (original-language + the three
   predominant world languages), and wants the AI/interface language set to match
   so the two selectors feel coherent.
   - **Recommendation:** trim `UI_LANGS` to `en, es, el, zh` (drop `hi`, `no`)
     for the talk, so interface/AI choices == the Cave's translation choices.
   - **Add Spanish + Chinese translations of the Cave text.** This is the bulk of
     the work: mirror the `TEXTS.el` structure (sections → paragraphs with
     `speaker`/`heading`/`text`) for `es` and `zh`, translated from the Sheehan
     English. Add them to the Cave reading's `languages` object beside `en`/`el`.
   - Open question for Todd: keep the **Modern** Greek pedagogical rendering, or
     swap to Plato's **Ancient/Classical** Greek as the true "original"? (He said
     "original language of the publication" — that's Ancient Greek.)

3. **Two selectors — keep but clarify (recommendation).** Keep them distinct: a
   Spanish speaker may legitimately read the Greek or English text while getting
   AI help in Spanish. But (a) align the option sets (above), (b) improve labels
   so it's obvious one is "text language" vs "your language," and (c) optional
   polish: when the chosen AI/interface language is also an available translation,
   show a subtle "read this in Español?" nudge.

## Key line references (close-reader.html)
- `#uiLangSelect` ~687 · `UI_LANGS` ~3476 · dropdown render ~3672 · `setUiLang`
- Cave Modern-Greek text `TEXTS.el` ~1214 · Cave `languages` wiring ~1232
- `.lang-btn` build ~4181 · `switchLang` · translation guard ~4301
- AI model label shows `llama3.2:3b` (matches the drive-spec model in the deck)

## Smallest path to "talk-ready"
Fix the dropdown color (#1), add `es` + `zh` Cave translations and trim
`UI_LANGS` to en/es/el/zh (#2). #3 labeling is polish if time allows.
