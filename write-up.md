# Write-Up: Design Rationale for The Daily Reflection Tree

---

## Why These Questions?

The assignment asks for questions that make a tired employee stop and think — not click through. Every question in this tree was stress-tested against a simple rule: *would I answer this honestly at 7pm, or would I game it?*

**Axis 1 (Locus)** opens with a weather metaphor rather than a direct question about agency. This is deliberate. Asking "did you take responsibility today?" primes for a socially desirable answer. Asking "if today were a weather report" is disarming — it invites the employee to describe the day before being asked to interpret it. The tree then uses their own word back to them (`"A {A1_OPEN.label} kind of day"`), which creates conversational continuity and signals that the system was actually listening.

The follow-up question on Axis 1 (`"If today repeated tomorrow, what would you change within your own control?"`) was included because it operationalizes the psychology. Locus of Control isn't just a belief — it's a disposition toward action. Asking for a concrete change filters for genuine internal locus vs. learned vocabulary about internal locus.

**Axis 2 (Orientation)** is the trickiest axis to surface honestly because entitlement is invisible to the person holding it. The framing "what was your energy going into it?" is softer than "were you contributing or expecting?" — it reduces defensive answering. The branch for entitlement-leaning employees (`A2_Q_ENTITLE_HIGH`) was designed to validate the desire for recognition before reframing: *"It's not wrong to want recognition... but there's a difference between wanting your work seen and keeping a ledger."* Non-moralizing reframes require agreeing with the emotion first.

**Axis 3 (Radius)** uses a spectrum of "who comes to mind" (me → team → colleague → customers) adapted from Batson's perspective-taking research. The insight from Maslow's later work — that orienting outward reduces suffering — is woven into the reflection text, not stated as instruction. The final question (`"If today added up to something beyond tasks..."`) is intentionally open-ended to prevent the employee from landing on a pat answer.

---

## How I Designed the Branching

### Trade-off 1: Depth vs. Coverage

A deeper tree (5+ questions per axis) would surface more nuance but fatigue the employee. I chose 2 primary questions per axis with 1 reflection node each, making the session completable in ~8 minutes. Longer isn't better for an end-of-day tool.

### Trade-off 2: Binary vs. Spectrum Routing

The assignment hints at binary routing (internal vs. external). I extended this to three signals: `internal`, `external`, and `mid` — with the mid path representing genuine ambivalence. This avoids forcing people onto poles they don't occupy and produces more honest summaries.

### Trade-off 3: Summary Typing

Instead of one summary, the tree has 4 summary archetypes (VCA, EES, ICM, DEFAULT) keyed to the combination of axis signals. This means the summary text actually reflects the path taken — not just a generic closing. The trade-off is complexity in the decision logic; the benefit is a summary that feels personally observed.

### What Makes the Axes Flow as One Conversation

Each bridge node is written to carry the emotional thread, not just announce the transition. BRIDGE_1_2: *"You've looked at how you moved through today. Now let's look at what you gave."* This connects agency (Axis 1) to contribution (Axis 2) — because a person who takes ownership naturally has something to give. BRIDGE_2_3 connects contribution to radius — because the act of giving widens your view of who you're giving to.

---

## Psychological Sources

| Concept | Source | Application in Tree |
|---------|--------|---------------------|
| Locus of Control | Julian Rotter (1954), *Social Learning and Clinical Psychology* | Axis 1 branching; options designed to distinguish internal attribution from external attribution without labeling them |
| Growth Mindset | Carol Dweck (2006), *Mindset* | A1_Q2_FOLLOWUP — asking what they'd change operationalizes growth mindset vs. fixed mindset framing |
| Psychological Entitlement | Campbell et al. (2004) | A2_Q_ENTITLE_HIGH — designed to surface the "ledger" behavior without naming it pejoratively |
| Organizational Citizenship Behavior | Dennis Organ (1988) | A2_Q_CONTRIB_HIGH — the "beyond your responsibility" question directly operationalizes OCB |
| Self-Transcendence | Maslow (1969), *The Farther Reaches of Human Nature* | A3_R_TRANSCEND reflection text; A3_Q2 closing question |
| Perspective-Taking | Batson (2011) | A3_OPEN options structured as a radius (me → team → colleague → end user) |

---

## What I'd Improve With More Time

1. **Adaptive question text based on earlier answers.** The tree interpolates `{A1_OPEN.label}` in a few places, but a richer system would reference specific options chosen earlier — e.g., if the employee said they "helped a colleague," the Axis 3 opening could name that moment.

2. **Longitudinal tracking.** The most valuable reflection happens over time — not one session, but noticing patterns across 30 days. A streak system or weekly digest comparing axis signals would make the data meaningful.

3. **More mid-branch questions.** Currently, mid-path employees get slightly less tailored reflections. More time would mean designing 2–3 nuanced "middle" paths per axis for employees who genuinely occupy the spectrum.

4. **Employee-controlled depth.** A "go deeper" option on each reflection node — letting the employee choose to explore an axis further before bridging — would serve high-engagement users without fatiguing the rest.

5. **Edge case handling.** The current tree assumes linear progression. A real deployment would need "go back" logic, session-save for interruptions, and handling for employees who flip their answers inconsistently (which is itself meaningful data).
