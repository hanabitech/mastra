Build from root: pnpm build:playground-ui
Test from root: pnpm --filter ./packages/playground-ui test
Typecheck: pnpm --filter ./packages/playground-ui typecheck (standalone `tsc`)

`build` is `vite build` only; vite-plugin-dts emits declarations and gates type
errors via the `afterDiagnostic` hook in vite.config.ts. Use the `typecheck`
script for an explicit `tsc` gate (CI runs turbo `typecheck`). The package's own
build is ~8s; a slow `build:playground-ui` is the cold turbo cache rebuilding
upstream deps (`^build`), not this package.

PRIMARY testing strategy: Vitest + MSW + typed @mastra/client-js fixtures.
This is the #1 way to validate changes here — ABOVE Playwright E2E.
Use the `playground-msw-tests` skill for business hooks, data components,
gating, and React Query flows.

After tests pass, mutation testing is mandatory on exactly the production
`.ts`/`.tsx` files the task changed (none changed = skip):
`pnpm --filter ./packages/playground-ui test:mutate "src/foo.ts,src/bar.tsx"`.
No dirs/globs, no unrelated files, no direct `stryker run`, no
tests/fixtures/generated/config/docs. Strengthen the TDD/BDD tests to kill
survivors (never weaken assertions); report truly equivalent/unreachable ones.

Rules:

- Drive the real @mastra/client-js + React Query stack; only mock the network.
- Never `vi.mock` our own data hooks, services, or auth gating.
- Fixtures live in nearby `__tests__/fixtures/` folders and MUST be typed with
  response types re-exported from @mastra/client-js.

Use Playwright E2E (`e2e-tests-studio` skill) only when MSW cannot model the
journey. Run e2e-frontend-validation before merging frontend changes when
applicable.

Include mobile, tablet, and desktop screenshots when handing off UI changes.
Preserve design-system consistency and existing component APIs where possible.
No new `asChild`; prefer Base UI's native `render` prop.


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
