# AURUM-V Action Demo

This repository proves that the public Marketplace Action can be installed and executed from a clean external repository.

## What the workflow proves

The demo workflow:

1. checks out this repository;
2. creates an ephemeral Ed25519 demo key inside the GitHub runner;
3. generates a signed approval bundle bound to this exact repository and commit;
4. installs `bradshawdanni-collab/aurum-v-action@v1.0.0`;
5. verifies the valid bundle and requires `result=VERIFIED`;
6. modifies the signed artifact after authorization;
7. runs the Action again and requires the tampered bundle to fail.

No private production key is stored in this repository. The demonstration key exists only for the lifetime of one workflow run.

## Run the proof

Open **Actions → AURUM-V external installation proof → Run workflow**.

Expected result:

```text
Valid signed approval -> VERIFIED
Modified signed artifact -> TAMPERED / non-zero exit
Workflow -> success
```

## Installed Action

```yaml
uses: bradshawdanni-collab/aurum-v-action@v1.0.0
```

For production use, protect signing keys outside the repository and retain branch protection and required checks. AURUM-V verifies authorization evidence; it does not grant merge credentials or replace GitHub repository controls.
