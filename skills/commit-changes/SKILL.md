---
name: commit-changes
description: Commits all changes made within the current chat thread, grouping related changes together into an individual commit per group. Use when the user runs /commit-changes or asks to commit the changes made in this conversation.
---

# /commit-changes — Commit Changes From This Thread

Commit all the changes accordingly, grouping related changes together and creating an individual commit for each group of changes.

## Steps

### 1. Review the diff

Run `git status` and `git diff` (and `git diff --staged` if anything is already staged) to see every changed, added, and removed file.

### 2. Scope to this thread only

Identify which of those changes were made **within this chat thread**. Do not sweep in unrelated, pre-existing uncommitted changes that were already present in the working tree before this conversation started — leave those untouched.

### 3. Group related changes

Group the in-scope files into logical sets by feature/concern (e.g. "new skill files", "README updates", "bugfix in component X"). Each group becomes one commit.

### 4. Commit each group individually

For each group:

```bash
git add <files in group>
git commit -m "<concise, descriptive message for this group>"
```

Use clear, conventional commit messages — no filler like "misc changes" or "updates".

### 5. Confirm

Run `git log --oneline -n <N>` and show the resulting commits to confirm each logical group landed as its own commit.

## Important

**ONLY commit the changes made within this chat thread.** If there are other uncommitted changes in the working tree that predate this conversation, leave them uncommitted — use `/commit-remain-changes` for those instead.
