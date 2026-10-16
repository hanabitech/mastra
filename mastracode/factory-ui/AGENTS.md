Dev (Docker services + API on :4111 + Vite on :5173): `pnpm --dir mastracode/web dev:ui`
Build: `pnpm --filter ./mastracode/factory-ui build`
Typecheck: `pnpm --filter ./mastracode/factory-ui typecheck`
Unit tests: `pnpm --filter ./mastracode/factory-ui test:unit`
MSW UI tests: `pnpm --filter ./mastracode/factory-ui test:msw`

This package owns the MastraCode React SPA, client data layer, Vite config, and UI tests. Its build is bundled into the Mastra CLI, not used by the web host at runtime. Dev orchestration starts in `mastracode/web`, which owns Docker and `.env`: its `dev:ui` script brings the containers up, then runs `turbo run dev dev:api --filter ./mastracode/factory-ui`. That builds this package's workspace dependencies, then starts Vite on :5173 and the host API on :4111. Both tasks live here because `mastracode/web` sits outside the workspace and Turbo can only run workspace packages, so `dev:api` is a shim for `pnpm --dir ../web api`. Run either alone to restart one side independently.

Build workspace dependencies without starting anything with `pnpm turbo build --filter ./mastracode/factory-ui`.

Primary tests use Vitest, MSW, real `@mastra/client-js`, and React Query. Mock only the network boundary—never our hooks, services, or auth gating. Unit tests run from `vitest.config.ts`; MSW UI tests use `e2e/ui/vitest.config.ts`, `e2e/ui/msw-server.ts`, and `e2e/ui/render.tsx`. Use `waitForMutationsIdle` for query chains.

Keep the `src`/`src/ui` layout: it avoids churn across 200+ reciprocal imports. `src/ui/tsconfig.json` includes type-resolution workarounds for Playground UI declarations.


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
