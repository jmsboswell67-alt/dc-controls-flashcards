# DC Controls Flashcards

> An open-source flashcard deck and study tool for **BMS / data center controls technician interviews**. ~340 cards across electrical, mechanical, controls, networking, and operations. Single self-contained HTML file. Optional local-LLM grading via Ollama — your answers never leave your machine.

![Status: Active](https://img.shields.io/badge/status-active-success) ![License: MIT](https://img.shields.io/badge/license-MIT-blue) ![No deps](https://img.shields.io/badge/dependencies-none-brightgreen)

---

## What this is

If you're interviewing for a **Building Management System (BMS / BAS) technician**, **Data Center Controls Technician**, **Critical Facilities Engineer**, **Mission-Critical Operations** role — or you're a BAS person trying to bridge into hyperscale — you've probably noticed the technical question bar is wide and deep: electrical theory, mechanical systems, BACnet/Modbus, networking, operations language, scenarios.

This is a self-contained study tool that drills you across all of it.

### What's in the deck (~340 cards)

| Section | Cards | What's in it |
|---------|-------|--------------|
| ⭐ Ambush Fixes | 21 | PUE / WUE / CUE family + the 4 basic point types (AI / AO / BI / BO) — the stuff interviewers ask first to gauge your foundation |
| Vocabulary | 58 | Every acronym you need: BMS, AHU, CRAH, UPS, ATS, PDU, MOP/SOP/EOP, etc. — framed as "What is X?" questions |
| Magic Numbers | 26 | Port numbers (47808, 502), device limits, ASHRAE envelopes, PUE benchmarks |
| Electrical | 49 | Ohm's law, VFDs, UPS topology, ATS sequences, EPMS, transformers, NFPA 70E, LOTO, arc flash |
| Mechanical / Cooling | 43 | Refrigeration cycle, chiller types, cooling towers, evap cooling, ASHRAE A1-A4, hot/cold aisle containment, refrigerant phase-down |
| Controls (BMS protocols) | 39 | BACnet vs Modbus deep dive, RS-485, MS/TP token passing, BBMD, COV tuning, PID, P2P checkout |
| Networking & IT | 50 | OSI model, TCP/UDP, IP / CIDR / subnets, VLANs, STP, ports, SNMP, syslog, NTP, Purdue model, Cisco basics |
| Operations Language | 22 | MOP / SOP / EOP, change management, CoE, 5 Whys, concurrent maintainability, blast radius |
| Scenarios | 34 | "An AHU drops at 2 AM, walk me through it" — 30-45 second structured answers |

---

## Features

- **📇 Flip mode** — classic flashcard study. Click to flip, K = known, U = need work
- **⌨ Type mode** — type your answer, your local LLM grades it (lenient on wording, strict on accuracy) and tells you what was missing
- **🔍 Deep Dive** — one button gets a deeper explanation of any card from the LLM (how it works, why it matters in a data center, common gotchas, follow-up questions)
- **🔀 Shuffle / Sequential** — randomize or go in order
- **Section filters** — drill just one topic at a time
- **"Only need-work" filter** — focus on cards you've flagged as weak; they disappear from the active deck as you mark them known
- **Progress saved** in browser local storage — close the tab, come back tomorrow, your progress is intact
- **Keyboard shortcuts** — Space, ←/→, K, U, T (toggle Flip/Type), D (deep dive), Ctrl+Enter (grade)
- **Works offline** — no internet required once the HTML is on your disk. (LLM grading needs local Ollama; everything else works without it.)

---

## How to use

### Quickstart (Flip mode only — no AI)

1. Download `index.html`
2. Double-click to open in your browser
3. Start studying

That's it. Works offline, no install, no account.

### Add local AI grading (free, private, offline)

The Type mode and Deep Dive features call a local [Ollama](https://ollama.com) instance to grade your typed answers and produce expanded explanations. **No data leaves your machine.**

#### Setup (Windows)

1. **Install Ollama:** [ollama.com/download](https://ollama.com/download)
2. **Allow local browser access** — Ollama blocks `file://` origins by default. Two options:
   - **System-wide:** Open *System Properties → Environment Variables*, add user variable `OLLAMA_ORIGINS` = `*`, then **fully restart Ollama** (right-click tray icon → Quit, then re-launch).
   - **One session:** Open PowerShell and run `$env:OLLAMA_ORIGINS="*"; ollama serve` (replaces the background service for that terminal).
3. **Pull a model.** In PowerShell:
   ```
   ollama pull llama3.1
   ```
   Or for a faster/smaller option: `ollama pull llama3.2:3b`. Or for stronger reasoning: `ollama pull qwen2.5`.
4. Open `index.html`, click **⚙ Settings → Test connection**. Green = good.
5. Switch to **⌨ Type** mode and start drilling.

#### Setup (macOS / Linux)

Install Ollama, then either set `OLLAMA_ORIGINS=*` in your shell profile and restart Ollama, or run `OLLAMA_ORIGINS=* ollama serve` for an ad-hoc session.

#### Recommended models

| Model | Speed | Quality | Notes |
|-------|-------|---------|-------|
| `llama3.1` (8B) | Medium | Good | Solid default |
| `llama3.2:3b` | Fast | OK | Use if grading feels slow |
| `qwen2.5` | Medium | Strong reasoning | Good at structured technical Q&A |
| `mistral` | Medium | Good | Solid alternative |

First grading call per session is slow (15-45s) while the model loads into memory. Subsequent calls take 5-15s on average hardware.

---

## Suggested study plan

If you have **~2 weeks** before an interview:

- **Week 1 — baseline.** One shuffled Flip-mode pass through *All Sections*. Mark every card as Known or Need-work. This builds your map of what you actually know.
- **Week 2 — drill the gaps.** Switch to Type mode + check "Only show need-work". Let the LLM grade you. Watch the deck shrink as you mark cards known. Use **Deep Dive** on any card you don't fully understand.
- **Day before — light review.** Section filter "⭐ Ambush Fixes" + shuffle. Five-minute rapid pass. Sleep matters more than another 30 cards.

If you only have **a couple of days**: focus on Ambush Fixes, Magic Numbers, and Scenarios. Those are the highest-density payoff.

---

## Contributing

PRs welcome. Especially:

- **More cards** in any section — particularly Mechanical (chiller types, water treatment) and Electrical (paralleling switchgear specifics, breaker coordination)
- **New sections** if you spot a gap — refrigerant deep dive, fire suppression, water treatment, regional codes
- **Card improvements** — sharper questions, tighter answers
- **Translations** — if you'd find a non-English version useful
- **Bug fixes / UX improvements** on the HTML/JS

Adding a card is dead-simple. Open `index.html`, find the `const cards = [...]` array (around line 770), and add an entry:

```js
{ s: "electrical", q: "Your question here?", a: "Your answer here — keep it 1-3 sentences." },
```

Section keys: `ambush`, `vocab`, `numbers`, `electrical`, `mechanical`, `controls`, `networking`, `ops`, `scenarios`.

---

## Why this exists

I built this drilling for a controls interview at a hyperscale data center operator. I'd been a BAS field tech for a while — Metasys / BACnet / MS/TP / customer-IT integration — but the depth and breadth of a data center interview hit harder than I expected. Generic study sites didn't cover this niche. So I built my own.

Now that the deck exists, sharing it seems obviously useful. **The BMS / mission-critical world should have an open prep tool.** If you find it helpful, drop a star, share it with someone studying, or PR a card you wish had been there for you.

---

## License

MIT — see [LICENSE](LICENSE). Use it, fork it, modify it, ship it. Attribution appreciated but not required.

---

## Tech stack

- One HTML file. No build, no deps, no framework.
- Vanilla JS. ES2017+. Inline CSS.
- Optional [Ollama](https://ollama.com) for local LLM grading.
- Designed to run from `file://` or from any static host (GitHub Pages, Netlify, Cloudflare Pages).

## Roadmap ideas (PRs welcome)

- [ ] Bring-your-own-key support for cloud LLMs (Anthropic, OpenAI, Groq) as an alternative to Ollama
- [ ] Spaced-repetition scheduling (SM-2 algorithm) instead of just Known/Need-work
- [ ] Export/import progress as JSON
- [ ] Card decks for adjacent roles (Niagara/Tridium-specific, EPMS-specific, Cx engineer)
- [ ] Section for safety scenarios (NFPA 70E walkthroughs, LOTO drills)
- [ ] Print-to-PDF clean stylesheet for offline study
