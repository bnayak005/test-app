# Quiz CLI

An interactive command-line quiz game for learning JavaScript. The application presents multiple-choice questions by category, provides immediate feedback and explanations, tracks score and progress, reviews incorrect answers, and supports replaying the quiz.

## Features

- Interactive terminal-based quiz experience
- Category selection: JavaScript Basics, Node.js Fundamentals, General Programming
- Configurable number of questions
- Shuffled question and answer flow
- Immediate answer feedback
- Explanations for questions
- Score and progress tracking
- Review of incorrect answers
- Option to replay the quiz
- ANSI terminal formatting without external packages
- Question data stored in JSON for customization

## Prerequisites

- Node.js 18 or later
- An interactive terminal
- Unicode and ANSI color support recommended

No runtime dependencies, environment variables, database, or external service is required.

## Installation

After cloning, the application is located in the nested `test-app/` directory:

```bash
git clone https://github.com/bnayak005/test-app.git
cd test-app/test-app
npm install
```

`npm install` is optional because the project has no dependencies; it is harmless and confirms the package metadata is usable.

## Running the Quiz

From `test-app/test-app/`:

```bash
npm start
# equivalent: node index.js
```

The flow displays a banner, asks you to choose a category and question count, presents answers for each question, gives immediate feedback and explanations, shows results and incorrect-answer review, and offers to replay.

## Question Data and Customization

Questions are stored in `data/questions.json`. The current data has five questions in each of these categories: JavaScript Basics, Node.js Fundamentals, and General Programming.

Each question uses this shape:

```json
{
  "question": "What keyword declares a constant in JavaScript?",
  "options": ["var", "let", "const", "define"],
  "answer": 2,
  "explanation": "const declares a block-scoped constant."
}
```

To customize the quiz, edit `test-app/data/questions.json` while preserving valid JSON, the expected fields, and a zero-based `answer` index. Keep the file at that path so the application can load it.

## Project Structure

```text
test-app/
├── data/questions.json  # Categories and question content
├── src/colors.js        # ANSI terminal formatting helpers
├── src/input.js         # Readline input and validation helpers
├── src/quiz.js          # Quiz state, scoring, and presentation
├── index.js             # Application entry point and orchestration
└── package.json         # Project metadata and npm scripts
```

## Implementation and Architecture

- `index.js` loads the JSON data, presents the category and question-count choices, orchestrates the quiz loop, and handles replay and top-level errors.
- `src/quiz.js` manages quiz state, scoring, progress, answer feedback, results, and review of incorrect answers.
- `src/input.js` provides readline-based prompts, selection validation, confirmation, and pause helpers.
- `src/colors.js` provides ANSI formatting without a third-party package.
- `data/questions.json` contains the editable question content.

The project uses native ES modules (`"type": "module"`), `async`/`await` and promises, Node.js filesystem and readline APIs, classes, array methods, destructuring, template literals, and error handling. It has no external packages.

## Available npm Scripts

Run these commands from `test-app/test-app/`:

- `npm start` — runs `node index.js`.
- `npm test` — runs Node’s built-in test runner with `node --test`.

## Testing Status

Testing is configured through `npm test`, but no test files or test directories currently exist. Consequently, the repository has no automated test coverage results. There is no CI workflow.

## Dependencies

The application has no external dependencies and uses Node.js built-in APIs only. There is no lockfile and no build configuration.

## Deployment

This is a local interactive CLI application. No deployment configuration is included.

## License Notes

`package.json` identifies the project as MIT licensed. No `LICENSE` file was found, so the full license text is not included in this repository.
