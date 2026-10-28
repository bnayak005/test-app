# Quiz CLI

An interactive command-line programming quiz game built with Node.js. Choose a quiz category, select the number of questions, answer through numbered prompts, and receive immediate feedback, explanations, and a final score.

## Features

- Interactive terminal-based quiz experience
- Quiz category selection
- Configurable number of questions
- Randomized question order using Fisher–Yates shuffling
- Immediate answer feedback
- Explanations for each question
- Progress bar during the quiz
- Final score and performance message
- Review of incorrect answers
- Replay support
- ANSI terminal colors without third-party dependencies

## Technology Stack

- JavaScript
- Node.js 18 or newer
- ES Modules
- Node.js built-in modules:
  - `node:fs/promises`
  - `node:path`
  - `node:url`
  - `node:readline`
- JSON-based quiz content
- ANSI terminal formatting

## Prerequisites

- [Node.js](https://nodejs.org/) `18.0.0` or newer
- npm, included with Node.js

No third-party dependencies are required.

## Installation

Clone the repository and switch to the project directory:

```bash
git clone https://github.com/bnayak005/test-app.git
cd test-app/test-app
```

The project has no external dependencies, so no dependency installation is required. You can run it directly with Node.js.

If you want npm to validate the package configuration, you may run:

```bash
npm install
```

## Running the Quiz

Start the interactive quiz with:

```bash
npm start
```

This is equivalent to:

```bash
node index.js
```

The application will guide you through:

1. Selecting a quiz category
2. Choosing the number of questions
3. Answering each question using numbered choices
4. Reviewing your results and incorrect answers
5. Choosing whether to play again

## Available Categories

The included question data contains the following categories:

- JavaScript Basics
- Node.js Fundamentals
- General Programming

Each category currently contains five questions. Every question includes four answer options, a correct answer, and an explanation.

## Project Structure

```text
.
├── data/
│   └── questions.json   # Quiz categories and questions
├── src/
│   ├── colors.js        # ANSI color and text-style helpers
│   ├── input.js         # Readline prompts and input validation
│   └── quiz.js          # Quiz state, scoring, feedback, and review logic
├── index.js             # Application entry point
└── package.json         # Project metadata and npm scripts
```

## Adding or Updating Questions

Quiz content is stored in [`data/questions.json`](data/questions.json). Questions use the following structure:

```json
{
  "question": "Question text",
  "options": [
    "First option",
    "Second option",
    "Third option",
    "Fourth option"
  ],
  "answer": 0,
  "explanation": "Explanation of the correct answer."
}
```

The `answer` value is a zero-based index:

- `0` refers to the first option
- `1` refers to the second option
- `2` refers to the third option
- `3` refers to the fourth option

Keep four answer options for compatibility with the current interactive menu.

## Testing

The package defines a test command using Node.js’s built-in test runner:

```bash
npm test
```

This runs:

```bash
node --test
```

No test files are currently included in the repository, so there are no discovered automated tests at present.

## Configuration

The application does not require environment variables, external services, databases, or an `.env` file. Configuration and quiz content are contained in:

- [`package.json`](package.json)
- [`data/questions.json`](data/questions.json)

## License

No license file or authoritative license metadata is currently included in the repository. state
The Agent creates a new branch.
The Agent commits the README file.
The Agent opens a Merge Request.
The Merge Request link is stored in the  state. 
