# Product Requirements Document: "Ich mag dich" — The Hidden-Message Quiz

**Version:** 1.0
**Date:** 2026-08-27
**Status:** Draft
**Author:** Hermes Agent (PRD Writer), based on discovery with the user

---

## 1. Executive Summary

"Ich mag dich" is a single-page web game disguised as a German A0 vocabulary exercise. The recipient opens what looks like an innocent three-question flashcard quiz ("Deutsch-Quiz: Was ist das?"); after answering all questions correctly, the three German words she has "won" — **Ich**, **dich**, **mag** — magically rearrange into **"Ich mag dich"** (I like you), followed by the real ask: **"Willst du mit mir ausgehen?"** (Do you want to go out with me?). Answering **JA** opens a tiny Fri/Sat time-picker; answering **NEIN** triggers a playful, self-deprecating "dance" screen so rejection costs no awkwardness. Built as a zero-dependency static HTML/CSS/JS page, mobile-first, and intended as a disposable one-off delivered as a link.

## 2. Business Model

| Element | Detail |
|---------|--------|
| **Who** | One specific adult German A0 learner — the user's classmate ("she"); secondary user is the sender ("he"), who is testing the Hermes PRD pipeline on this project |
| **Problem** | Asking a classmate out playfully and without awkwardness, in the context of a shared German class |
| **Solution** | A study-tool disguise that lets her "discover" the message herself, plus a graceful, funny rejection path |
| **Name** | "Ich mag dich" (working title; bait-page title is "Deutsch-Quiz: Was ist das?") |

Not a commercial product: personal one-off, no monetization.

## 3. User Personas

### Primary Persona: She — the A0 Classmate

- **Who they are**: A German A0 learner, classmate of the sender; comfortable with ~10 basic food/activity words (Ich, dich, mag, ausgehen).
- **Goals**: Do the "exercise," feel good about knowing the answers, be delighted.
- **Pain points**: Believes it's homework-adjacent; must not feel quizzed or pressured.
- **Context**: Opens a link on her phone, likely during free time; one sitting, under 2 minutes.

### Secondary Persona: He — the Sender

- **Who they are**: The user; speaks enough German to craft the copy and wants a low-pressure, memorable ask.
- **Goals**: Deliver the question in a way that is sweet, surprising, and never humiliating either way.
- **Pain points**: Rejection awkwardness; the reveal falling flat.
- **Context**: Wants to ship this as part of testing a disposable pipeline project.

## 4. User Journeys

### Journey 1: The Happy Path (JA!)

1. She opens the link on her phone → sees "Deutsch-Quiz: Was ist das?" with a cute study-tool look.
2. She answers 3 super-easy A0 questions ("Wähle das richtige Wort für jedes Bild!"); wrong answers get gentle retry feedback.
3. After the 3rd correct answer, confetti/sparkles fire — "Gut gemacht! 🎉".
4. Her three reward words appear — **Ich**, **dich**, **mag** — and rearrange into **"Ich mag dich" ❤️**.
5. "Und jetzt die letzte Frage…" → **"Willst du mit mir ausgehen?"** with **JA!** / **NEIN...** buttons.
6. She taps **JA** → a cheerful picker: "Wann? Freitag oder Samstag?" plus time options.

### Journey 2: The Kind Rejection Path

1–5. Same as above through the ask.
6. She taps **NEIN...** → screen goes sad-gray: "Schade... 😢".
7. "Aber ich tanze für dich!" — a silly animated dancing emoji (🕺/wiggly cat).
8. "Tschüss! Bis morgen in der Klasse!" — no hard feelings, framed as a joke.

### Journey 3: The Stuck Quiz (minor)

- She answers incorrectly → inline feedback ("Fast! Versuch es nochmal!") with the option retried until correct; she can always reach the reveal.

## 5. Feature Set

### MVP (Must-Have)

