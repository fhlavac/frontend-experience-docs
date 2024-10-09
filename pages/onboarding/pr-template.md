# Pull Request Template

This documentation describes the purpose and structure of the Pull Request (PR) template used in repositories maintained by the Platform Experience UI team. The template is designed to ensure a consistent and thorough review process, maintain quality, and simplify communication among team members.

## PR template sections

### 1. **Description**
Provides a brief summary of the proposed changes in the PR. 

**Required Information**:
 - 2-3 sentences summarizing the proposed changes.
 - Links to any affected User Interface (UI) areas.
 - Steps to reproduce the issue, if applicable.
 - Link to any related issue or story, preferably a JIRA link (`RHCLOUD-XXXXXX`).
   
**Example**:
```md
This PR improves the error messages displayed when the create user flow fails.

[RHCLOUD-XXXXX](https://issues.redhat.com/browse/RHCLOUD-XXXXX)
```

---

### 2. **Screenshots**
To visually demonstrate the changes made to the UI, providing "Before" and "After" comparisons.

**Required Information**:
- Capture relevant UI screenshots of key changes.
- Highlight the specific UI areas that have been impacted.

**Example**:
```md
#### Before:
(Insert screenshot of the UI before the change)

#### After:
(Insert screenshot of the UI after the change)
```

---

### 3. **Checklist ☑️**
Ensure that important quality and process checks are completed before merging the PR. The checklist helps maintain code quality and consistency.

**Required Checks**:
- Each PR should focus on fixing a single issue or story.
- Review the code for any extraneous elements (e.g., console logs, comments, unnecessary files).
- Ensure adherence to UI best practices (responsive design, feature gating, input validation, etc.).
- Limit the number of commits and ensure that they are well-named and meaningful.
- Verify that all PR checks (build, lint, tests, etc.) pass locally before submitting.
**Optional Checks**:
- If the changes impact QE (Quality Engineering), notify QE.
- If the changes impact the end-user experience or UI design, notify UX designers.

**Example**:
```md
### Checklist ☑️
- [ ] PR only fixes one issue or story <!-- open new PR for others -->
- [ ] Change reviewed for extraneous code <!-- console statements, comments, files, incorrect file renaming (not using `git mv`), whitespace, etc. -->
- [ ] UI best practices adhered to <!-- TODO: add a link; responsiveness, input sanitization, prioritizing PatternFly and FEC, feature gating, etc. -->
- [ ] Commits squashed and meaningfully named <!-- (2-3 commits per PR maximum, 1 is ideal) -->
- [ ] All PR checks pass locally (build, lint, test, E2E)

##
- [ ] _(Optional) QE: Needs QE attention (OUIA changed, perceived impact to tests, no test coverage)_
- [ ] _(Optional) QE: Has been mentioned_
- [ ] _(Optional) UX: Needs UX attention (end user UX modified, missing designs)_
- [ ] _(Optional) UX: Has been mentioned
##
```

## Full PR template markdown source

```md
### Description
<!-- Must include 2-3 sentence summary of proposed changes -->
<!-- Must include links to impacted UI(s) or information regarding the impacted UI -->
<!-- Must include any relevant steps to reproduce (if not clear in tracked issue or story) -->
<!-- Must include RHCLOUD-XXXXXX link (if proposed change involves tracked issue or story) -->
description text...

[RHCLOUD-XXXXX](https://issues.redhat.com/browse/RHCLOUD-XXXXX)

---

### Screenshots
<!-- Before and after proposed changes is ideal -->
<!-- Any key UI permutations should be captured -->
<!-- Draw attention to the area of UI that has changed -->
#### Before:


#### After:


---

### Checklist ☑️
- [ ] PR only fixes one issue or story <!-- open new PR for others -->
- [ ] Change reviewed for extraneous code <!-- console statements, comments, files, incorrect file renaming (not using `git mv`), whitespace, etc. -->
- [ ] UI best practices adhered to <!-- TODO: add a link; responsiveness, input sanitization, prioritizing PatternFly and FEC, feature gating, etc. -->
- [ ] Commits squashed and meaningfully named <!-- (2-3 commits per PR maximum, 1 is ideal) -->
- [ ] All PR checks pass locally (build, lint, test, E2E)

##
- [ ] _(Optional) QE: Needs QE attention (OUIA changed, perceived impact to tests, no test coverage)_
- [ ] _(Optional) QE: Has been mentioned_
- [ ] _(Optional) UX: Needs UX attention (end user UX modified, missing designs)_
- [ ] _(Optional) UX: Has been mentioned_
##
```
