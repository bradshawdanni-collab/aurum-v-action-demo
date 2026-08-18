# ΩB-PRE-MUTATION-DEPLOYMENT-RECEIPT-001

**Status:** CAPTURED / STOP — PROVIDER MUTATION NOT AUTHORIZED  
**Contract:** `ΩB-DEPLOYMENT-VERIFICATION-001 — Mandatory AURUM Before Merge`  
**Repository:** `bradshawdanni-collab/aurum-v-action-demo`  
**Target branch:** `main`  
**Captured at:** `2026-08-18T19:15:36+10:00` (`Australia/Melbourne`)  
**Capture mode:** READ-ONLY provider inspection; documentation write only  
**Provider mutation:** NONE  
**Workflow mutation:** NONE  
**Merge credential introduced:** NONE  
**AURUM-V v1.1 mutation:** NONE

## 1. Repository / target identity

```text
repository            bradshawdanni-collab/aurum-v-action-demo
target_branch         main
main_sha              b48bf5fb859ef498ed0bd2185ba2d7b8fb2bbc55
repository_visibility public
repository_owner      bradshawdanni-collab
```

## 2. Current AURUM workflow identity

The target repository currently contains one workflow under `.github/workflows/`:

```text
path                   .github/workflows/aurum-v-demo.yml
workflow_blob_sha      f7055696e30afd15be9e65c01faf83102cd7721f
workflow_name          AURUM-V external installation proof
job_key                prove-external-installation
trigger                workflow_dispatch + push(main)
workflow_permissions   contents: read
```

The workflow invokes:

```text
bradshawdanni-collab/aurum-v-action@v1.0.0
```

The `v1.0.0` ref resolves to:

```text
98be599b683a3a3d1e206b45b53fe6b4b1dedf36
```

### Required-check identity classification

```text
workflow_name_exact                 ESTABLISHED
job_key_exact                       ESTABLISHED
provider_generated_check_identity   UNKNOWN
configured_required_check_identity  NONE ESTABLISHED
```

The current repository evidence establishes the workflow name and job key but does not directly expose a provider-generated Check Run / required-status-check identity for this deployment. A commit-status lookup through the available connector returned no status records for the current `main` commit. The contract prohibits guessing that the job key is necessarily the exact provider-required-check string.

**STOP CONDITION ENGAGED:** `required-check identity is ambiguous`.

## 3. Provider enforcement state

Current classic branch metadata for `main` reports:

```text
protected                      false
classic_protection_enabled     false
required_status_checks         off
required_status_check_contexts []
```

Repository merge-method configuration currently permits:

```text
merge_commit   true
squash_merge   true
rebase_merge   true
auto_merge     false
```

### Ruleset state

```text
applicable_repository_rulesets      UNKNOWN
applicable_parent_rulesets          UNKNOWN
ruleset_enforcement_mode            UNKNOWN
ruleset_required_checks             UNKNOWN
ruleset_bypass_actors               UNKNOWN
```

The connected GitHub interface available for this capture does not expose the repository-ruleset listing needed to establish repository and inherited rulesets. No inference from `protected=false` is used to claim that rulesets are absent.

**STOP CONDITION ENGAGED:** `applicable ruleset state cannot be established`.

## 4. Merge-capable actors

Directly established actor evidence:

```text
actor                  bradshawdanni-collab
repository_role        owner
repository_permission  admin
merge_capable          YES, by repository permission
```

The current workflow itself is scoped to `contents: read`, so this workflow does not establish a GitHub Actions merge-capable token path.

### Complete actor enumeration

```text
all collaborators with write/maintain/admin    UNKNOWN
all GitHub Apps with merge-capable permission  UNKNOWN
all automation/service identities              UNKNOWN
all external credentials / PAT holders         UNKNOWN
```

The available connector can verify permission for a named collaborator but does not expose a complete collaborator / installation enumeration in this capture.

**STOP CONDITION ENGAGED:** complete merge-capable actor enumeration is not established.

## 5. Bypass actors

Classic branch protection is disabled, so no classic protected-branch bypass list is established for `main`.

However, because applicable rulesets are UNKNOWN, the following remain UNKNOWN:

```text
ruleset bypass actors
admin bypass mode
GitHub App bypass grants
team bypass grants
pull-request-only bypass paths
```

The known repository owner/admin is merge-capable, but this receipt does not label that actor a `ruleset bypass actor` without an applicable ruleset to test against.

**STOP CONDITION ENGAGED:** `bypass actors cannot be enumerated`.

## 6. Pre-mutation enforcement conclusion

```text
classic provider enforcement              OFF
mandatory AURUM required check             NOT ESTABLISHED
provider-generated required-check identity UNKNOWN
applicable rulesets                        UNKNOWN
known merge-capable owner/admin            ESTABLISHED
complete merge-capable actor set           UNKNOWN
complete bypass actor set                  UNKNOWN
```

Therefore the pre-mutation deployment state does not currently establish:

\[
MergeEligible \Rightarrow AURUMCheck = SUCCESS
\]

and does not establish:

\[
\neg ValidAURUMAuthorization \Rightarrow \neg GitHubMerge
\]

for the provider boundary.

This is an evidence result, not a failure observation.

## 7. Contract disposition

```text
PRE-MUTATION RECEIPT        CAPTURED
PROVIDER CONFIG MUTATION    STOP
WORKFLOW MUTATION           STOP
TEST EXECUTION              STOP
v1.1                        FROZEN
C_v1.1                      UNCHANGED
FirstDivergence             NONE
```

No provider-enforcement configuration is authorized by this receipt.

Before provider mutation can be considered, the following evidence gaps must be resolved without changing the provider configuration:

1. observe the exact provider-generated check identity intended to become mandatory;
2. establish applicable repository/inherited ruleset state;
3. establish the merge-capable actor set to the extent required by the deployment contract;
4. establish applicable bypass actors / bypass modes.

If any of these cannot be established, retain `STOP / NOT ESTABLISHED` rather than repair or infer.