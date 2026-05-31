# Active Life — Design Doc

A gamified fitness PWA (installable web app, hosted free on GitHub Pages), modelled on
**Duolingo's mechanics** with a **Jujutsu Kaisen** theme. Goal: improve physical state via
bodyweight strength + flexibility, with game systems that motivate without distorting the training.

> **Status:** concept locked, pre-build. Expert (trainer) input incorporated.
> **Core principle:** the game serves the training, never the reverse.

---

## 1. Win condition — two parallel tracks (equally weighted)

Success is measured on **two independent progress systems**, shown side by side:

| Track | What it rewards | Hero metric |
|---|---|---|
| **Consistency** | Showing up, building the habit | Streak (days the plan was completed) |
| **Capability** | Getting physically stronger / more mobile | Rank (real measurable feats) |

Neither feeds the other. You can have a long streak at a low rank (consistent but easy), or a high
rank with a broken streak (strong but inconsistent). The app surfaces both honestly.

---

## 2. Training model (from trainer)

- **Autoregulated progression** — the *player chooses* when to level up / make the routine harder.
  The app **suggests** a bump based on logged performance ("hit 3×12 for 5 sessions — ready for the
  next grade?") but the player confirms. Guidance, not automation, not pure free choice.
- **One focus per day** — a 7-day rotation, one muscle/movement area per day, with an **optional
  bonus muscle** for extra XP. *(Open Q: confirm which seven areas — likely organized by movement
  pattern: push / pull / legs / core / etc.)*
- **Light days** — player can toggle a light day anytime; it **halves/reduces reps**. Critically, a
  light day **keeps the streak alive**. This is the rest/recovery mechanic — recovery counts as
  training, not as a gap.
- **Flexibility book-ends every session** — mobility as warm-up *and* cooldown.
- **Multiple short sessions/day allowed** — training can be split across the day (morning/noon/night),
  which also suits the flexibility protocol below.

### Flexibility protocol
- Core targets: **pancake + all three splits** (4 exercises).
- Method: **consistency over novelty** — train the *same progressions* repeatedly. Trainer's
  protocol: ~3 min each, morning/noon/night.
- **Pose = measurement, progression = training.** Train the progressions toward each pose; use the
  full poses as periodic tests.
- **Timeline is a goal, NOT a promise.** Trainer estimates ~3–4 weeks with the full protocol, but this
  varies hugely by individual. **Never show a countdown** ("splits in 21 days") — track *range of
  motion improving over time* instead, so a slow week never reads as failure.

### Testing
- Player decides when to test feats. App sends **weekly reminders** to run tests.

---

## 3. Rank ladder (JJK-themed)

Ranks map onto **real measurable feats** (not accumulated XP). One ladder per movement; flexibility
gets its own.

**Push-up ladder (from trainer):**

| Rank | Feat |
|---|---|
| Grade 4 | Knee push-ups |
| Grade 3 | Regular push-ups |
| Grade 2 | Diamond push-ups |
| Grade 1 | One-arm push-ups |
| Special Grade | Handstand push-ups |

**To define:** parallel ladders for pull, legs, core, and flexibility
(e.g. Flexibility Special Grade = full pancake + all 3 splits).

**Path choice:** player picks **Curse** or **Sorcerer** at the start — an identity frame, not just a
skin. *(Open Q: what distinguishes them — e.g. Curse = aggressive/high-volume, Sorcerer =
disciplined/technique? Confirm Victor's intent.)*

---

## 4. Game economy (deliberately constrained)

Duolingo's economy maximizes *time in app*; ours must maximize *training quality*. So:

- **XP = honest record of work done.** No purchasable XP multipliers (hollow for a single player and
  it trains you to game the meta instead of train).
- **Gems → cosmetic unlocks ONLY** — characters, rank-up animations, curse/sorcerer themes. Never
  anything that distorts the training signal.
- **Streak** with light-day protection (see above). Optional Duolingo-style "freeze" for genuine
  missed days.
- **Quests** — the motivational core of the XP tab (e.g. "test your splits this week", "hit a bonus
  muscle 3× this week").

---

## 5. Daily session flow

1. Flexibility **warm-up** (core mobility set).
2. Today's **focus** muscle/movement — at current grade's prescription.
3. Optional **bonus muscle** (extra XP).
4. Flexibility **cooldown** (core mobility set + splits/pancake progressions).
5. **Light-day toggle** available throughout; streak counts if the day's plan was completed.

---

## 6. App layout — 4 bottom tabs (Duolingo-style)

1. **Profile** — path (curse/sorcerer), chosen character, overall rank.
2. **Training** — today's routine, the 7-day rotation, light-day toggle, progression controls.
3. **Quests / XP** — quests, XP, gem spending, cosmetic unlocks.
4. **Progress** — the two tracks side by side: streak/consistency + rank/capability, RoM graphs,
   test history.

---

## 7. Safety messaging (daily, non-negotiable)

- **Muscle effort / burn = expected and fine. Sharp, joint, or stabbing pain = stop immediately.**
  (Tightened from "bearable vs unbearable pain" to clearly separate effort from injury.)
- Always stretch to avoid cramps.
- Breaks are allowed; sessions can be split across the day.

---

## 8. Technical direction

- **Static PWA on GitHub Pages.** Installable on phone, works on any device online, offline-capable.
- **No live AI API calls** — the API key would be exposed in a public static client. Instead:
  **ship a pre-written exercise/stretch library** the app selects from (free, offline, safe). The
  library can be *expanded* offline (e.g. via an LLM) and shipped with the app.
- **localStorage** for all progress/state (match Victor's existing PWA stack — TBD).
- Standard PWA bits: manifest, service worker, app icon.

---

## 9. Open questions / to confirm

1. **Which seven** muscle/movement areas for the daily rotation? (trainer)
2. **Curse vs Sorcerer** — what's the actual difference in the design? (Victor)
3. **Rank ladders** for pull, legs, core, flexibility — define feats per grade.
4. **Existing PWA stack** — what framework/structure do Victor's current GitHub Pages apps use, so
   this matches his world?

---

## Appendix — design decisions & rationale

- **Two equal tracks** chosen over capability-first or consistency-first (Victor's call) — keeps
  habit-building and real strength gains both visible and honest.
- **Light days keep the streak** — resolves the core tension that a daily-output streak fights
  recovery physiology and risks overuse injury.
- **Autoregulated, app-nudged progression** — resolves "increase every 50 days is too rigid"; the
  nudge guards against the opposite failure (never progressing / ego-jumping).
- **Consistency over novelty in flexibility** — adaptation comes from repeating the same
  progressions, not fresh stretches each session.
- **Constrained economy** — game rewards must not distort the training signal.
