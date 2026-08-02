# AGENTS.md

## Cursor Cloud specific instructions

### What this repository is

This is a **documentation / prompt repository**, not a software project. It contains a
Chinese-language, AI-assisted **novel-writing workflow** ("小说创作工作流"). The entire
repo is Markdown (`*.md`) plus `.gitignore` — there is **no application code, no
`package.json`/`requirements.txt`, no build system, no automated tests, and no lint
configuration**.

Because of that:

- There is **nothing to install, build, compile, or `npm run`/`pip install`**. The
  update script is intentionally a no-op.
- Do **not** add tooling (e.g. `markdownlint`, a `package.json`, a linter) — the repo
  deliberately has none, and adding it would introduce infrastructure that is not part
  of the codebase.
- The only real runtime dependency of the workflow is **`git`** (version control is a
  core step of the workflow — see "章后回灌 → git commit").

### The "application" and how to run it

The "application" is the workflow itself: an AI agent reads the templates and the two
**skills**, then produces / reviews novel content. Authoritative docs (follow these if
present, in this priority):

- `工作流手册.md` — the 7-phase workflow (立项 → 创作契约 → 世界观 → 角色 → 总纲 → 卷纲/章纲 → 正文 → 修订).
- `使用说明.md` — step-by-step operator guide with copy-paste prompts.
- `skills/novel-writing-workflow/SKILL.md` and `skills/novel-quality-review/SKILL.md` —
  the two SOP skills that drive writing and review.

Key non-obvious rule for "running" (writing) correctly: every time you generate 正文,
you MUST pack the **four-piece context** — `07_文风规范` + the chapter's `04_章纲/*` +
the on-stage `02_角色/*` character cards + `06_章节摘要.md` (the summary, **never** the
full prose). See `工作流手册.md` → "AI 协作三机制 / 上下文打包".

### Layout notes

- Top-level numbered folders (`01_世界观`, `02_角色`, `03_大纲`, `04_章纲`, `05_正文`, ...)
  and top-level `*_模板.md` files are **templates / scaffolding** for a new book.
- `试跑_东宫IF/` is a **completed worked example** (a finished IF fan-fiction) that
  exercises the whole workflow end-to-end — use it as a reference for what "done" looks
  like. Treat it as read-only reference material.
- All content is in Chinese.

### Verifying the environment works

There is no server or GUI. A meaningful smoke test is to exercise the workflow's
decision-gate action — generate a short `文风样例` (style sample) that obeys
`07_文风规范` while packing the four-piece context — and confirm `git` versioning works
(`git status`, `git log`). Do this in a scratch location; do not commit generated
demo prose into the workflow repo.
