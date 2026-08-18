# ΩB-DEPLOYMENT-VERIFICATION-001 — Mandatory AURUM Before Merge

**Status:** ACCEPTED / FROZEN  
**Target repository:** `bradshawdanni-collab/aurum-v-action-demo`  
**Protected target:** `main`  
**Contract authority:** ACCEPTED  
**Provider-configuration authority:** NONE under this record  
**Core v1.1 changes:** PROHIBITED  
**C_v1.1 expansion:** NONE  
**FirstDivergence mutation:** NONE

## 1. Objective

Establish, for the exact tested deployment:

\[
\boxed{
\neg ValidAURUMAuthorization
\Rightarrow
\neg GitHubMerge
}
\]

This contract tests deployment enforcement only.

It does not alter `C_v1.1` or reinterpret `Ω_A`.

## 2. Enforcement architecture under test

Initial architecture:

```text
SignedApproval
    -> AURUMVerification
    -> RequiredGitHubCheck
    -> MergeEligibility
```

Primary enforcement mechanism:

```text
PROVIDER ENFORCEMENT
```

Credential isolation is outside this first experiment.

## 3. Required deployment state

Before any enforcement mutation or falsification run, record and freeze:

- repository;
- target branch;
- exact AURUM Action ref / commit;
- workflow file SHA;
- provider-generated required-check identity;
- branch-protection / ruleset identity;
- branch-protection / ruleset content;
- bypass actors;
- repository administrators;
- merge-capable actors;
- allowed merge methods;
- configuration timestamp.

No test result is valid without this deployment receipt.

If the required-check identity, applicable ruleset state, bypass actors, or merge-capable actors cannot be established, STOP and classify rather than infer.

## 4. Required-check invariant

For the target branch:

\[
MergeEligible
\Rightarrow
AURUMCheck = SUCCESS
\]

The test must establish that the AURUM check is mandatory, not merely present.

```text
workflow exists          != enforcement
workflow runs            != enforcement
AURUM returns VERIFIED   != enforcement

required status check
+ provider refusal when absent/failing
                        = enforcement evidence
```

## 5. Positive case — P1

### Preconditions

A valid signed authorization is bound to the exact:

```text
(repository, PR, head)
```

AURUM verification returns:

```text
VERIFIED
```

### Expected provider result

```text
AURUM required check       PASS
merge eligibility          ALLOWED
```

Acceptance:

\[
ValidApproval
\land
AURUMCheck = PASS
\Rightarrow
GitHubAllowsMerge
\]

This proves the authorised path exists. It does not alone prove exclusivity.

## 6. Negative cases

| Case | Mutation / condition | Required result |
|---|---|---|
| N1 | No approval bundle | AURUM fails; merge blocked |
| N2 | Malformed artifact | AURUM fails; merge blocked |
| N3 | Tampered signed artifact | AURUM fails; merge blocked |
| N4 | Repository mismatch | AURUM fails; merge blocked |
| N5 | PR mismatch | AURUM fails; merge blocked |
| N6 | Head SHA mismatch | AURUM fails; merge blocked |
| N7 | Signed refusal | AURUM fails; merge blocked |
| N8 | Expired approval, if supported by the tested Action contract | AURUM fails; merge blocked |
| N9 | Required AURUM check absent / pending | merge blocked |
| N10 | Direct UI merge attempt before AURUM passes | merge blocked |
| N11 | Direct API / CLI merge attempt before AURUM passes | merge blocked |
| N12 | Privileged / admin attempt | result recorded without assumption |

Every negative case must preserve:

- AURUM result;
- denial code;
- GitHub check state;
- merge-attempt method;
- provider response;
- `merge_occurred: true|false`;
- blocking rule;
- actor identity / class;
- timestamp;
- target SHA.

## 7. Bypass test rule

The strongest deployment test is not merely:

\[
AURUMFails
\]

It is:

\[
AURUMFails
\land
ActorAttemptsMerge
\land
GitHubRefusesMerge
\]

The provider refusal is the load-bearing evidence.

For every identified merge-capable actor `m`:

\[
\forall m:
\neg ValidAURUMAuthorization
\Rightarrow
\neg Merge_m
\]

If an administrator can bypass the required check and merge anyway:

\[
\exists m:
\neg ValidAURUMAuthorization
\land
Merge_m
\]

then the result is not automatically an AURUM v1.1 defect. It means `B_production` has not been closed by the tested provider configuration.

## 8. Controlled result vocabulary

### ESTABLISHED

Every tested merge-capable path is subordinate to successful AURUM verification.

### PARTIALLY_ESTABLISHED

Provider enforcement works for ordinary paths, but one or more privileged paths remain unresolved.

### NOT_ESTABLISHED

Required evidence or configuration was unavailable or insufficient to prove exclusivity.

### FAILED

A tested path successfully merged without the required valid AURUM authorization.

`FAILED` requires an observed unauthorized merge path, not merely the existence of an unknown.

## 9. Acceptance condition

The deployment gate passes only if:

\[
\boxed{
\forall p \in IdentifiedMergePaths:
Merge(p)
\Rightarrow
ValidAURUMAuthorization(p)
}
\]

and:

\[
\boxed{
\forall p:
\neg ValidAURUMAuthorization(p)
\Rightarrow
ProviderBlocks(p)
}
\]

for the exact actors and configuration under review.

## 10. Evidence boundary

An `ESTABLISHED` result proves only:

> For the exact repository, target branch, identities, configuration, Action version and provider state tested, the identified merge paths were enforced downstream of successful AURUM verification.

It does not prove:

- all GitHub deployments are non-bypassable;
- all future configurations remain equivalent;
- all administrators globally lack override powers;
- credential isolation;
- unknown identities do not exist;
- AURUM-V is impossible to bypass.

## 11. Stop conditions

Immediately STOP and classify rather than repair if:

- required-check identity is ambiguous;
- applicable ruleset state cannot be established;
- bypass actors cannot be enumerated;
- test would require modifying v1.1;
- test requires introducing a merge credential;
- provider behavior differs from the frozen contract;
- an unexpected merge path appears.

No corrective implementation is allowed inside the falsification run.

## 12. Frozen disposition

```text
ΩB-DEPLOYMENT-VERIFICATION-001

contract             ACCEPTED / FROZEN
v1.1                 FROZEN
C_v1.1 expansion     NONE
FirstDivergence      NONE
provider mutation    NONE
provider testing     NONE

NEXT GATE
    capture pre-mutation deployment receipt
    then obtain explicit authority for provider-enforcement mutation
```

This contract does not authorize branch-protection, ruleset, required-check, bypass, credential, workflow-runtime, or v1.1 implementation changes.