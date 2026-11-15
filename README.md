# Bug-Bounty-CVE-Hunt

**Expert-level AI agent skills for advanced bug bounty and white-box CVE research.**

The specialist methodologies are the core of this project: deep source auditing, analysis of interacting security controls, and evidence-based vulnerability chaining. The advanced workflows investigate parser and representation mismatches, deferred consumers, identity and state transitions, and trust boundaries across components.

The toolkit combines these skills with Semgrep research rules, CodeQL analysis guidance, controlled local labs, and a corpus of thousands of public HackerOne and Bugcrowd disclosure records. It supports the path from a falsifiable security hypothesis to a supported finding, a focused fix, and a meaningful regression check.

## Expert-level research methodology

The specialist workflows emphasize two demanding forms of security investigation:

| Research focus | What the methodology requires |
| --- | --- |
| **Deep vulnerability research** | Resolve a nontrivial interaction between representations, controls, components, trust contexts, or state transitions. Establish the exact mechanism, effective defenses, security invariant, and a discriminating control. |
| **Vulnerability chain analysis** | Compose independently established primitives across an additional security boundary. Document the dependency graph, compatible actors/state/versions, validated and conditional links, and a control that would break the chain. |

### What the advanced workflows emphasize

- **Deep source and control tracing:** follow attacker-controlled inputs through transformations, effective guards, and the actual sink or security decision, with reproducible source locations and version context.
- **Control interaction analysis:** investigate validation/use disagreements, parser differentials, second-order processing, deferred execution, and identity/state binding under the actual implementation.
- **Hypothesis-driven validation:** state falsifiable predictions, plausible alternative explanations, meaningful negative controls, and the precise evidence needed to confirm or refute the mechanism.
- **Evidence-based chains:** establish each independent primitive and the additional crossed boundary; record compatible prerequisites and unresolved links.
- **Finding-to-fix discipline:** keep finding validation, patch review, and executed regression results separate, preserving legitimate behavior and documenting remaining gaps.

The [SSRF evidence contract](SKILLS/ssrf/references/evidence-reporting.md) and [GraphQL evidence contract](SKILLS/graphql_api/references/evidence-and-reporting.md) provide implemented examples of these requirements. Scope and eligibility remain defined by each specialist. Each conclusion is tied to its evidence, preconditions, and demonstrated impact.

This is a personal security research workspace intended for private use. Skills are Markdown documents with YAML metadata, accompanied by selected executable helpers. Choose and load the relevant documents through the agent or workflow you actually use, verifying any tool integration against the local configuration.

## What is included

| Component | Purpose | Start here |
| --- | --- | --- |
| Specialist skills | Black-box/gray-box assessment and white-box source review, with conditional add-ons and shared references. | [Skill index and roadmap](skills.txt), [SKILLS/](SKILLS/) |
| Semgrep research rules | Locate source patterns and produce candidates for manual validation. Includes synthetic examples and helper scripts. | [Semgrep guide](labs/semgrep/README.md) |
| CodeQL guidance | Guidance within the source-review methodology for deeper data-flow investigation. | [XSS source-review skill](SKILLS/xss/xss_source_hunter_skill.md) |
| WordPress lab | Docker Compose setup, dedicated role/data fixtures, and a runtime-verification workflow. | [WordPress lab guide](labs/wordpress/README.md) |
| Public-disclosure corpus | Structured research records, original-source links, classification, confidence, and review history. | [Research corpus](research/reports/) |

Semgrep rules and helpers are included. CodeQL is currently referenced as an analysis tool in the skills; this snapshot does not include a dedicated CodeQL query pack or configured CodeQL automation.

## Security research coverage

Choose the specialist closest to the security boundary under investigation. Read its add-on triggers rather than loading the entire catalog at once.

