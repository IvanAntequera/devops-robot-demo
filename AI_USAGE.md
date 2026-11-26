# AI Usage Declaration

## Tools and Models

- **Tool:** Google Gemini
- **Model / Mode:** Neon (High Thinking mode)

## Purpose

Generative AI was used as a technical assistant during Phases 3, 4, and 5 for the following tasks:

- **Repository configuration (Phase 3):** Understanding how to configure GitHub branch protection rules (`Rulesets`) on `main` to require the `test` status check.
- **Workflow debugging (Phase 4):** Diagnosing why the `Continuous Delivery` workflow did not trigger after pushing the `v1.0.0` tag and determining the correct Git workflow to fix and re-tag the release.
- **Documentation and review (Phases 4 and 5):** Structuring answers to the reflection questions, checking completeness against the assignment rubric, and translating and formatting `README.md` into English.

Core implementation (`robot.py`, `test_robot.py`, `requirements.txt`, initial CI setup), Git operations, Pull Requests, and execution of all workflows were carried out directly in the repository.

## Relevant Prompts and Responses Used

1. **Configuring branch protection and questioning PR restrictions on `main`:**
   - *Prompt summary:* Asked how to implement the Phase 3 recommended extension, and challenged whether enabling "Require a pull request before merging" was necessary if the assignment only required the `test` check—specifically asking whether a direct `git push` to `main` would trigger the tests instead.
   - *Outcome used:* Confirmed that GitHub evaluates branch protection rules synchronously on push, while Actions runs asynchronously after a push is accepted. Because `.github/workflows/ci.yml` only triggers on `push` to `main` and `pull_request` to `main`, requiring the `test` check effectively blocks direct pushes to `main` and requires modifying `main` through feature branches and Pull Requests.

2. **Debugging the Continuous Delivery trigger in Phase 4:**
   - *Prompt summary:* Reported that running `git tag v1.0.0` and `git push origin v1.0.0` did not trigger `Continuous Delivery` or re-run tests, and later asked how to update `.github/workflows/release.yml` and re-tag after discovering malformed quotes around `'v*'`.
   - *Outcome used:* Identified the YAML syntax issue with the tag pattern, fixed `.github/workflows/release.yml` via a dedicated branch and Pull Request, and followed the proper tagging procedure to trigger the delivery pipeline.

3. **Reflection review and `README.md` translation:**
   - *Prompt summary:* Requested concise technical answers to the Phase 4 and Phase 5 reflection questions, followed by an English translation and formatting audit of `README.md` against the assignment rubric.
   - *Outcome used:* Reorganized headings, properly fenced terminal/test logs, added the missing project overview and explicit Phase 3 failure analysis, and translated the documentation into English.

## Contributions

- **AI-assisted:** Branch protection explanation and setup steps, diagnosis of the `release.yml` tag trigger failure, draft structure of the Phase 4/5 reflection answers, English translation and Markdown formatting of `README.md`, and initial draft of this `AI_USAGE.md` file.
- **Author-only:** Creation and management of the GitHub repository, implementation of `robot.py` and `test_robot.py`, execution of Git branches, Issues, Pull Requests, and tags, capture of workflow screenshots, and local inspection of the generated artifact.

## Human Validation

All AI suggestions were independently verified against GitHub's actual behavior and the official assignment requirements:

- **Branch protection behavior:** Verified directly in GitHub Settings and on the Phase 3 Pull Request that `main` rejected merging while `test` was failing and allowed merging only after restoring `distance > 0.5`. Also verified in `.github/workflows/ci.yml` that the configured triggers matched the explanation regarding direct pushes vs. Pull Requests.
- **Release workflow and artifact:** Inspected `.github/workflows/release.yml` manually to confirm the quote formatting error, verified the resulting green `Continuous Delivery` run in GitHub Actions, downloaded the `robot-demo` artifact, and extracted `robot-demo.tar.gz` locally (`tar xvf`) to confirm it contained `robot.py` and `README.md`.
- **Documentation accuracy:** Cross-checked the translated `README.md` against every phase and deliverable in the assignment PDF, replaced placeholder links/tags with actual repository evidence, and reviewed the technical reflections to ensure they accurately describe what occurred in the project.
