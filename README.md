# Scheduler Quest (React + Tailwind)

CPU scheduling simulator: Priority (preemptive and non-preemptive), SRTF, a challenge mode, and a Research Lab (traditional SRTF vs prediction-assisted scheduling).

## Run
```
npm install
npm run dev
```
Build for production with `npm run build`. Run the tests with `npm test` (Node's built-in runner, Node 18+). The Archivo font loads from Google Fonts, so it needs an internet connection.

## Structure
- `src/engine.js`: scheduling logic (`init`, `tick`, `decision`, `met`)
- `src/data.js`: colours, rules text, challenge levels, speeds
- `src/pages/`: Home, Setup, Sim, Challenge
- `src/components/`: Card, Arena, Gantt, Stats, Bar, Opt (Log is defined but not shown on any screen)
- `src/App.jsx`: page state and navigation
- `src/research/predictive.js`: Research Lab engine (traditional SRTF, prediction-assisted rule, metrics, MAE)
- `src/pages/ResearchLab.jsx`: Research Lab page (presets, predictions, duel lanes, scoreboard)
- `tests/research.test.js`: checks both research methods, the presets and the original engine

## Research Lab in one paragraph
Both methods get the same arrivals and actual bursts, and the same context-switch cost (a CS block in the Gantt chart).
**A · Traditional SRTF** runs the smallest *actual* remaining time and preempts whenever someone is strictly shorter.
**B · Prediction-Assisted** never sees actual bursts. It uses estimated remaining = estimate − executed, where the
estimate starts at the predicted burst and doubles if the process outlives it. A running process is preempted
only if a challenger's estimate is more than θ smaller. A process completes after its *actual* burst.
Predictions come from manual entry, exponential averaging (a heuristic, not ML), or synthetic error. No ANN is implemented.
