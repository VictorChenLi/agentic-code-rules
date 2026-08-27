---
name: commit-remain-changes
description: Commits all remaining/outstanding uncommitted changes in the working tree, grouping related changes together into an individual commit per group. Use when the user runs /commit-remain-changes or asks to commit whatever is still left uncommitted.
---

# /commit-remain-changes — Commit All Remaining Changes

Commit all the REMAINING changes accordingly, grouping related changes together and creating an individual commit for each group of changes.

## Steps

### 1. Review the full diff

Run `git status` and `git diff` (and `git diff --staged`) to see every outstanding changed, added, and removed file in the working tree — regardless of which chat thread produced them.

### 2. Group related changes

Group the files into logical sets by feature/concern. Each group becomes one commit. Do not lump unrelated changes into a single catch-all commit.

### 3. Commit each group individually

For each group:

```bash
git add <files in group>
git commit -m "<concise, descriptive message for this group>"
```

### 4. Confirm

Run `git status` again to confirm the working tree is clean (or note anything intentionally left uncommitted, e.g. files the user asked to exclude), and `git log --oneline -n <N>` to show the resulting commits.

## Notes

- Unlike `/commit-changes` (which is scoped to the current chat thread only), this skill commits **everything** currently uncommitted in the working tree.
- Still group logically — do not create one giant commit for unrelated changes just because they're all "remaining".
