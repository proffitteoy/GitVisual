# GitVisual

GitVisual is a browser-side codebase analysis tool. It can analyze both GitHub repositories and local project folders, then render the result as a file tree, code viewer, logs, module list, and panorama graph.

## Current Capabilities

- Analyze project basics: project summary, languages, tech stack, and likely entry files.
- Build a recursive function call chain from the entry flow.
- Filter sub-function analysis to core workflow calls instead of routine string, collection, or boilerplate operations.
- Support object-oriented function names such as `ClassName::method` and class-scoped method lookup.
- Cache repeated function drill-down results and show cache hit or miss status in the log panel.
- Group function nodes into high-level modules, color modules, and filter the panorama by module.
- Support OpenAI-compatible interfaces plus official Anthropic and Gemini interfaces from the settings panel.
- Export the panorama graph as an SVG file.
- Persist the full analysis snapshot to `localStorage`, including:
  - project source and basic info
  - AI analysis result
  - file list
  - function call chain
  - module assignments
  - AI work logs
  - engineering Markdown file
- Restore historical analysis records from the home page.
- Link panorama nodes to source code so clicking a node opens the corresponding file and jumps to the function location.
- Show AI workflow status, request and response payloads, AI call count, input tokens, and output tokens in the log panel.

## Prerequisites

- Node.js 20+
- npm

## Environment

Configure `code/.env.local`:

```env
AI_PROVIDER=""
AI_API_KEY=""
AI_BASE_URL=""
AI_MODEL=""
AI_REVIEW_MODEL=""

DEEPSEEK_API_KEY="YOUR_DEEPSEEK_API_KEY"
DEEPSEEK_BASE_URL="https://api.deepseek.com"
DEEPSEEK_MODEL="deepseek-chat"
DEEPSEEK_REVIEW_MODEL="deepseek-chat"

ANTHROPIC_API_KEY=""
ANTHROPIC_BASE_URL="https://api.anthropic.com"
ANTHROPIC_MODEL=""

GEMINI_API_KEY=""
GEMINI_BASE_URL="https://generativelanguage.googleapis.com/v1beta"
GEMINI_MODEL=""

FUNCTION_ANALYSIS_MAX_DEPTH="2"
KEY_SUB_FUNCTION_LIMIT="10"
GITHUB_TOKEN="YOUR_GITHUB_TOKEN"
```

You can also skip environment variables and configure the provider directly in the app settings.

`AI_PROVIDER` supports `deepseek`, `openai`, `anthropic`, `gemini`, `openrouter`, `ollama`, and `compatible`.

Backward-compatible `DEEPSEEK_*` and `OPENAI_*` variables are still supported.

## Run Locally

1. Install dependencies with `npm install`
2. Start the dev server with `npm run dev`
3. Open [http://localhost:3000](http://localhost:3000)

## Scripts

- `npm run dev`
- `npm run build`
- `npm run preview`
- `npm run lint`

## Analysis Flow

1. Load the GitHub repository tree or the local folder file list.
2. Ask AI for repository summary, languages, tech stack, and entry-point candidates.
3. Verify likely entry files.
4. Recursively analyze key sub-functions only.
5. Cache repeated function drill-down results by file path and line range.
6. Classify function nodes into modules.
7. Save the full result as a historical snapshot and engineering Markdown file in `localStorage`.

## Security

This is still a browser-side app. AI and GitHub credentials are injected into the client bundle at runtime, so the current setup is suitable only for local or private use.

If you plan to deploy it for shared access, move both model requests and GitHub requests behind a backend proxy before using real production credentials.
