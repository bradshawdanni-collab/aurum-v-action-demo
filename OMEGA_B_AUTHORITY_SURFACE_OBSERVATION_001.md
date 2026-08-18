# ΩB-AUTHORITY-SURFACE-OBSERVATION-001

**Status:** CAPTURED / ENUMERATED WITH EXPLICIT AUTHORITY-BEARING APPS  
**Repository:** `bradshawdanni-collab/aurum-v-action-demo`  
**Target:** `main`  
**Mode:** observation only; no provider enforcement mutation  
**Related contract:** `ΩB-DEPLOYMENT-VERIFICATION-001 — Mandatory AURUM Before Merge`

## 1. Repository rulesets

User-supplied GitHub Settings evidence shows:

```text
You haven't created any rulesets
```

Classification:

```text
repository_rulesets      NONE OBSERVED / ESTABLISHED
ruleset_enforcement      N/A
ruleset_bypass_actors    N/A
```

Classic branch protection was already observed OFF in the pre-mutation receipt.

## 2. Direct human access

User-supplied GitHub Settings → Collaborators evidence shows:

```text
You haven't invited any collaborators yet
```

Together with the repository-owner/admin observation:

```text
human_merge_capable_actor
    bradshawdanni-collab   owner/admin

additional_direct_collaborators
    NONE OBSERVED
```

## 3. Deploy keys

User-supplied GitHub Settings → Deploy keys evidence shows:

```text
There are no deploy keys for this repository
```

Classification:

```text
deploy_keys              NONE
write_enabled_deploy_keys NONE
```

## 4. Installed GitHub Apps

User-supplied GitHub Settings evidence enumerates these installed apps with repository access:

```text
Base44 Builder
ChatGPT Codex Connector
Google Cloud Build
Google Cloud Developer Connect
Semantic Pull Requests
```

### 4.1 Base44 Builder

Observed permissions:

```text
Read access:
    metadata

Read and write access:
    administration
    code
    repository hooks
```

Classification:

```text
authority_bearing        YES
contents/code write      OBSERVED
administration write     OBSERVED
direct merge capability  ESTABLISHED BY CONTENTS/CODE-WRITE AUTHORITY
```

GitHub documents the REST `Merge a pull request` endpoint as requiring repository `Contents: write` permission. The observed GitHub UI permission labelled `code` is the repository-content/code write authority exposed for the installed app.

### 4.2 ChatGPT Codex Connector

Observed permissions:

```text
Read access:
    checks
    commit statuses
    metadata

Read and write access:
    actions
    code
    issues
    pull requests
    workflows
```

Classification:

```text
authority_bearing        YES
contents/code write      OBSERVED
pull-request write       OBSERVED
workflow write           OBSERVED
direct merge capability  ESTABLISHED BY CONTENTS/CODE-WRITE AUTHORITY
```

### 4.3 Google Cloud Build

Observed permissions:

```text
Read access:
    code
    issues
    metadata
    pull requests

Read and write access:
    checks
    commit statuses
```

Classification:

```text
contents/code write      NOT OBSERVED
pull-request write       NOT OBSERVED
direct merge capability  NOT ESTABLISHED FROM OBSERVED PERMISSIONS
status/check authority   YES
```

### 4.4 Google Cloud Developer Connect

Observed permissions:

```text
Read access:
    code
    issues
    metadata
    pull requests

Read and write access:
    checks
    commit statuses
```

Classification:

```text
contents/code write      NOT OBSERVED
pull-request write       NOT OBSERVED
direct merge capability  NOT ESTABLISHED FROM OBSERVED PERMISSIONS
status/check authority   YES
```

### 4.5 Semantic Pull Requests

Observed permissions:

```text
Read access:
    file `.github/semantic.yml`
    metadata

Read and write access:
    commit statuses
    pull requests
```

Classification:

```text
contents/code write      NOT OBSERVED
pull-request write       OBSERVED
direct REST merge        NOT ESTABLISHED FROM OBSERVED PERMISSIONS
status/PR authority      YES
```

The direct REST merge endpoint requires `Contents: write`; that permission is not shown for this app in the supplied evidence.

## 5. Repository-local authority surface

Provider-visible repository-local authority is now enumerated as:

```text
DIRECT MERGE-CAPABLE / AUTHORITY-BEARING
    bradshawdanni-collab     owner/admin
    Base44 Builder           code/contents write + administration write
    ChatGPT Codex Connector  code/contents write + pull-request/workflow write

OTHER INSTALLED AUTOMATION
    Google Cloud Build              checks/status write; code read
    Google Cloud Developer Connect  checks/status write; code read
    Semantic Pull Requests          PR/status write; no code-write observed

RULESETS
    NONE OBSERVED

CLASSIC BRANCH PROTECTION
    OFF (per pre-mutation receipt)

DEPLOY KEYS
    NONE

DIRECT COLLABORATORS
    NONE beyond owner/admin observed
```

Therefore:

```text
AuthoritySurface(repository-local/provider-visible) = ENUMERATED
AuthoritySurface(owner-only)                         = FALSE
```

## 6. Deployment consequence

Because at least the owner/admin and two installed GitHub Apps have direct authority-bearing write access while provider enforcement is not configured, the current deployment does not establish:

\[
\neg ValidAURUMAuthorization \Rightarrow \neg GitHubMerge
\]

This is not a v1.1 implementation defect. It is a deployment-boundary fact in `Ω_B`.

No unauthorized merge has been observed, so result vocabulary remains:

```text
FAILED               NO
ESTABLISHED           NO
PARTIALLY_ESTABLISHED NO — enforcement has not yet been configured/tested
NOT_ESTABLISHED       YES
```

## 7. Evidence boundary

This record enumerates the repository-local, provider-visible authority surface shown in the supplied GitHub Settings evidence. It does not prove absence of user-level OAuth credentials, PAT instances, compromised credentials, undisclosed external services, or future permission changes. Those are outside the exact repository-local settings surface captured here.

## 8. Disposition

```text
AUTHORITY SURFACE OBSERVATION   COMPLETE FOR REPOSITORY-LOCAL SETTINGS
repository rulesets             NONE OBSERVED
classic branch protection       OFF
human direct collaborators      NONE beyond owner/admin
write deploy keys               NONE
installed apps                  ENUMERATED
merge-capable apps              Base44 Builder; ChatGPT Codex Connector
provider enforcement mutation   NONE
workflow mutation               NONE
v1.1                            FROZEN
C_v1.1                          UNCHANGED
FirstDivergence                  NONE
```

**NEXT GATE:** define/freeze a PR-enforcement workflow contract and an explicit provider-enforcement design that accounts for the enumerated authority-bearing actors before any Settings mutation.