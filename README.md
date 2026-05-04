# React Quiz App

A timed React quiz application built with modern React patterns:

- `useReducer` for predictable state transitions
- Context API for global quiz state
- `json-server` as a lightweight local API

This project includes two versions of the app:

- `src/`: Context API version (final refactor)
- `src-no-context/`: pre-context version for comparison

## Features

- Load quiz questions from a local API
- Start, answer, and navigate through multiple-choice questions
- Score tracking with per-question points
- Live progress indicator
- Countdown timer (`30s` per question)
- Auto-finish when time runs out
- High score persistence during the session
- Restart flow after finishing

## Tech Stack

- React 18
- Context API
- `useReducer` + `useEffect`
- `json-server`
- Create React App

## Getting Started

### 1. Install dependencies

```bash
npm install
```

### 2. Start the mock API server

```bash
npm run server
```

This runs `json-server` at:

- `http://localhost:9000/questions`

### 3. Start the React app

In a second terminal:

```bash
npm start
```

Open `http://localhost:3000` in your browser.

## Available Scripts

- `npm start`: Runs the app in development mode.
- `npm run server`: Starts local mock API from `data/questions.json` on port `9000`.
- `npm test`: Launches the test runner.
- `npm run build`: Builds the app for production.

## Project Structure

```text
.
|- data/
|  |- questions.json
|- src/
|  |- components/
|  |- contexts/
|  |  |- QuizContext.js
|- src-no-context/
```

## State Flow (Context Version)

The quiz state is centralized in `QuizContext`:

- Fetch lifecycle: `loading -> ready -> active -> finished`
- Actions handled by reducer:
  - `dataReceived`
  - `dataFailed`
  - `start`
  - `newAnswer`
  - `nextQuestion`
  - `finish`
  - `restart`
  - `tick`

Core derived values:

- `numQuestions`
- `maxPossiblePoints`
- `secondsRemaining`

## Data Format

Questions are stored in `data/questions.json` and follow this shape:

```json
{
  "question": "Which hook to use for an API request on initial render?",
  "options": ["useState", "useEffect", "useRef", "useReducer"],
  "correctOption": 1,
  "points": 10
}
```

## Troubleshooting

- If the quiz stays on loading:
  - Ensure `npm run server` is running.
  - Verify `http://localhost:9000/questions` is reachable.
- If port `9000` is busy:
  - Stop the conflicting process or change the server port and update the fetch URL in `src/contexts/QuizContext.js`.

## Learning Goal

This app demonstrates how to refactor from prop drilling to centralized state with Context API + reducer architecture while keeping UI components focused and reusable.
