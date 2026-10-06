# Validation scope — nine-skill edition

Prepared for publication on 2026-10-06. This is an instructions-only package, so no runtime test results are claimed for it.

Release checks cover:

- Exactly the nine upstream skill directory names, with no Dinesh Eval offline/manual variant entrypoints.
- YAML frontmatter and UI metadata parsing, skill name/directory correspondence, descriptions, and consistent plugin identity/version across the three manifests.
- Local Markdown links resolving within the package, with no dangling dependency on the separate CLI.
- Retained Apache-2.0 license, upstream authorship, immutable upstream revision and source hashes, and modification notices on adapted upstream Markdown.
- UTF-8 publication contents, archive integrity, and absence of private local paths, credentials, workplace assets, and generated runtime files in the selected publication file set.
- Preservation of the previously delivered Dinesh Eval 0.1.1 archive.

These are structural/source checks. They do not establish that a host has installed the plugin or can execute every workflow. No live model, generated review UI, human labeling session, cross-host behavioral evaluation, or plugin-directory review was performed for this release. The separate offline CLI's test results do not apply to this package, which excludes that CLI.

The package has no running service or bundled executable scripts. Workflow examples may require dependencies, model access, or project code when actually used; inspect and authorize those operations in the consuming environment.
