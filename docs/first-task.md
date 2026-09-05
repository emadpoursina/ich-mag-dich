# First task — build the quiz page

Keep this job tiny. Build **only** the must-have quiz. Do not add sound, hosting, extra languages, or extra pages.

## What to build

One file: `index.html` (CSS and JavaScript inside it). No libraries. No network calls.

The page must cover:

1. Landing — title **Deutsch-Quiz: Was ist das?** and subtitle **Wähle das richtige Wort für jedes Bild!**
2. Three easy picture questions. Wrong answer: **Fast! Versuch es nochmal!** Stay on the same question.
3. After each correct answer, collect a reward word in order: **Ich**, then **dich**, then **mag**.
4. After the third correct answer: confetti, **Gut gemacht! 🎉**, then the words rearrange into **Ich mag dich ❤️**.
5. Then the ask: **Und jetzt die letzte Frage… Willst du mit mir ausgehen?** with **JA!** and **NEIN...**
6. **JA** — **Wann? Freitag oder Samstag?** plus times **18 / 19 / 20 Uhr**. After a day and time: a short confirm such as **Freitag, 19 Uhr — Bis dann! 😊**
7. **NEIN** — sad-gray screen, **Schade... 😢**, **Aber ich tanze für dich!** with a dancing 🕺, then **Tschüss! Bis morgen in der Klasse!**

Follow `docs/prd.md` for look and feel (pastel flashcards, German only, phone-friendly big buttons).

## Locked choices (do not stop to ask)

- Quiz pictures: ☕, 🥨, 🍞. Reward words are always Ich / dich / mag, even if the question is about food.
- Times: Friday or Saturday, 18 / 19 / 20 Uhr.
- Language: German only.
- Phone type: do not worry yet.

## Done when

- `index.html` exists in this folder.
- Opening it shows the landing, then the full yes path and the full no path.
- A wrong quiz tap does not skip ahead.

## Out of scope

Sound, a public web link, English mode, extra word sets, extra files.
