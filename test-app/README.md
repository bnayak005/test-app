# Quiz CLI

An interactive command-line quiz game for learning JavaScript, Node.js, and general programming concepts.

## Overview

Quiz CLI is a dependency-free Node.js application that presents multiple-choice questions in an interactive terminal session. Players choose a category, select the number of questions, answer each question by entering an option number, receive immediate feedback and explanations, and review their results at the end.

The repository is also an example of modern JavaScript development with ES modules, asynchronous programming, Node.js file-system APIs, classes, and terminal input handling.

## Features

- Three built-in quiz categories:
  - JavaScript Basics
  - Node.js Fundamentals
  - General Programming
- Choice of all available questions, three questions, or five questions when enough questions exist.
- Randomized question order for each quiz.
- Immediate correct/incorrect feedback and explanations.
- Progress bar and score percentage.
- Review of incorrect answers after the quiz.
- Option to play multiple quizzes in one session.
- ANSI-colored terminal output without external runtime dependencies.

## Requirements

- Node.js 18.0.0 or newer.
- A terminal capable of displaying standard ANSI escape codes.

No npm packages are required by this project.

## Installation and setup

Clone the repository and enter the application directory:

```bash
git clone <repository-url>
cd test-app
```

The project has no dependencies to install. If you want npm to validate the manifest and create local npm metadata, run:

```bash
npm install
```

Because the application uses only Node.js built-in modules, it can also be run directly after cloning.

## Usage

Start the interactive quiz with the defined npm script:

```bash
npm start
```

Or invoke the entry point directly:

```bash
node index.js
```

During a session:

1. Choose a category by entering its menu number.
2. Choose all questions, three questions, or five questions where available.
3. Press Enter to begin.
4. Enter the number corresponding to your answer for each question.
5. Press Enter between questions when prompted.
6. Review the score and missed questions.
7. Enter `y` or `n` when asked whether to play again.

Example interaction (representative):

```text
Choose a category:

  1. JavaScript Basics
  2. Node.js Fundamentals
  3. General Programming

Your choice (enter number): 1
```

Invalid menu numbers are rejected until a number within the displayed range is entered. Confirmation accepts responses beginning with `y` as yes; all other responses are treated as no.

## Project structure

```text
test-app/
├── data/
│   └── questions.json   # Categories, questions, answer indexes, and explanations
├── src/
│   ├── colors.js        # ANSI color and text-style helpers
│   ├── input.js         # readline interface and interactive prompts
│   └── quiz.js          # Quiz class, shuffling, scoring, and result display
├── index.js              # Application entry point and main game loop
├── package.json          # Project metadata, scripts, and Node.js requirement
└── README.md             # Project documentation
```

## Architecture and implementation

The application is an ES module project (`"type": "module"` in `package.json`) with a small separation of concerns:

- `index.js` creates the readline interface, loads `data/questions.json` with `node:fs/promises`, displays the category and question-count menus, and controls the overall play-again loop.
- `src/input.js` wraps Node.js `readline` callbacks in Promises and provides reusable selection, confirmation, and pause prompts.
- `src/quiz.js` contains the `Quiz` class. It copies and shuffles the selected questions with the Fisher–Yates algorithm, tracks progress and answers, evaluates responses, and renders results.
- `src/colors.js` provides ANSI escape-code helpers for status messages, headings, feedback, and progress text.
- `data/questions.json` is the content source. Each question stores its text, an array of options, a zero-based correct-answer index, and an optional explanation.

At startup, the JSON file is resolved relative to `index.js`, so running the application from another working directory still uses the repository's bundled question data.

## Question data format

Questions are grouped under a top-level `categories` object. A category has a display `name` and a `questions` array. Each question follows this shape:

```json
{
  "question": "Question text",
  "options": ["First option", "Correct option"],
  "answer": 1,
  "explanation": "Why the answer is correct."
}
```

`answer` is a zero-based index into `options`. For example, `answer: 0` selects the first option and `answer: 2` selects the third. When adding questions, keep this index aligned with the options array.

The current data contains five questions in each of the three categories, so all three question-count choices are available for every category.

## Available npm scripts

| Command | Description |
| --- | --- |
| `npm start` | Runs `node index.js` and starts the interactive quiz. |
| `npm test` | Runs Node.js's built-in test runner with `node --test`. |

## Testing

Run the repository-defined test command:

```bash
npm test
```

No test files are currently included in the repository, so the built-in test runner has no project-specific test cases to execute. The command is retained as the project's test entry point.

## Configuration

There are no environment variables, configuration files, database migrations, network services, or external API credentials used by the application.

To change quiz content, edit [`data/questions.json`](data/questions.json). To change interaction behavior, update [`index.js`](index.js), [`src/input.js`](src/input.js), or [`src/quiz.js`](src/quiz.js). Terminal styling is defined in [`src/colors.js`](src/colors.js).

## Error handling and limitations

- Failure to read or parse `data/questions.json` is caught by the main application, printed with an error message and stack trace, and exits with status code 1.
- The application is terminal-only; it does not provide a web interface, HTTP API, persistence, user accounts, or score history.
- Scores exist only for the current quiz session.
- Questions are selected from the beginning of the category list before being shuffled; the selected subset is randomized, but the application does not randomly sample from the full category when a three- or five-question quiz is chosen.
- The interface assumes a terminal that supports ANSI color and Unicode box-drawing/progress characters. Colors are not configurable or disabled by a command-line option.
- There is no automated test coverage in the current repository.

## Development notes

The codebase uses built-in Node.js modules only, including `node:fs/promises`, `node:path`, `node:url`, and `node:readline`. It uses asynchronous functions and Promises for file loading and terminal input. No formatter, linter, bundler, Docker configuration, or CI/CD workflow is present.

When making changes, preserve the question-data contract described above and verify the interactive flow manually with:

```bash
npm start
```

## License

The project declares the [MIT License](https://opensource.org/licenses/MIT) in `package.json`. No separate `LICENSE` file is included in the repository.

## Documentation gaps

The repository does not define a canonical public clone URL, supported operating-system list, terminal compatibility matrix, contribution guidelines, release process, or CI workflow. Those details should be added by maintainers if they become part of the supported project workflow.
