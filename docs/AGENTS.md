Use @styleguides/STYLEGUIDE.md first. Read neighboring pages, the relevant sidebar, and source or tests before editing. Prefer the canonical page over overlapping guidance.

Content families:

- src/content/en/docs (/docs): Product documentation
- src/content/en/integrations (/integrations): External integrations and deployment platforms
- src/content/en/reference (/reference): API and configuration reference
- src/content/en/models (/models): Generated; do not edit manually

Relevant guidance:

- @styleguides/INFORMATION_ARCHITECTURE.md: Content ownership and routes
- @styleguides/DOC.md: All /docs page types
- @styleguides/GUIDE_INTEGRATION.md: All /integrations pages
- @styleguides/REFERENCE.md: Reference pages
- @styleguides/COMPONENTS.md
- @styleguides/DIAGRAM.md: Mermaid diagram style and accessibility
- @styleguides/AUTHORING_WORKFLOW.md
- @CONTRIBUTING.md: Setup, frontmatter, and MDX syntax
- .claude/skills/docs-diagrams: Existing image-to-Mermaid conversions

Use model tokens from src/plugins/remark-model-tokens/models.ts for model names and IDs.

Follow @styleguides/AUTHORING_WORKFLOW.md for operational commands and checks.


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
