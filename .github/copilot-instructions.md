# Space Quiz Project Guidelines

## Build and validation

- The app is a dependency-free static document. There is no package manifest, build step, test runner, or linter; do not introduce tooling or a server unless explicitly requested.
- Run the app by opening `index.html` directly with a `file:///` URL in the VS Code integrated browser.
- Validate changes in the browser. Exercise one correct answer, one wrong answer, next-question navigation, the tenth-question result screen, and restart.
- For interaction or accessibility changes, also verify Tab focus, number keys 1-4, Enter navigation, the progress bar's `aria-valuenow`, live feedback, dark mode, and reduced-motion behavior.
- There is no automated single-test command. Use the smallest relevant browser interaction as the focused test.

## Architecture

- `index.html` is the complete application: the first inline script selects the light/dark theme, the inline stylesheet defines all presentation and animation, semantic HTML provides the quiz and result screens, and the final inline script owns data and behavior.
- `questions` is the content model. Each item has `category`, `question`, four `answers`, a zero-based `correct` index, and `explanation`.
- The app is a small state machine driven by `currentIndex`, `score`, and the per-question `responses` array. `renderQuestion` rebuilds answer buttons and restores prior feedback, `selectAnswer` locks and grades the current question once, navigation moves among unanswered or selected questions, `showResults` switches screens only after every response, and `restartQuiz` resets state.
- The quiz and result views coexist in the document and switch via the `hidden` attribute. Keep score text, progress text/bar/ARIA state, feedback, and focus movement synchronized with state transitions.

## Project conventions

- Keep the artifact self-contained: use inline CSS and JavaScript, browser-native APIs, and no external assets, network requests, storage, frameworks, or dependencies.
- UI copy is Korean. Preserve the existing space-mission tone and concise answer explanations.
- Use only the existing `--cp-*` custom properties for colors. Maintain both `:root` and `html[data-theme="dark"]` values when adding a theme token.
- Preserve the early theme-detection script before other JavaScript so the initial render uses `scoutTheme` when supplied and otherwise follows `prefers-color-scheme`.
- Maintain accessibility behavior: semantic buttons, visible `:focus-visible` styles, `aria-live` score/feedback, progressbar attributes, descriptive answer labels, focus movement after transitions, and the `prefers-reduced-motion` override.
- Answer buttons are generated with DOM APIs and user-visible values are assigned with `textContent`; continue this pattern rather than inserting HTML strings.
- The number-key handler and button labels assume exactly four answers per question. If the answer count changes, update both keyboard behavior and the visible hint.
- The experience is intentionally ten questions. The `/ 10` labels, progressbar maximum, result percentage calculation, and `questions` length must remain consistent if the quiz size changes.
