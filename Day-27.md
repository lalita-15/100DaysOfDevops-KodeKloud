# Day 21 – Git Branching, Merging & Remote Push

## Objective
Create a new branch named `nautilus` from the `master` branch, add a new file, merge the branch back into `master`, and push both branches to the remote repository.

## Steps Performed

### 1. Navigate to the Repository

```bash
cd /usr/src/kodekloudrepos/news
```

### 2. Switch to Master Branch

```bash
git checkout master
```

### 3. Create and Switch to the `nautilus` Branch

```bash
git checkout -b nautilus
```

### 4. Copy the Required File

```bash
cp /tmp/index.html .
```

### 5. Stage and Commit the Changes

```bash
git add index.html
git commit -m "Add index.html"
```

### 6. Switch Back to Master

```bash
git checkout master
```

### 7. Merge the `nautilus` Branch

```bash
git merge nautilus
```

### 8. Push Both Branches to the Remote Repository

```bash
git push origin master
git push origin nautilus
```

## Verification Commands

```bash
git branch
git log --oneline --graph --all
git status
```

## Key Learnings

- Created a new Git branch from `master`.
- Added and committed a new file in the feature branch.
- Merged the feature branch into the `master` branch.
- Pushed both local branches to the remote repository.
- Practiced a common Git workflow used in real-world DevOps projects.

