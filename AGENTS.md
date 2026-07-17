# Dialogue Knowledge Guide

This directory is the Dialogue Knowledge root specified by `.dialogue.yml`.

## Document layout

- `docs/`: current state, specification support, validation results
- `governance/`: the Authority Registry and operational authority
- `proposals/`: undecided or to-be-approved semantic changes
- `changes/`: the semantic history of applied changes

## Read protocol

1. Confirm the Active State and the Authority Registry for the target scope.
2. Do not treat a Proposal as the current state.
3. Read a related Change Record only when the change history is needed.
4. Do not use Archived knowledge except in an explicit history investigation.
5. If a unique source of truth cannot be resolved, do not update and escalate.

## Write protocol

1. Before writing, synchronize the remote `main` and re-confirm the target revision.
2. For a settled semantic change, update the State and an independent Change Record.
3. For C3 or C4, record the target and revision of the Human Approval.
4. Do not later overwrite an Applied Change Record. Record a correction as a new change.
5. Validate with `cd development && uv run python scripts/validate_repository.py` before pushing.