| Area | Main focus | Directory |
| --- | --- | --- |
| Reconnaissance | Scoped attack-surface inventory, evidence correlation, and specialist handoffs. | [recon](SKILLS/recon/) |
| Authentication and sessions | Identity binding, OAuth/OIDC transitions, and session lifecycle. | [authn_session](SKILLS/authn_session/) |
| Authorization | BOLA/IDOR, object/property/function access, and tenant isolation. | [authz_bola](SKILLS/authz_bola/) |
| JWT | Token cryptography, validation, and profile-specific trust decisions. | [jwt](SKILLS/jwt/) |
| XSS and client-side security | Rendering contexts, source-to-sink flows, browser behavior, and client-side gadget chains. | [xss](SKILLS/xss/) |
| SQL and query injection | SQL/ORM/query construction, parsing, controls, and evidence-backed triage. | [sqli](SKILLS/sqli/) |
| SSRF | Destination-policy transitions, deferred consumers, and internal trust boundaries. | [ssrf](SKILLS/ssrf/) |
| CSRF and CORS | Browser request feasibility, state-changing actions, and response-read policies. | [csrf-cors](SKILLS/csrf-cors/) |
| GraphQL | Demand controls, document/operation identity, transport, and resource lifecycle. | [graphql_api](SKILLS/graphql_api/) |
| HTTP desynchronization | Framing, intermediary/backend interpretation, and connection lifecycle. | [http_desync](SKILLS/http_desync/) |
| File handling | Path resolution, upload/inclusion boundaries, and later file consumers. | [file_attack](SKILLS/file_attack/) |
| Information disclosure | Sensitive-data exposure, representation boundaries, provenance, and secrets. | [info_disclosure](SKILLS/info_disclosure/) |
| Business logic and races | State invariants, reservations, idempotency, interleavings, and settlement. | [logic_race](SKILLS/logic_race/) |
| Command/code/template injection | Interpreter boundaries, argument handling, deferred processing, and conditional chains. | [rce_injection](SKILLS/rce_injection/) |
| WordPress | Core/plugin/theme auditing, capabilities, hooks, metadata, and controlled runtime verification. | [wordpress](SKILLS/wordpress/) |

The skill index is a navigation aid. Check the actual files and their declared scope before relying on a module or roadmap item. Use the relevant evidence requirements when assessing severity, certainty, and CVE eligibility.

## A practical workflow

1. **Define the task.** Identify the authorized repository or assessment scope, actors, roles, tenant boundaries, versions, and intended security policy.
2. **Choose a skill.** Start with the relevant primary document and load supporting references only when their triggers apply.
3. **Develop a falsifiable hypothesis.** State the suspected boundary failure, an alternative explanation, and the control that would distinguish them.
4. **Gather evidence.** Trace source and effective guards, inspect supplied traffic, or use selected static rules to locate candidates.
5. **Validate the smallest relevant effect.** Use owned synthetic data and an appropriately isolated local environment when runtime checks are needed and authorized.
6. **Record the outcome.** Preserve confirmed findings, rejected hypotheses, unresolved gaps, and coverage limits. Develop a narrow patch and regression when those tasks are authorized.

A scanner match, error, dependency name, unusual response, or incomplete trace is a candidate. A finding needs evidence of a real security boundary failure. Keep observed behavior separate from inferred mechanics and conditional impact. Track finding validation, patch review, and executed regression results independently.

## Using the skills

Start with [skills.txt](skills.txt), then open the relevant primary document under `SKILLS/`. For example:

- A WordPress plugin review starts with [the WordPress specialist](SKILLS/wordpress/wordpress_cms_security_research_skill.md).
- A source-level SSRF investigation starts with [SSRF Source Hunter](SKILLS/ssrf/ssrf_source_hunter_skill.md).
- A browser-facing XSS source review starts with [XSS Source Hunter](SKILLS/xss/xss_source_hunter_skill.md).
- An attack-surface inventory starts with [the reconnaissance skill](SKILLS/recon/recon_attack_surface_skill.md).

Give the agent the actual task, authorized scope, relevant artifacts, and the selected skill document. Skill selection and file loading depend on the environment in use. Several documents describe optional external tools or harnesses; verify any integration against the local configuration before using it.

## Semgrep rules and local checks

The current research rules cover six module groups:

