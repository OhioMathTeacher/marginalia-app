# Marginalia

A reading-and-writing studio for the classroom: read a canonical text closely,
think in the margins, and write your way toward understanding — with two AI
thinking partners on call. No account, no backend; your work stays in your
browser.

**Open it → [https://ohiomathteacher.github.io/marginalia/](https://ohiomathteacher.github.io/marginalia/)**

## What you can do

- **Read** five source documents, several offered in translation:
  - *The Allegory of the Cave* — Plato (*Republic*, VII) — English & Modern Greek
  - *Hind Swaraj: What is True Civilization?* — M. K. Gandhi (Ch. XIII) — English, Spanish, Chinese, Hindi
  - *Analects, Book 1 (On Learning)* — Confucius (孔子) — English, Spanish, Hindi
  - *Thanatopsis* — William Cullen Bryant
  - *A Doll's House* — Henrik Ibsen
- **Annotate** — select any passage and ask a question; the answer lands in the
  margin and is saved beside the text.
- **Freewrite** — open a private page and keep your pen moving. Raw, unguarded
  thinking in the spirit of Peter Elbow: auto-saved, never graded, never shared.
- **Build a Writer's Journal** — send a passage or a freewrite to a dated page
  and come back to it later; browse the journal by date or by reading.
- **Six-language interface** — English, Spanish, Chinese, Hindi, Greek, Norwegian.
- **Export / import** your notes and journal as JSON, for backup or transfer.

## Two AI thinking partners

Marginalia gives you two voices, after Peter Elbow's *believing and doubting game*:

- **Socrates** — plays the doubting game. He questions, presses, and looks for
  what doesn't hold up.
- **Elbow** — plays the believing game. He encourages, takes your idea seriously,
  and helps you build it out. (Named in tribute to Peter Elbow, 1935–2025, whose
  freewriting and believing game shape the writing side of this app.)

## Choosing a model

Pick any provider in the **🤖 AI Setup** menu:

- A **local model** (Ollama) running on your own machine — fully private, no key.
- A **cloud provider** with your own key: Anthropic Claude, Google Gemini, or
  Groq. Keys are stored only in your browser and never written into the source.

## Privacy

Everything — annotations, freewrites, the journal, your API key — lives in your
browser's local storage. Nothing is sent to a server of ours (there isn't one).
Use **Export** to keep a JSON backup or move your work to another machine.

## Running it yourself

The app is a single self-contained `close-reader.html` plus a small `vendor/`
folder (for `.docx`/`.pdf` import). Serve the repository root with any static
server — e.g. `python3 -m http.server` — and open `close-reader.html`. The repo
also carries a Tauri scaffold (`src-tauri/`) for building a native desktop
version, but the web app is the primary surface.

## Credits

Built by [@OhioMathTeacher](https://github.com/OhioMathTeacher). The believing
and doubting game, and the freewriting practice at the heart of the writing
tools, are Peter Elbow's. Socrates is on loan from Plato.
