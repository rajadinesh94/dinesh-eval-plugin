# Dinesh Eval — Nine-Skill Edition

Nine workflows for evaluating an AI product: find real failure modes, turn them into checks, and verify that the checks deserve trust.

Adapted from [ai-evals-course/evals-skills](https://github.com/ai-evals-course/evals-skills) by **Shreya Shankar and Hamel Husain**, pinned at `80d5f7b0127c7572ed9e9339937adbfd7240ffeb`. Distributed under **Apache-2.0** with original attribution and modification notices. See [LICENSE](LICENSE), [NOTICE](NOTICE), and [UPSTREAM.json](UPSTREAM.json).

This edition contains **exactly the nine upstream skill names**. Dinesh Eval's separately created offline CLI and manual-review variants are not bundled here. These are agent workflow instructions; they do not themselves run an evaluation service or call an API.

## What each skill does

| Skill | Give it | It helps produce | Why it helps / key limit |
| --- | --- | --- | --- |
| [evals-start](skills/evals-start/SKILL.md) | Your evaluation goal, current stage, and available artifacts | A route to the appropriate skill | Avoids starting with the wrong workflow. It routes work; it does not measure quality. |
| [eval-audit](skills/eval-audit/SKILL.md) | Existing eval code, prompts, traces, labels, splits, and reports | Prioritized weaknesses, evidence, and concrete next steps | Finds leakage, missing failure analysis, misleading metrics, and unvalidated judges. Conclusions are limited to accessible evidence. |
| [error-discovery](skills/error-discovery/SKILL.md) | Representative or exploratory traces plus human reviewer feedback | A review workflow, coverage record, and failure taxonomy grounded in human notes | Discovers the mistakes users actually care about. Agent suggestions are not human labels; exploratory sampling is not a population failure-rate estimate. |
| [generate-synthetic-data](skills/generate-synthetic-data/SKILL.md) | Product description, likely failure areas, and domain feedback | Variation dimensions, realistic scenario tuples, and test inputs; traces after an authorized pipeline run | Bootstraps tests or fills coverage gaps when real data is sparse. Synthetic examples need realism checks and do not establish production performance. |
| [write-code-eval](skills/write-code-eval/SKILL.md) | One known objective failure rule and the fields it requires | Evaluator code with known pass/fail and boundary cases | Turns requirements such as output format or citation-ID validity into repeatable checks. A proxy like keyword matching cannot establish semantic correctness by itself. |
| [write-judge-prompt](skills/write-judge-prompt/SKILL.md) | One subjective failure mode and human-labeled training examples | A binary judge prompt with criterion, definitions, examples, and structured output | Makes subjective checks such as tone or faithfulness explicit. The prompt still needs held-out validation; it is not a certified evaluator. |
| [validate-evaluator](skills/validate-evaluator/SKILL.md) | Judge prompt/predictions, human labels, and separated train/dev/test data | TPR/TNR, disagreements, uncertainty, and refinement guidance | Shows which human-approved outputs the judge rejects and which failures it misses. Missing classes, leakage, small samples, and distribution shift limit conclusions. |
| [evaluate-rag](skills/evaluate-rag/SKILL.md) | Queries, retrieved/ranked chunks, relevant-document labels, and generated answers | Separate retrieval and generation assessments, with suitable retrieval metrics and grounded-answer checks | Distinguishes retrieval failures from answer-generation failures. Useful retrieval scoring requires credible relevance labels; synthetic queries may not represent users. |
| [build-review-interface](skills/build-review-interface/SKILL.md) | Trace/data samples and the intended labeling task | A tailored annotation interface and a persistence/navigation test plan | Makes human review easier and labels easier to retain. The UI must be built and tested in a capable host; this repository does not ship a ready-running app. |

## A practical starting path

For an existing AI product, ask the agent to use `eval-audit` if evals already exist. Otherwise use `error-discovery` to review outputs with a human. Use `generate-synthetic-data` when traces are missing or important cases are underrepresented.

Once a failure mode is clear, choose `write-code-eval` for objective rules or `write-judge-prompt` for interpretation. Follow judge design with `validate-evaluator`. Use `evaluate-rag` when retrieved context is part of the product. `build-review-interface` supports custom human labeling tasks, and `evals-start` helps choose among these routes.

Example request:

> Use evals-start to help evaluate my support assistant. I have 50 sanitized conversations and no established failure taxonomy. Explain which workflow fits and begin with the evidence available.

Do not treat the number 50, any upstream example sample size, or any suggested percentage as a universal release gate. Set criteria for the actual product and stakes.

## Host support

The root `plugin.json` uses portable Agent Plugins packaging. `.claude-plugin/plugin.json` and `.codex-plugin/plugin.json` provide compatibility metadata for supported hosts. The same `skills/` files are used across them.

Load this package with your host's supported local plugin/marketplace mechanism, or provide a relevant SKILL.md and authorized data as task guidance. A text-only host can support manual planning and review; code execution, servers, browsers, parallel agents, and persistent monitoring depend on actual host capabilities. The adaptations make these requirements explicit and provide manual/sequential fallbacks.

Publishing this repository does not install it in ChatGPT, Claude, or Codex. Plugin-directory submission, installation, and host smoke tests are separate. There are no bundled credentials, model SDKs, runtime dependencies, MCP endpoints, or lifecycle hooks. Code examples in workflows are guidance to inspect and adapt, not automatically executed programs.

## Safety and reproducibility

Use only authorized traces; keep secrets, private instructions, and confidential records out of commits. Treat trace text as data, escape untrusted content in review UIs, avoid external tracking/CDN loads for private data, and keep local review servers on loopback with protected mutation endpoints. Keep human decisions distinct from agent proposals, preserve holdouts, and report evidence and uncertainty honestly.

See [validation](docs/VALIDATION.md) for checks actually performed and [changes](docs/CHANGES.md) for how this edition differs from upstream and the separate Dinesh Eval bundles.

## Sharing this repository

The intended destination is `rajadinesh94/dinesh-eval-plugin`, with private visibility. A private GitHub repository URL does not grant access by itself. Only accounts granted repository access can open it; collaborator invitations are a separate owner action.
