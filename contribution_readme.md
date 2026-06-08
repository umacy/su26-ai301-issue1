# Contribution [#]: 335

**Contribution Number:** 1 
**Student:** Uzair Macy
**Issue:** [[GitHub issue link](https://github.com/ocaml/dune/issues/12567)]
**Status:** [Phase I]

---

## Why I Chose This Issue

This issue tackles adding support for newer Dune keywords such as parameters and library_parameter. This is important because users editing Dune files in Emacs don't have the best visual feedback currently, which makes configuration files harder to read and maintain. I chose this issue because its an approachable contribution to working on a developer tool, which is something I've always been interested in.

---

## Understanding the Issue

### Problem Description

The emacs dune-mode in dune.el doesn't highlight the OxCaml parameterized-library keywords (library_parameter, parameters, instantiate), because they were added to dune's grammar but never to the mode's keyword lists.

### Expected Behavior

library_parameter should highlight as a stanza (keyword-face), parameters as a field (function-name-face), and instantiate as a builtin (builtin-face), just like library, name, and file do.

### Current Behavior

All three render as plain, unhighlighted text.

### Affected Components

Only the three hand-maintained regexp-opt lists in dune.el: dune-stanzas-regex (:59), dune-fields-regex (:71), dune-builtin-regex (:110).

---

## Reproduction Process

### Environment Setup

[Notes on setting up your local development environment - challenges you faced, how you solved them]

### Steps to Reproduce

1. [Step 1]
Run these commands in Powershell in this order (only tested with Windows):
Set-ExecutionPolicy -Scope CurrentUser RemoteSigned
irm get.scoop.sh | iex
scoop bucket add extras
scoop install emacs

2. [Step 2]
Create a file named dune with this content:
(library_parameter
 (name param))

(library
 (name lib)
 (parameters param))

(executable
 (name bin)
 (libraries (instantiate lib impl)))

Then run:
& "C:\Program Files\Emacs\emacs-30.2\bin\emacs.exe" -Q -L editor-integration/emacs -l dune.el dune

3. [Observed result]

executable, name, and libraries are colored, but library_parameter, parameters, and instantiate are plain white/default text.

### Reproduction Evidence

- **Commit showing reproduction:** 
- **Screenshots/logs:** [If applicable]
- **My findings:** [What you discovered during reproduction]

---

## Solution Approach

### Analysis

[Your analysis of the root cause - what's causing the issue?]

### Proposed Solution

[High-level description of your fix approach]

### Implementation Plan

Add the three OxCaml parameterised-library keywords to the corresponding regexp-opt keyword lists in dune.el, mirroring how the existing virtual-library keyword implements is handled:

library_parameter → add to dune-stanzas-regex (dune.el:62-67) so it highlights as a stanza (keyword-face) and gets correct SMIE indentation.
parameters → add to dune-fields-regex next to implements (dune.el:86) so it highlights as a field (function-name-face).
instantiate → add to dune-builtin-regex in the "Dependency specification" group (dune.el:129) so it highlights as a builtin (builtin-face).

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [X] Progress

[What you built this week, challenges faced, decisions made]

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** [List]
- **Key commits:** [Links to important commits]
- **Approach decisions:** [Why you chose certain approaches]

---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