| # | Feature | Description | Priority |
|---|---------|-------------|----------|
| F1 | Bait landing screen | "Deutsch-Quiz: Was ist das?" + subtitle + cute study-tool icon (coffee cup/pretzel emoji) | P0 |
| F2 | 3-question quiz | Emoji prompt, 3 German options each, tap-to-answer, instant gentle feedback, retry until correct | P0 |
| F3 | Word rewards | Each correct answer collects one of Ich / dich / mag as a visible "reward" | P0 |
| F4 | Reveal sequence | Confetti + "Gut gemacht! 🎉" → reward words rearrange into "Ich mag dich" ❤️ | P0 |
| F5 | The Ask | "Und jetzt die letzte Frage… Willst du mit mir ausgehen?" with JA! / NEIN... | P0 |
| F6 | Yes branch | "Wann? Freitag oder Samstag?" + time options | P0 |
| F7 | No branch | Sad-gray screen, "Schade... 😢", dance animation, "Tschüss! Bis morgen in der Klasse!" | P0 |

### V1.1 (Should-Have)

| # | Feature | Description | Priority |
|---|---------|-------------|----------|
| F8 | Sound | Tiny optional pling on correct answers / reveal (off by default) | P1 |
| F9 | Shareable link | Static hosting (Vercel/Netlify) so the link opens anywhere | P1 |

### Future (Nice-to-Have)

| # | Feature | Description | Priority |
|---|---------|-------------|----------|
| F10 | Question-set variants | More word sets for other messages | P2 |
| F11 | German/English mode toggle | For non-A0 friends | P2 |

## 6. Page / Screen List

Single-page app — screens are states, all in one `index.html`:

```
/
└── index.html (one page, state machine)
    ├── State: landing   ("Deutsch-Quiz: Was ist das?")
    ├── State: quiz      (3 question screens, one at a time)
    ├── State: reveal    (confetti → words → rearrange → "Ich mag dich")
    ├── State: ask       (JA! / NEIN...)
    ├── State: yes       ("Wann? Freitag oder Samstag?" + times)
    └── State: no        (sad screen → dance → "Bis morgen!")
```

## 7. Functional Requirements

### F1: Bait Landing Screen

**User Story:** As a recipient, I want the page to look like a normal study exercise, so that the surprise stays hidden.

**Acceptance Criteria:**
1. WHEN the page loads, THE System SHALL display the title "Deutsch-Quiz: Was ist das?" and the subtitle "Wähle das richtige Wort für jedes Bild!".
2. WHEN the landing is shown, THE System SHALL NOT display any words from the hidden message outside the quiz flow.

### F2: Three-Question Quiz

**User Story:** As a recipient, I want three easy A0 questions with instant feedback, so that I stay engaged and always finish.

**Acceptance Criteria:**
1. WHEN the quiz starts, THE System SHALL present exactly 3 questions, each with one emoji prompt and 3 German word options.
2. WHEN the recipient taps a correct option, THE System SHALL advance to the next question (or reveal) and add the word to her rewards.
3. WHEN the recipient taps a wrong option, THE System SHALL show gentle inline feedback ("Fast! Versuch es nochmal!") and keep the question active.
4. WHEN the recipient is on a question, THE System SHALL accept only taps on the 3 options (one answer per question).

### F3: Word Rewards

**User Story:** As a recipient, I want each correct answer to visibly collect a word, so the reveal feels earned.

**Acceptance Criteria:**
1. WHEN a question is answered correctly, THE System SHALL append the reward word (Ich → dich → mag, in order) to a visible collection area.

### F4: Reveal Sequence

**User Story:** As a recipient, I want the words to rearrange into "Ich mag dich" with celebration, so the message is unambiguous and delightful.

**Acceptance Criteria:**
1. AFTER the 3rd correct answer, THE System SHALL show confetti/sparkles and "Gut gemacht! 🎉".
2. WHILE the reveal is showing, THE System SHALL animate the words Ich, dich, mag rearranging into "Ich mag dich" with a heart (❤️).
3. WHEN the reveal finishes, THE System SHALL automatically transition to the ask screen.

### F5: The Ask

**User Story:** As a recipient, I want a clear final question with two options, so I can answer honestly with one tap.

**Acceptance Criteria:**
1. WHEN the reveal completes, THE System SHALL display "Und jetzt die letzte Frage…" and "Willst du mit mir ausgehen?" with two buttons: **JA!** and **NEIN...**.
2. WHEN the recipient taps JA!, THE System SHALL show the yes screen (F6).
3. WHEN the recipient taps NEIN..., THE System SHALL show the no screen (F7).

### F6: Yes Branch

**User Story:** As a recipient, I want to pick a day and time easily, so saying yes is frictionless.

