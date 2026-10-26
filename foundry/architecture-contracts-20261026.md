# BTG Universal Technology Foundry — Canonical Architecture and Interface Contract

**Architecture edition 2026-10-26 · Blackmore Technology Group Limited**

**Purpose:** One platform able to ingest authorized technology, identify and repair defects, assemble reusable components, verify their behavior, run on appropriate consented hardware, preserve ownership, and account for genuine licensed use.

**This is the architecture of the completed system, not an assertion that every proposed operation is deployed.** For dated acceptance status consult [the engineering evidence register](engineering-evidence-20261026.md).

## A. Architecture principles

1. **One public platform:** BTG Universal Technology Foundry. Its distinct user products are Studio, Command Centre, Bridge, FarmNode Host, Bit Trade Global and domain applications. Independent applications do not need independent identity, Council, data authority or scheduler implementations.
2. **Original authorities stay authoritative:** ENTITY for identity, owner-granted rights, signing, permission and revocation; original ADAM/BTDU for canonical underlying payload, trusted state and reconstructible execution; FarmNode Fabric for execution receipts and measured device use; Bit Trade Global for asset/issuer and commercial or market records.
3. **Multiple stores are legitimate when authority is bounded.** A single architecture does not mean copying secrets, canonical state, private owner data and financial settlement into one database.
4. **AI model proposals are not trusted executable artefacts.** Council-authored code or mathematical formulas require frozen source, independent tests, challenge, explicit admission and approval.
5. **No value is invented by internal bookkeeping.** Contributed compute is only measured, owner-authorized completed work. Licensed use requires a separate actual right and execution. Payments and investment rights remain distinct.
6. **Preserve originals.** All migrations must have provenance hashes, selected canonical destination, parity/restore tests, a rollback mechanism and explicit owner approval before old folders can be retired.
7. **Portable through typed interfaces.** Research engines AION, ARCI and ForgeNet may provide useful compatible components, but do not replace the original authority simply by being moved into the Foundry tree.

## B. Service responsibilities

| Service / interface | Responsibilities | Must NOT own |
|---|---|---|
| BTG Studio | Import authorized projects; graph decomposition; visual DataChip/Circuit composition; build/export | New independent ENTITY identities or Exchange balances |
| Command Centre | Operator approvals, run logs, release gates and fleet supervision | Alternate canonical user data |
| NIKI Council | Propose, criticize, revise and explain candidates; independently evaluate them | Automatic production authority or rights ownership |
| DataChip / Circuit / Genome | Typed I/O, composition, versioning, runtime policy and qualified executable references | Undocumented mutable global state |
| ADAM / BTDU | One authoritative payload and reconstructive views; versioned execution, recovery, audit and replay | Authority to override owner rights |
| FarmNode Fabric and Host | Logical job placement, physical host enrolment, isolation, resource budgets, actual job receipts | Fictional GPU or RAM capacity |
| ENTITY | Shared actor identity, signature, scoped grants, source/asset provenance, expiry and revocation | Execution scheduling or financial clearing |
| BTG Bridge | Source and device consent, permissions, encrypted connectivity and revocable resource offers | Automatic assignment of underlying dataset ownership |
| Bit Trade Global | Asset, issuer, instrument, licensed-use and economic event records under applicable rights | The original source repository or core runtime authority |
| HuntAR / SearchAR / HikeAR | Spatial application logic using shared engines and BSIE capabilities | New incompatible copies of the platform foundation |

## C. Required data contracts

### SourcePackage
`source_digest, source_manifest, original_location, actor, grant_ref, content_type, dependency_graph, target_platforms, safety_profile, frozen_acceptance_tests`

### RepairProposal
`source_digest, defect_id, problem_statement, candidate_diff_digest, creator_model_id, reviewer_ids, independent_oracle_ids, test_report_digest, failure_cases`

### QualifiedDataChip
`chip_id, version, implementation_digest, typed_input_schema, typed_output_schema, permission_scopes, resource_budget, test_evidence, provenance`

### Circuit/Genome
`genome_id, dependency_DAG, chip_refs, build_environment, signed_release_policy, replay_oracle, deployment_targets, rollback_ref`

### ENTITYGrant
`owner_subject, actor_subject, asset_id, allowed_action, device_or_app_scope, purpose, expiry, revocation_epoch, signature`

### FarmJobReceipt
`run_id, qualified_genome_digest, physical_host_id, logical_farmnode_id, resource_budget, actual_resource_measurements, completed_work_digest, authenticated_receipt, timestamps`

### BridgeConsent
`owner, source_or_device_ref, purpose, scopes, retention, resource_cap, expiry, revocation_token`

### ExchangeTechnologyUse
`asset_id, rights_instrument_id, license_ref, issuer_ref, qualified_use_entitlement, real_execution_receipt_ref, fee_rule, transaction_provenance`

Financial instruments and actual payment records are represented in distinct ledgers and schemas rather than conflated with DataChip instances or idle RAM.

## D. One stage-gated execution lifecycle

1. **Ingest:** authorized ZIP/repository or system export, verify source hashes and ownership, preserve immutable original.
2. **Describe:** parse languages, configurations, assets, devices and typed dependency graph, record reproducible defects, acceptance criteria and safety constraints.
3. **Create:** use NIKI creators for bounded candidate algorithms or repairs; annotate versioned DataChip type contracts.
4. **Challenge:** independent model critics and executable test oracles reject invalid, nondeterministic, unsafe or out-of-scope outputs. Keep failures in evidence.
5. **Admit:** reconstruct a versioned Genome through original ADAM/BTDU, maintaining data lineage, typed interfaces and signed owner authorization.
6. **Place:** FarmNodes choose appropriate local hardware or remote consented hosts with real OS-enforced CPU/RAM/GPU limits and estimated networking costs.
7. **Run:** execute only admitted work under scoped ENTITY grants and Bridge consent, preserving actual physical-work receipts and recovery logs.
8. **Use rights:** record real licensed technology-use events and instrument-specific economic information in Bit Trade Global; never infer security ownership from compute or dataset access alone.
9. **Reuse:** retain authenticated qualified components and negative tests for future compatible projects; always preserve source rights and undo paths.

## E. Formal fail-closed rules

- Invalid, expired or revoked ENTITY grant → no dispatch or data disclosure.
- Mismatched typed graph → no Genome assembly.
- Absent independent oracle or missing required Council reviewers → no qualified promotion.
- Missing physical host measurement → no compute contribution credited.
- Data source consent withdrawn → no further processing.
- Missing asset licence/entitlement → no billable technology-use record.
- Native device acceptance missing → no native application production claim.
- Host disconnect, timeout or receipt replay → the job remains incomplete or is proven idempotent; no invented completion.

## F. The proof BTG must provide

Qualify real HuntAR source repair with complete native device testing. Repeat with unrelated software. Verify 25 distinct independent Council members, physical distributed execution on three different hosts, unified ENTITY sign-on, original ADAM/BTDU parity, end-to-end rights-to-use receipts and independent cost/reliability comparisons against established software engineering approaches.

**Primary public explanation:** https://www.blackmoretechgroup.com/platform-architecture.html

**Engineering evidence:** https://www.blackmoretechgroup.com/engineering-proof.html
