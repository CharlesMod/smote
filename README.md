# SMOTE Ⅲ — the pure fishbowl

A single-file, **zero-player roguelike the AI plays entirely on its own**, in the
tradition of *Godville* and *Progress Quest* — except nobody is steering, including you.
A party marches left-to-right across five zones to slay the Demon King. Every hero is
LLM-puppeted and takes their own turn; the same model, wearing a different hat, runs the
monsters. You only watch.

The party knows you're watching. They write their log *to* you. You never answer —
there are no buttons to answer with — and they build an entire theology out of the
silence (see the **Doctrine** tab).

**[▶ Watch it](https://charlesmod.github.io/smote/)** *(hosted build; see caveat below)*

Everything is one HTML file. No build step, no dependencies. Open it and it runs.

---

## The idea

A deterministic, seeded substrate runs the whole march — combat resolution, XP, gold,
shops, permadeath. On top sits an optional LLM playing **every role from one model**:

- **The heroes** — each party member picks their combat action in character (from a
  fixed spell kit → structured JSON → deterministic dice, so the model can't cheat),
  banters at the campfire with memory of past conversations, and holds grudges.
- **The Dungeon Master** — declares enemy intents you can read, phases bosses,
  restocks the absurd-wanderer bestiary (the Municipal Goose is procedurally rendered
  *as a goose*), writes tavern rumors.
- **The chronicler** — ghostwrites the shared road-log in the voice of the original
  SMOTE community corpus: a first-person-plural grievance ledger filed upward at a god
  who never replies. Gravestones get epitaphs. Victories get ballads. Wipes get laments.

Between them sit **the dice**: seeded, deterministic, and indifferent to eloquence.

If no model is connected, everything falls back to hand-written template tables in the
same voice — the march never stalls. An amber badge tells you when the model has gone
silent, so canned never masquerades as written.

## The roguelike

- **Solo start.** One hero sets out alone. Companions are *earned* — first blood,
  boss kills, moments of valor, kindness repaid — never handed out.
- **Five zones**, rising difficulty, a demon general gating each, the Demon King last.
- **Permadeath with memory.** Graves persist across runs and line the road for every
  party that follows. Good gear outlives its owner as heirlooms. The fallen are visited,
  quoted, and occasionally avenged.
- **Elemental affinities** the hero LLMs read and exploit — salamanders fear ice,
  the dead fear holy, gazebos fear lightning, and blades pass through wisps.
- **An economy**: gold, waystations, rations that run out, murky vials best identified
  by drinking, relics, scars, a rival band racing you to the keep.
- **A pet.** One per party, legally bonded, indestructible. It survives wipes and waits
  at the first milestone for the next party. It does not explain itself.
- Weather, day/night, zone title cards, a synth the size of a coin (🔊 to enable).
- **The Annals**: every run archived — party, fates, doctrine, ballad, full chronicle —
  exportable as markdown.

Balance is calibrated by a headless simulation harness (`window.simRuns(n)` in the
console) to ~53% unassisted win rate, so both victory and grief stay common enough
to mean something.

## Connecting your own model

The **⚙** panel takes any OpenAI-compatible endpoint (llama-swap, LiteLLM, vLLM, etc.)
or Anthropic in-app. Point the base URL at your server (e.g. `http://localhost:8080/v1`)
and set the model to one your server lists. A small fast model is the right choice —
the game makes many short calls per minute.

> **Reasoning models:** keep **disable thinking** on (it is by default). A reasoning
> model's `<think>` pass eats the short token budgets and returns *empty* content. The
> toggle sends `chat_template_kwargs: {enable_thinking: false}`, which llama.cpp and
> vLLM honor and other servers ignore.

> **Caveat:** the hosted GitHub Pages build is served over HTTPS, which blocks fetches
> to plain-HTTP LAN endpoints (mixed-content). To use a local model, **download
> `index.html` and open it from disk**, then point the ⚙ panel at your endpoint. The
> hosted build still runs fully in template mode with the brain off.

Settings and progress persist in `localStorage`. When a party wipes, a new one sets out
on its own thirty seconds later. `errlog()` in the console shows any captured errors.

## Files

- [`index.html`](index.html) — SMOTE Ⅲ, the fishbowl
- [`smote-v1.html`](smote-v1.html) — the original single-hero version, for reference

## License

MIT
