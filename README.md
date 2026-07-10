# SMOTE Ⅱ — a zero-player picaresque, deluxe

A single-file, zero-player RPG in the tradition of *Godville* and *Progress Quest*:
one hero lives an entire life in a window on the left while you read their diary on
the right. You are their god. You watch, and — sparingly — you **bless**, **punish**,
and **whisper**.

**[▶ Play it](https://charlesmod.github.io/smote/)** *(hosted build; see caveat below)*

Everything is one HTML file. No build step, no dependencies. Open it and it runs.

---

## The idea

A deterministic, seeded substrate runs the hero's whole life — quests, epics, bosses,
loot, gold, temple-building, death. On top of that sits an optional LLM playing **two
roles from one model**:

- **The Hero** — the LLM puppets "the guy" in the first person. In a fight it declares
  free-text actions (`>throw sand in its eyes then stab`) and can heed your last
  whisper. Its declaration *is* the diary entry, so you watch it think and fight.
- **The Dungeon Master** — the same model wearing the world's hat. It runs the monsters,
  rules on how the hero's action lands, and doles out the spoils (including real weapons).

Between them sits **the dice**: a deterministic resolver reads the character sheet and a
seeded RNG and settles the numbers. The DM frames the odds; the dice decide the outcome.
That split is deliberate — it keeps the model from fanfic-ing the hero to godhood, and it
means your divine influence moves *intent*, never *outcome*.

If no model is connected, everything falls back to hand-written template tables and a
deadpan seed corpus — the picaresque never stalls.

## Verbs of a god

| verb | cost | effect |
|---|---|---|
| ☀ **Encourage** | 25 gp | heal & lift mood; mid-fight it wounds the foe |
| ⚡ **Punish** | 25 gp | smite the hero; enough of it and their theology curdles |
| **Speak** | 20 gp | a free-text whisper the hero interprets — and may act on in combat |

The hero **models you back**: your record of blessings, punishments, and silence becomes
their working theology (see the **Theology** tab), and it colors every diary entry and
where their gold goes — temple bricks when devoted, ale when resentful.

## Systems

Four attributes — **Might** (melee), **Finesse** (thrown/crit/dodge), **Wits**
(tricks/scrolls, ignores weapon quality), **Grit** (HP/armor) — each keyed off by an
equipment slot and an action type. Companions that live and die, cursed items, multi-step
epics, grudges that remember, a rival, weather, taverns, festivals, a graveyard, and a
markdown **chronicle export**.

## Connecting your own model

The **⚙ Machinery** panel takes any OpenAI-compatible endpoint (llama-swap, LiteLLM, etc.)
or Anthropic in-app. The full brain — improvised combat, ghostwritten milestones, whisper
interpretation — lights up when a model answers.

> **Caveat:** the hosted GitHub Pages build is served over HTTPS, which blocks fetches to
> plain-HTTP LAN endpoints (mixed-content). To use a local model, **download `index.html`
> and open it from disk**, then point the ⚙ panel at your endpoint. The hosted build still
> plays fully in template mode with the brain off.

Settings and progress persist in `localStorage`. **New Hero** starts a fresh life;
settings survive it.

## Files

- [`index.html`](index.html) — SMOTE Ⅱ, the deluxe build
- [`smote-v1.html`](smote-v1.html) — the original single-hero version, for reference

## License

MIT
