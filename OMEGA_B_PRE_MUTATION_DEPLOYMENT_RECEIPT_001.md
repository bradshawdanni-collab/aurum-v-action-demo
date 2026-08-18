# ΩB-PRE-MUTATION-DEPLOYMENT-RECEIPT-001

**Status:** CAPTURED / STOP — PROVIDER MUTATION NOT AUTHORIZED  
**Contract:** `ΩB-DEPLOYMENT-VERIFICATION-001 — Mandatory AURUM Before Merge`  
**Repository:** `bradshawdanni-collab/aurum-v-action-demo`  
**Target branch:** `main`  
**Captured at:** `2026-08-18T19:15:36+10:00` (`Australia/Melbourne`)  
**Updated evidence:** provider job record + supplied GitHub Actions runtime log  
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

### Provider-observed job / check identity

Exact provider evidence supplied for GitHub Actions run/job:

```text
run_id       31123847054
job_id       92690163065
job_name     prove-external-installation
status       completed
conclusion   success
```

The GitHub Actions runtime log for that same execution ends with:

```text
Complete job name: prove-external-installation
```

Therefore:

```text
workflow_name_exact                 ESTABLISHED
job_key_exact                       ESTABLISHED
provider_observed_job_name          ESTABLISHED: prove-external-installation
provider_generated_check_identity   ESTABLISHED: prove-external-installation
configured_required_check_identity  NONE ESTABLISHED
```

The earlier ambiguity over the provider-rendered job/check identity is resolved. This does not mean the check is currently configured as required; classic required-status-check enforcement remains off.

## 3. Workflow token authority

The GitHub Actions runtime log records:

```text
GITHUB_TOKEN Permissions
Contents: read
Metadata: read
```

The provider job record also confirms the job executed successfully using the expected AURUM Action ref.

Classification:

```text
current workflow GITHUB_TOKEN merge authority   NOT ESTABLISHED
contents write permission                        ABSENT IN OBSERVED RUN
pull-request write permission                    ABSENT IN OBSERVED RUN
workflow-local merge-capable token path          NOT ESTABLISHED
```

This closes the workflow-token branch only. It does not establish absence of external PATs, GitHub Apps, deploy keys, or other credentials outside the observed workflow.

## 4. Provider enforcement state

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
applicable_parent_rulesets          N/A for personal-account repository unless separately evidenced
ruleset_enforcement_mode            UNKNOWN
ruleset_required_checks             UNKNOWN
ruleset_bypass_actors               UNKNOWN
```

The connected GitHub interface available for this capture does not expose the repository-ruleset listing needed to establish repository-level rulesets. No inference from `protected=false` is used to claim that rulesets are absent.

**STOP CONDITION REMAINS:** applicable repository ruleset state cannot be established.

## 5. Merge-capable actors

Directly established actor evidence:

```text
actor                  bradshawdanni-collab
repository_role        owner
repository_permission  admin
merge_capable          YES, by repository permission
```

The observed workflow token is read-only for repository contents/metadata and does not establish a GitHub Actions merge-capable path.

### Complete actor enumeration

```text
all collaborators with write/maintain/admin    UNKNOWN
all GitHub Apps with merge-capable permission  UNKNOWN
all automation/service identities              UNKNOWN
all external credentials / PAT holders         UNKNOWN
```

The available connector can verify permission for a named collaborator but does not expose a complete collaborator / installation enumeration in this capture.

**STOP CONDITION REMAINS:** complete merge-capable actor enumeration is not established.

## 6. Bypass actors

Classic branch protection is disabled, so classic protected-branch bypass actors are:

```text
classic protection bypass actors    N/A (classic protection OFF)
```

Because applicable repository rulesets remain UNKNOWN, the following remain UNKNOWN:

```text
ruleset bypass actors
admin bypass mode
GitHub App bypass grants
user/role bypass grants
pull-request-only bypass paths
```

The known repository owner/admin is merge-capable, but this receipt does not label that actor a `ruleset bypass actor` without an applicable ruleset to test against.

**STOP CONDITION REMAINS:** ruleset bypass actors cannot be enumerated until repository ruleset state is observed.

## 7. PR-enforcement suitability

The current workflow trigger is:

```text
workflow_dispatch + push(main)
```

It has no `pull_request` trigger. Therefore the current external-installation proof is not yet established as a PR-enforcement workflow for proposed changes before merge.

```text
workflow exists                         ESTABLISHED
workflow runs on main/manual            ESTABLISHED
provider job name                       ESTABLISHED
provider job success                    ESTABLISHED
PR-triggered AURUM enforcement run      NOT PRESENT IN CURRENT WORKFLOW
```

No provider required-check configuration should be applied against this workflow until a separate PR-enforcement workflow contract is accepted.

## 8. Pre-mutation enforcement conclusion

```text
classic provider enforcement              OFF
mandatory AURUM required check             NOT ESTABLISHED
provider-generated required-check identity ESTABLISHED: prove-external-installation
applicable repository rulesets             UNKNOWN
known merge-capable owner/admin             ESTABLISHED
observed workflow merge authority           NOT ESTABLISHED / read-only token
complete merge-capable actor set            UNKNOWN
complete bypass actor set                   UNKNOWN
PR-triggered enforcement harness            NOT PRESENT
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

## 9. Contract disposition

```text
PRE-MUTATION RECEIPT        CAPTURED / UPDATED
CHECK IDENTITY GAP          CLOSED
WORKFLOW TOKEN GAP          CLOSED FOR OBSERVED RUN
PROVIDER CONFIG MUTATION    STOP
WORKFLOW MUTATION           STOP
TEST EXECUTION              STOP
v1.1                        FROZEN
C_v1.1                      UNCHANGED
FirstDivergence             NONE
```

No provider-enforcement configuration is authorized by this receipt.

Remaining deployment-observation gaps:

1. establish applicable repository-level ruleset state;
2. establish the merge-capable actor set to the extent required by the deployment contract;
3. establish applicable ruleset bypass actors / bypass modes.

Separately, before provider enforcement can be configured, a PR-enforcement workflow contract must be defined because the current external-installation proof does not run on pull requests.

If any remaining observation cannot be established, retain `STOP / NOT ESTABLISHED` rather than repair or infer.