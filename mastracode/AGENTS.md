Packages: `mastracode/sdk` (`@mastra/code-sdk`), `mastracode/tui` (`mastracode`), `mastracode/factory-ui` (`@internal/factory-ui`), and standalone `mastracode/web`. Scope commands to the changed package.

TUI: build deps with `pnpm build:mastracode`; test SDK+TUI with `pnpm test:mastracode`; typecheck with `pnpm --filter ./mastracode/tui check`; lint with `pnpm --filter ./mastracode/tui lint`. Build first before broad tests.

Focused TUI test: `pnpm --filter ./mastracode/tui exec vitest run <test-file> --reporter=dot --bail 1`.

Factory UI is the independent React SPA and CLI UI artifact; see `mastracode/factory-ui/AGENTS.md`.

Tests are colocated in package `src`. TUI scenarios: `mastracode/tui/e2e/tui/`; fixtures: `mastracode/tui/e2e/fixtures/`. Use `e2e:list`, `e2e:smoke`, or `e2e:test -- --reporter=dot`; focus with `MC_E2E_VITEST_SCENARIOS=<scenario> pnpm --filter ./mastracode/tui exec vitest run --config e2e/vitest.config.ts --reporter=dot`.

Use `testing-mastracode-tui` for interactive guidance and `mastracode/tui/e2e/README.md` for runner commands. TUI-visible behavior needs checked-in TUI E2E coverage. Sanitize any read-only local Application Support data into deterministic AIMock fixtures.


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
