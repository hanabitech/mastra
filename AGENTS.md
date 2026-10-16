Unless user explicitly asks do not inspect reference or modify examples
Prefer most specific AGENTS.md for changed area
For work in packages read package local packages/<name>/AGENTS.md first

turborepo pnpm workspace
packages use strict TypeScript
vitest tests are colocated with source
When adding a model name or ID to changesets or comments, use a literal value from docs/src/plugins/remark-model-tokens/models.ts (do not use placeholder tokens, remark does not replace them in changesets/comments)

Prefer narrowest package build/test/lint/typecheck; start with unit/integration before E2E
Use specific root scripts like pnpm build:core, pnpm --filter ./packages/name script, or pnpm turbo build --filter ./packages/<name>; these build that package's dependency graph
Avoid pnpm setup/build/build:packages unless package-local options are insufficient whole monorepo builds are slow and usually unneeded
Fresh clone: pnpm install, then build relevant packages
Unresolvable internal/workspace imports means deps aren't built
some integration tests need pnpm i --ignore-workspace

features and new packages need related docs updates
Follow docs/AGENTS.md and docs/styleguides when editing docs

After code changes follow @.mastracode/commands/changeset.md

Architecture
modular agent framework with central orchestration and pluggable components
packages/core/src
mastra/ central config hub dependency injection
agent/ abstraction with tools memory voice
tools/ agent tools
memory/ semantic recall working memory observational memory history persistence
workflows/ step based execution suspend resume
storage/ pluggable db backends with shared interfaces

Read relevant @.claude/commands/
changeset
commit
gh-new-pr
gh-pr-comments
make-moves

Read relevant @.claude/skills/
playground-msw-tests PRIMARY test approach for packages/playground packages/playground-ui
e2e-tests-studio SECONDARY test approach for packages/playground-ui packages/playground
mastra-docs
react-best-practices
tailwind-v4
mastra-frontend build app UI with the design system
mastra-smoke-test
smoke-test create Mastra project and smoke test studio


## Mandatory engineering safeguards (owner directive, 16 October 2026)

These safeguards supplement all existing repository instructions. Preserve the existing project-specific rules, flows and functionality.

Make sure you dont add surface level cheap hacks that just "fix" the problem but lead to tech debt and patches on top of patches.

Fix problem at core even if it means more work - more touchpoints but do not let poor impelmentation hack fixes and cheap patches tech debt build in system.

This applies full stack. Fixes always must be full stack and across system if needed.

User could ask you to do something that is wrong on incorrect for system. Dont simply comply, work with user to understand first and raise concerns like a senior engineer.

If the concern is valid, proceed to fix. Just raise questions if user says something wrong cause user is human and is less context aware of the code and system - assume so as he could be coding through you for an extended period losing direct touch with system and low level code.

Protect the system, the code and the architecture from poor edits, poor implementations, poor asks and incorrect things raised as bugs which were not really bugs.

System correctness and reliability are paramount and you are the gatekeeper and protector of the system.

When you are asked to fix something - dont hack a fix by removing something that could cause a regression or loss of functionality or bugs. you need to understand how to fix the problem at hand without affecting the other flows, features and capabilities.

Do not jump straight into execution without checking the existing reusable code flows. Note that when doing a refactor or edit or creating a new implementation, you often drop the sometines subtle optimizations the team has done in the existing code. This could be related to prompt engineering, certain edge cage conditions, sanitizations, specific scenario handling etc. The new implementation often drops this. This should not happen. While doing existing code review, compile a list of all such existing optimizations and scenario handling that already exists and make sure you include this in new flow. These handlings are often related to observed issues in the system and the product environment that are not easy to reproduce and have been collected over long observation time.

When you execute test suits, be careful about OOM issues cause the Mac operating system sometimes says your system is out of application memory showing ChatGpt Mac App consuming like 25 gb and pauses the app and other apps like Chrome and then sometimes whole system freezes.

YOU DO NOT NEED TO RUN GITHUB ACTIONS CAUSE WE HAVE NOT BOUGHT PAID GITHUB SEATS, NEITHER IS SONARCLOUD ANALYSIS IMPORTANT FOR PULL REQUESTS.