**Acceptance Criteria:**
1. WHEN the yes screen is shown, THE System SHALL display "Wann? Freitag oder Samstag?" with day options and a set of time options.
2. WHEN a day and time are selected, THE System SHALL display a confirmation ("Freitag, 19 Uhr — Bis dann! 😊" or similar).

### F7: No Branch

**User Story:** As a recipient, I want rejection to be light and funny, so there's no awkwardness.

**Acceptance Criteria:**
1. WHEN the no screen is shown, THE System SHALL display "Schade... 😢" on a sad-gray background.
2. WHEN the no screen is shown, THE System SHALL display "Aber ich tanze für dich!" with an animated dancing emoji 🕺.
3. WHEN the dance plays, THE System SHALL display "Tschüss! Bis morgen in der Klasse!" as the final line.

## 8. Non-Functional Requirements

1. THE System SHALL run entirely client-side with zero dependencies, no build step, and no network calls (works over `file://` or any static server).
2. WHEN viewed on a phone viewport (≤ 480 px wide), THE System SHALL remain fully usable with thumb-sized tap targets (≥ 44 px).
3. THE System SHALL load and become interactive in under 1 second on a typical phone over 4G.
4. THE System SHALL NOT collect, store, or transmit any personal data.
5. THE System SHALL render correctly in current iOS Safari and Android Chrome without browser extensions.

## 9. Tech Stack Recommendations

| Layer | Choice | Rationale |
|-------|--------|-----------|
| App | Single `index.html` with inline CSS + vanilla JS | Zero-dependency, opens anywhere, trivially disposable; state machine is ~6 screens |
| Graphics | Emoji + CSS animations (confetti via CSS keyframes) | No image assets, renders fine on phone, fits pastel flashcard look |
| Serving | Local static server for the test; Vercel/Netlify static drop for the real link | Same artifact deploys to either with zero changes |
| Versioning | git repo in `/workspaces/ich-mag-dich` | Free baseline; pipeline test |

## 10. Design Direction

Cute minimal pastel flashcard aesthetic — soft cream/rose background, rounded cards, chunky friendly typography, emoji-driven art (☕ / 🥨 on the bait page). The bait screen must read as a school exercise: simple, clean, slightly corporate-quiet. The reveal is the big moment: confetti burst, warm gradient, the three words sliding into "Ich mag dich ❤️". Buttons are large pastel pills; the NEIN button is smaller and muted so the intent gradient is gentle. German copy throughout, matching A0 vocabulary.

## 11. Success Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| Quiz completion (reaches reveal) | 100% of the time she opens it | Manual observation; optional `console.log`/URL-hash state trail |
| Ask answered (JA or NEIN tapped) | 100% of reveals | Same state trail |
| Load + interactive time | < 1 s | DevTools throttling test on phone preset |
| Zero broken states on her phone | All states reachable | Pre-send device test on iOS Safari + Android Chrome |

## 12. Risks and Assumptions

| Risk / Assumption | Impact | Mitigation |
|-------------------|--------|------------|
| She answers a question wrong and feels dumb | Medium | Only 3 easy A0 questions; gentle "Treib es nochmal!" feedback; correct-first design |
| She closes the tab before the reveal | High | Quiz is 3 taps; every tap gives dopamine (correct + reward word appears immediately) |
| The message is ambiguous ("is this a joke?") | Medium | "Und jetzt die letzte Frage…" + heart + direct wording makes intent explicit |
| Emoji render differently on her phone | Low | Use common emoji (☕🥨🍞🥛🧃); verify on device before sending |
| She wants to say yes but can't pick a time | Low | Default-friendly options; easy confirm |
| Assumption: she knows Ich / dich / mag from class | — | They're the first ~50 A0 words; if unsure, swap reward words while keeping the message |
| Disposable project — no one will maintain it | — | Accepted by design; static file outlives any repo |

## 13. Open Questions

1. Which 3 quiz questions should earn the reward words? (Need prompts whose *rewards* are Ich/dich/mag — e.g., reward words shown after each correct answer regardless of prompt, or word-per-question mapping.)
2. What time options should the Yes calendar offer? (Default: 18, 19, 20 Uhr on Freitag/Samstag.)
3. Should the quiz questions relate to the reward words at all, or are rewards purely decorative per the final "Magic Word" design?
4. iOS or Android for her phone? (Affects emoji/confetti QA priority.)
5. German-only UI confirmed? (Assumed yes.)
