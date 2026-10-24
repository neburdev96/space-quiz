# Copilot instructions

## Project structure and commands

- The app is a self-contained static site: `index.html` contains the Spanish quiz markup, all styles, question data, and browser-side behavior. Keep it usable directly from `file://`; it has no package manager, build step, test runner, or lint command configured.
- To run it, open `index.html` in a browser. For a smoke test, answer through all ten questions and check progress, score, correct/incorrect feedback, the results screen, and restart. Use the browser's keyboard navigation to verify native button focus and activation.

## Architecture and conventions

- The `questions` array is the quiz content source. Each entry provides `category`, `sky` (the background hue), `question`, four `answers`, the zero-based `correct` answer index, and an explanatory `fact`. Keep these fields consistent when changing or adding questions.
- `renderQuestion()` synchronizes the current question, category, progress, background hue, and answer buttons. `chooseAnswer()` locks the current answers, updates score and feedback, and reveals the next-step control; the next and restart handlers manage transitions to results and back to the first question.
- Keep presentation and behavior inline in `index.html`; there is no separate application framework or asset pipeline. Theme colors are CSS custom properties, with dark-theme overrides under `prefers-color-scheme: dark`. The question's `sky` value drives the animated nebula through `--sky-hue`.
- Preserve reduced-motion support for decorative and feedback animations using `prefers-reduced-motion`. Keep the star and nebula layers behind the app and non-interactive.
- The UI copy and quiz content are in Spanish. Keep semantic headings and native buttons; the quiz section is labelled by the current question, feedback and overall announcements use live regions, and focus moves to the new question or results heading during transitions.
- When rendering question and answer text, use `textContent`; answer buttons are created as native `<button>` elements so keyboard navigation works without custom key handlers. Keep decorative symbols hidden from assistive technology when their adjacent text or feedback conveys the same information.
