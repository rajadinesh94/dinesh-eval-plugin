# Nine-skill edition changes

Edition version: 0.2.0. Prepared 2026-10-06.

Upstream: ai-evals-course/evals-skills, version 0.3.1, commit `80d5f7b0127c7572ed9e9339937adbfd7240ffeb`, Apache-2.0, credited to Shreya Shankar and Hamel Husain.

- Retains exactly the nine upstream skill directories and their original names, plus their OpenAI UI metadata and the error-discovery review-loop reference.
- Adds common guidance for authorized data, prompt-injection resistance, host-capability fallbacks, local UI safety, and honest reporting of work actually performed.
- Makes delegation and active-session polling conditional on capabilities and authorization. Removes a required Claude-specific monitor mechanism and suggests sequential/manual alternatives.
- Clarifies that sample counts and alignment thresholds are heuristics, and corrects statistical guidance about class-specific uncertainty, transportability, and ill-conditioned production-rate correction.
- Removes references to the Dinesh Eval CLI, which belongs to a separate optional distribution and is not part of these nine workflows.
- Supplies Dinesh Eval portable, Claude, and Codex manifests, with license, attribution, upstream source hashes, and prominent notices on modified Markdown.

The previously prepared Dinesh Eval 0.1.1 delivery bundle remains separate and unchanged. It contains additional original offline/review options; those must not be presented as part of the nine upstream skills.

This edition adds no installed dependencies, live model calls, private project instructions, workplace assets, credentials, or user data.
