# MockDev

MockDev is a technical interview platform that combines interviewer orchestration, a live coding workspace, sandboxed code execution, and session persistence in a single web application.

The system is designed to support structured software engineering interview practice with realistic problem delivery, follow-up questioning, code execution, and end-of-session review.

## What it does

- Runs mock SWE interviews with an AI interviewer that can introduce problems, ask follow-ups, give hints, and adapt tone.
- Supports multiple interviewer modes such as strict interviewer, friendly coach, and FAANG-style pressure mode.
- Provides an in-browser coding workspace with Monaco, language switching, stdin, console output, and hidden test cases.
- Executes code in isolated Docker sandboxes with CPU, memory, process, and network restrictions.
- Persists user sessions, transcripts, hints, code runs, and summaries in Postgres.

## Tech stack

- Next.js
- TypeScript
- Tailwind CSS
- OpenAI APIs
- Monaco Editor
- Postgres
- Docker
- Vercel

## Core product areas

### 1. Interview orchestration

The interviewer is prompt-driven and session-aware. It keeps track of:

- current problem
- transcript
- prior hints
- selected language
- execution history
- interview mode and difficulty

It can answer commands like:

- `give me a hint`
- `repeat the question`
- `what do you think of my approach?`
- `am I missing an edge case?`
- `can you ask a follow-up?`

### 2. Coding workspace

The interview workspace includes:

- Monaco editor
- language selection for Python, JavaScript, Java, C++, and Go
- run with stdin
- hidden and visible test cases
- per-question starter templates
- console output and compile/runtime feedback

### 3. Secure code execution

Each execution runs inside a restricted Docker container with:

- no outbound network access
- strict timeout limits
- CPU and memory caps
- PID limits
- compile/runtime error reporting

### 4. Persistence and auth

The application uses a Postgres-backed session model plus lightweight cookie auth:

- route protection
- Zod request validation
- parameterized SQL
- per-user session history
- interview summaries and replayable prior sessions

## Architecture

```mermaid
flowchart LR
  A["Next.js frontend"] --> B["Interview session APIs"]
  A --> C["Code runner API"]
  B --> D["Interviewer orchestration"]
  B --> E["Postgres session store"]
  C --> F["Docker sandbox"]
  D --> G["OpenAI models"]
```

## Design priorities

- Clear separation between frontend, orchestration, persistence, and execution layers
- Safe handling of untrusted user code through isolated containerized execution
- Session-aware interviewer behavior rather than stateless chat responses
- Extensibility across languages, question sets, and interview modes

## Repository scope

This repository is the public project overview for MockDev. It documents the system architecture, feature set, and implementation approach without exposing private environment configuration or internal development history.

## Live demo

- App: [interview-prepper-seven.vercel.app](https://interview-prepper-seven.vercel.app)
