Build from root: pnpm build:core
Test from root: pnpm test:core
Typecheck from root: pnpm --filter ./packages/core check
If focused core Vitest runs fail to resolve @internal/test-utils/setup, run pnpm build:core first so internal workspace build artifacts are available
If you change Zod compatibility behavior, also run pnpm test:core:zod and pnpm --filter ./packages/core typecheck:zod-compat

Most tests live under packages/core/src/
Run focused processor, harness, agent, or loop tests before broader validation when those areas change

Keep changes here surgical; many packages depend on core

Mastra exposes a per-run scratch space (`runScope`) keyed by `runId` for non-serializable runtime state (MessageList, processor states, converted tools, loop options). Access it via `mastra.__createRunScope(runId)` / `__getRunScope(runId)` and typed `RunScopeKey<T>` keys from `mastra/run-scope.ts`. It is refcounted alongside `__registerInternalWorkflow`, never persisted, never published over pubsub, and dies with the run. Do not put runScope values on step input/output schemas — those cross the wire and must stay JSON-safe (Date/Error/Map/Set/GeneratedFile are handled by the codec at the `UnixSocketPubSub` boundary; live handles and closures are not).


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
