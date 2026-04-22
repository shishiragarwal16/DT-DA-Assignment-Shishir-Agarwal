# The Daily Reflection Tree
### DT Fellowship Assignment — Daily Reflection Tool
### Submitted by Shishir Agarwal
A deterministic end-of-day reflection tool built on a structured decision tree. No LLM at runtime — the intelligence is encoded in the tree structure and reflection text.

---

## Repository Structure

```
/tree/
  reflection-tree.json     ← Part A: Full tree data (35 nodes)
  tree-diagram.md          ← Part A: Mermaid visual diagram

/agent/
  index.html               ← Part B: Web UI agent (open in any browser)

/transcripts/
  persona-1-transcript.md  ← Part B: Victor/Contribution/Altrocentric path
  persona-2-transcript.md  ← Part B: Victim/Entitlement/Selfcentric path

write-up.md                ← Part A: Design rationale (2 pages)
README.md                  ← This file
```

---

## Part A: Reading the Tree

### Format: JSON

The tree is in `tree/reflection-tree.json`. Each node has:

| Field | Purpose |
|-------|---------|
| `id` | Unique node identifier |
| `type` | `start`, `question`, `decision`, `reflection`, `bridge`, `summary`, `end` |
| `text` | What the employee sees. `{A1_OPEN_label}` interpolates their earlier answer. |
| `options` | Array of fixed choices (question nodes only). Each option has `label`, `value`, optionally `signal` and `next`. |
| `routing` | Array of condition→next mappings (decision nodes only, expressed as JS functions in the agent) |
| `next` | Default next node |
| `signal` | What this node contributes to state: `axis1:internal`, `axis2:contribution`, etc. |
| `axis` | Which axis this node belongs to (1, 2, or 3) |

### Tracing a Path

To trace a path manually through the JSON:
1. Start at `START`
2. Follow `next` for non-question nodes
3. For `question` nodes, pick an option and follow that option's `next` (or the node's `next` if the option doesn't have one)
4. For `decision` nodes, evaluate `routing` conditions in order; first match wins

### Node Counts

| Type | Count |
|------|-------|
| start | 1 |
| question | 11 |
| decision | 7 |
| reflection | 9 |
| bridge | 2 |
| summary | 4 |
| end | 1 |
| **Total** | **35** |

### Three Axes

- **Axis 1 — Locus (Victim ↔ Victor):** Nodes `A1_*`
- **Axis 2 — Orientation (Entitlement ↔ Contribution):** Nodes `A2_*`
- **Axis 3 — Radius (Selfcentric ↔ Altrocentric):** Nodes `A3_*`

Each axis has 2 question nodes, 1 decision node, 2–3 reflection nodes, and contributes to a running tally that shapes the final summary.

---

## Part B: Running the Agent

### Web UI (Recommended)

1. Open `agent/index.html` in any modern browser
2. No server, no dependencies, no install
3. The agent loads the tree logic from the embedded JavaScript and walks you through the full conversation

**Features:**
- Axis progress tracker (shows which axis you're on)
- Progress bar
- Reflections styled differently from questions
- 4 personalized summary archetypes based on your path
- Restart capability

### No LLM at Runtime

The agent makes zero API calls. All branching, reflection text, and summary generation is handled by:
- `if/else` routing conditions
- String interpolation (`{A1_OPEN_label}` → your earlier answer)
- Signal tallies (`axis1.internal`, `axis2.contribution`, etc.)

---

## Design Highlights

1. **Weather metaphor as opener** — avoids priming with "did you take responsibility today?" before the employee has described their day
2. **Non-moralizing reflections** — the external locus path says "somewhere in today, you made a call" not "you should have taken responsibility"
3. **4 summary archetypes** — VCA (Victor/Contribution/Altrocentric), EES (External/Entitlement/Selfcentric), ICM (Internal/Contribution mixed), DEFAULT
4. **Interpolation throughout** — the tree uses the employee's own words back to them to create continuity
5. **Bridge nodes connect axes** — not just transitions, they carry the emotional thread forward

See `write-up.md` for full design rationale and psychological grounding.

---

## Psychological Foundations

| Framework | Source | Application |
|-----------|--------|-------------|
| Locus of Control | Rotter (1954) | Axis 1 branching logic |
| Growth Mindset | Dweck (2006) | A1_Q2_FOLLOWUP question design |
| Psychological Entitlement | Campbell et al. (2004) | Axis 2 entitlement branch |
| Org. Citizenship Behavior | Organ (1988) | Axis 2 contribution branch |
| Self-Transcendence | Maslow (1969) | A3_R_TRANSCEND reflection |
| Perspective-Taking | Batson (2011) | A3_OPEN radius spectrum |
