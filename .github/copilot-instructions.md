# Orbit space quiz

## Running and checking

Open `index.html` directly in a browser using a `file://` URL. Keep the app
self-contained: HTML, CSS, JavaScript, and SVG artwork all live in this file,
with no server, external resources, or dependencies.

Use the integrated browser for interaction checks:
- Single-question check: choose a wrong answer on question 1; confirm red shake,
  the correct answer highlighted green, an explanation, score 0, and progress 1/10.
  Further answer attempts must not change the score.
- Complete a run to check final score, accuracy, and the emoji result. Result
  tiers start at 5 and 8 correct answers. Replay must reset score and progress.
- Check number keys 1-4, keyboard focus, narrow layouts, light/dark appearance,
  and reduced-motion behavior when changing the corresponding UI.

## Application structure and state

The head contains an early theme-selection script and all styles. The body
contains the quiz and initially hidden results panel. The final script defines
question data, renders answer buttons, and wires navigation and keyboard events.

`questions` entries contain `category`, `question`, four `answers`, a zero-based
`correct` index, and `explanation`. Keep the quiz at 10 questions; some visible
labels and the progress maximum explicitly use 10.

`index`, `score`, and `answered` are in-memory state:
- `renderQuestion()` rebuilds answer buttons and clears question feedback.
- `selectAnswer()` locks the question before updating score, feedback, and
  progress. Progress counts answered questions, not the displayed question number.
- The Next handler advances only after an answer; after the last answer it
  calls `showResults()`. Results replace the quiz within the same card.
- The restart handler resets state and renders the first question.

## UI conventions

Use the existing Clawpilot `--cp-*` CSS variables for component and SVG colors.
Light values are in `:root`; dark overrides use `html[data-theme="dark"]`.
Theme selection runs before rendering, considers `scoutTheme` in the URL, and
otherwise follows `prefers-color-scheme`; the media-query listener handles
subsequent system changes when no URL override is present.

Keep the centered 504px maximum-width column, 15px sans-serif body text,
Segoe UI/Aptos font stack, and 540px responsive breakpoint. Correct answers
use `.correct` with a green pop; incorrect selections use `.wrong` with a red
shake. Animation and transition changes must retain the reduced-motion override.

Use the `$()` ID lookup helper and existing DOM IDs when extending handlers.
Question and answer text is inserted using `textContent`; existing `innerHTML`
assignments are limited to app-owned markup and numeric state.

Visibility is controlled with `hidden`, backed by `[hidden] { display: none
!important; }`. Preserve native answer buttons, the answer group's heading
association, live feedback/score announcements, textual correctness labels,
and focus movement to Next, the new question, or the result heading.
Number-key shortcuts ignore repeats and modifier combinations and stop after
the current question is answered.