| Module | Configuration |
| --- | --- |
| Localhost/daemon CORS and related browser-access review | [localhost-daemon-pna-cors](labs/semgrep/localhost-daemon-pna-cors/localhost-daemon-pna-cors-hunter.yaml) |
| SameSite/Lax, HTTP verbs, and GraphQL | [samesite-lax-verb-graphql](labs/semgrep/samesite-lax-verb-graphql/samesite-lax-verb-graphql-hunter.yaml) |
| OAuth transaction/account-linking review | [oauth-state-desync-account-linking](labs/semgrep/oauth-state-desync-account-linking/oauth-state-desync-account-linking-hunter.yaml) |
| SameSite=None and CSRF correlation | [samesite-none-csrf-correlation](labs/semgrep/samesite-none-csrf-correlation/samesite-none-csrf-correlation-hunter.yaml) |
| Credentialed CORS origin trust | [cors-credentialed-origin-trust](labs/semgrep/cors-credentialed-origin-trust/cors-credentialed-origin-trust-hunter.yaml) |
| WordPress nonce/capability review | [wp-csrf-nonce-hunter](labs/wordpress/semgrep/wp-csrf-nonce-hunter.yaml) |

Install the Semgrep CLI separately in the execution environment you use. Python 3 is needed for the Python helpers. The [Semgrep guide](labs/semgrep/README.md) documents the reference version, rule-test conventions, and evidence contract.

From the repository root, an example using one explicit local configuration is:

```bash
semgrep scan \
  --config labs/semgrep/oauth-state-desync-account-linking/oauth-state-desync-account-linking-hunter.yaml \
  --metrics=off \
  --disable-version-check \
  /path/to/authorized/source
```

Replace the final path with the source you are permitted to assess. Use local YAML files explicitly; `labs/` also contains Docker Compose configuration. Read execution errors and coverage information alongside any findings. An empty or failed scan is not evidence that the target is secure.

The [Python helper](labs/semgrep/run_sast_audit.py) discovers the research configurations and supports rule tests through `--test`. The [report helper](labs/semgrep/sast_gatekeeper_report.py) structures Semgrep output for additional review. Their generated reports still require source tracing and context-specific validation. Synthetic rule tests evaluate the patterns they exercise, not vulnerability prevalence or real-project accuracy.

## WordPress runtime lab

Read the [lab guide](labs/wordpress/README.md) before starting or adding target code. The setup expects Bash/WSL, Docker Compose v2 with the documented readiness options, and the utilities listed in that guide.

From the repository root:

```bash
bash labs/wordpress/setup-wp-lab.sh
```

The Compose configuration publishes the web service on loopback at `127.0.0.1:8080`. The setup supports role/data fixtures and explicit target-plugin selection. Follow the lab guide for image identity, existing persistent state, target activation, and controlled verification.

Internal CLI/function diagnostics and HTTP/browser verification establish different things. Claims depending on browser credentials, nonces, routing, or middleware require evidence from the corresponding lifecycle. Record versions, actor, initial fixture state, actual result, controls, and cleanup for each executed check.

## Public HackerOne and Bugcrowd research corpus

The corpus links public disclosures and selected public summaries to structured research records. It supports comparative reading, root-cause study, candidate prioritization, and the design of better skills, source queries, and local fixtures. The original disclosure remains the reference for what the researcher reported.

### Snapshot

The following figures come from [progress.json](research/reports/progress.json) and the CSV export inspected on **2026-11-15**:

| Measure | Records |
| --- | ---: |
| Total exported records | 6,484 |
| HackerOne | 5,751 |
| Bugcrowd | 733 |
| Pipeline status `complete` | 6,269 |
| Pipeline status `error` | 215 |

These are research-record and processing counts. `complete` means the pipeline processed the record; it does not establish full-text availability, independent vulnerability reproduction, correct classification, remediation, or CVE eligibility. Read confidence, evidence level, source status, and the original report before drawing a conclusion. Counts and exports are snapshots and may change.

### Files to use

