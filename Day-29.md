# Day 29: Git Revert Latest Commit

## Task

The Nautilus application development team reported that the latest commit pushed to the Git repository was incorrect. The task was to revert the repository **HEAD** to the previous commit using **git revert** and create a new commit with the message:

`revert ecommerce`

---

## Objective

* Navigate to the Git repository.
* Revert the latest commit (HEAD).
* Create a new revert commit with the required commit message.
* Verify that the revert was successful.

---

## Steps Performed

### 1. Navigate to the repository

```bash
cd /usr/src/kodekloudrepos/ecommerce
```

### 2. Verify commit history

```bash
git log --oneline
```

This confirmed the latest commit (HEAD) and the previous commit with the **initial commit** message.

### 3. Revert the latest commit

```bash
git revert HEAD --no-edit
```

### 4. Update the commit message

```bash
git commit --amend -m "revert ecommerce"
```

### 5. Verify the new commit

```bash
git log --oneline -3
```

The latest commit was successfully created with the message:

```text
revert ecommerce
```

---

## Commands Used

```bash
cd /usr/src/kodekloudrepos/ecommerce

git log --oneline

git revert HEAD --no-edit

git commit --amend -m "revert ecommerce"

git log --oneline -3
```

---

## Outcome

* Successfully reverted the latest Git commit without modifying repository history.
* A new revert commit was created with the required message:

  * `revert ecommerce`
* Verified that the repository HEAD now points to the revert commit while preserving the previous commit history.

---

## Key Learnings

* `git revert` safely undoes changes by creating a new commit.
* Unlike `git reset`, `git revert` preserves commit history, making it the preferred approach for shared repositories.
* Always verify commit history after performing Git operations using `git log`.
