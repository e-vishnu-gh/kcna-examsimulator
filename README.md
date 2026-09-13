# KCNA Exam Simulator

A web-based simulator for the Kubernetes and Cloud Native Associate (KCNA) exam.

## Features

- Two sets of questions extracted from KCNA exam dumps
- 60-question exam simulation
- Timer to simulate real exam conditions
- Question navigation
- Optional practice mode: reveals correct (green) / incorrect (red) right after each question, with an explanation, instead of waiting until the end
- Detailed results with correct/incorrect answers
- Explanations for each question

## How to Use

1. Open `index.html` directly in a web browser (double-click it, or use `File > Open`)
2. Choose between Question Set 1 or Question Set 2
3. Answer all 60 questions within the 90-minute time limit
4. Submit your exam to see your results
5. Review your answers and explanations

No local server is required — see [Loading question data](#loading-question-data) below for why.

## Technical Details

- Built with vanilla HTML, CSS, and JavaScript
- No external dependencies required
- Responsive design for desktop and mobile devices

### Loading question data

Question data lives in `data/questionSet1.js` and `data/questionSet2.js` as plain JavaScript
(`const questionSet1Data = [...]`, `const questionSet2Data = [...]`), loaded via ordinary
`<script>` tags in `index.html`, rather than as `.json` files fetched with `XMLHttpRequest`/`fetch`.

This matters because opening `index.html` straight from disk (a `file://` URL) makes the browser
treat every request as coming from a null origin. `XMLHttpRequest`/`fetch` of a `data/*.json` file
gets blocked by CORS in that situation, which is why an earlier version of this app required
running a local server first:

```
npx http-server . -p 8000
# then open http://localhost:8000
```

`<script src="...">` tags aren't subject to that restriction, so loading the data as JS instead of
JSON lets the app work by simply double-clicking `index.html` — no server needed. Running it via a
local server (as above) still works too, if you prefer.

If you need to edit the question data, edit `data/questionSet1.js` / `data/questionSet2.js`
directly — the array literal is just JSON with a `const ... =` prefix and a trailing `;`.

## Project Structure

```
kcna-examsimulator/
├── index.html          # Main HTML file
├── css/
│   └── styles.css      # Styling for the application
├── js/
│   └── app.js          # Application logic
├── data/
│   ├── questionSet1.js  # First set of questions (JS, not JSON — see above)
│   └── questionSet2.js  # Second set of questions (JS, not JSON — see above)
└── README.md           # This file
```

## License

This project is for educational purposes only.