| File | Use |
| --- | --- |
| [classified_reports.csv](research/reports/classified_reports.csv) | Filter by platform, category, confidence, evidence level, or processing status; compare causes, prerequisites, impact, lessons, and mitigations. |
| [progress.json](research/reports/progress.json) | Check the recorded processing snapshot and queue statistics. |
| [final_analysis.md](research/reports/final_analysis.md) | Read research interpretation and limitations; respect the dates attached to historical checkpoints. |
| [high_value_findings.md](research/reports/high_value_findings.md) | Explore selected case notes and a study/verification route. |
| [prioridades.md](research/reports/prioridades.md) | Understand research categories, collection scope, and classification rules. |
| [resume.md](research/reports/resume.md) | Consult operational history and handoff notes; historical process IDs or scheduler states do not describe the current machine automatically. |

Research pipeline scripts, schemas, caches, and review outputs are under [research/reports/](research/reports/). Reading the CSV and notes is enough to start using the existing corpus. Acquisition, classification, scheduling, or external-model calls are separate operations with their own prerequisites; opening this repository does not start them.

### Turn a report into useful research

1. Pick one class and select three to five relevant records. Check processing status, evidence level, confidence, and source links.
2. Read the original disclosures where available. Separate what the source demonstrates, what it merely claims, and what the local summary infers.
3. Extract the actor, controlled input, intended policy, failed control, concrete effect, preconditions, and proposed fix.
4. Write a falsifiable hypothesis for your own authorized source review. Identify a legitimate or protected case that would refute an overbroad rule.
5. Where needed, design a small isolated fixture using synthetic data to test the invariant. Record whether the test was proposed or actually executed.
6. Improve the relevant skill, add a narrowly justified query/rule, or create a regression exercise. Preserve the source locator and document what the new artifact does and does not establish.

For an IDOR/BOLA study, for example, compare reports about missing ownership checks, identify where the authorized principal should be bound to the requested object, and model two synthetic users in a local fixture. A useful rule or regression should distinguish the protected path from the broken path. A public disclosure is background evidence, not authorization to replay requests against the original target.

## Repository layout

```text
Bug-Bounty-CVE-Hunt/
|-- README.md
|-- LICENSE
|-- THIRD_PARTY_NOTICES.md
|-- skills.txt
|-- SKILLS/                 Primary skills, add-ons, references, selected assets/schemas
|-- labs/
|   |-- semgrep/            Research rules, synthetic examples, helpers, playbooks
|   `-- wordpress/          Compose lab, setup script, verification guide, WordPress rules
|-- research/
|   `-- reports/            Public-disclosure research and processing artifacts
`-- tmp/                    Authoring prompts, focused research, and temporary planning material
```

Use documented artifacts as entry points rather than relying on incidental database, cache, backup, lock, or runtime files. Keep credentials, model tokens, browser sessions, lab data volumes, and machine-specific runtime state outside distributable documentation and source bundles.

## Research and evidence boundaries

Use the toolkit only with an established authorization and scope. Prefer source inspection and controlled local evidence, minimize collected sensitive data, and preserve the distinction between a proposed test and an executed result. Let each specialist define its own proof and stop conditions. Scope, impact, patch status, and disclosure status are separate decisions.

Original public-report authors and programs retain credit for their disclosures. Source summaries and AI-assisted classifications can be incomplete or wrong. Neither a public report, a scanner result, nor this repository establishes a new CVE or guarantees a bounty.

## License and ownership

Project owner: **Web Security Labs - @websecuritylabs**.

The project owner's policy for otherwise unlicensed original project material is **proprietary, with all rights reserved**, as stated in [LICENSE](LICENSE). Existing per-file license declarations and third-party rights remain in force; the root notice does not replace them.

The inspected tree contains files declaring **MIT** and **Apache-2.0**. Their paths and the third-party corpus boundaries are recorded in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md). Public HackerOne/Bugcrowd disclosures, copied extracts, external tool components, and upstream material are not claimed as exclusively owned by this project.

Repository visibility is configured separately through GitHub settings. Making a repository private does not withdraw previously granted licenses or remove copies already obtained by others. Before sharing any source or corpus bundle, preserve applicable licenses, notices, attribution, and source-specific terms.
