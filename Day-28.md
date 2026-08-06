# Day XX - Git Remote Management and Push to New Remote

## Objective
Update the Git repository by adding a new remote, copy a file into the repository, commit the changes, and push the `master` branch to the newly added remote.

---

## Tasks Performed

### 1. Navigate to the Git Repository
```bash
cd /usr/src/kodekloudrepos/demo
```

### 2. Add a New Git Remote
Added a new remote named **dev_demo** pointing to the Git repository located at `/opt/xfusioncorp_demo.git`.

```bash
git remote add dev_demo /opt/xfusioncorp_demo.git
```

Verify the remote:

```bash
git remote -v
```

---

### 3. Copy the File into Repository

Copied the `index.html` file from the `/tmp` directory into the repository.

```bash
cp /tmp/index.html .
```

---

### 4. Stage and Commit the Changes

Added the new file to the staging area and committed it to the `master` branch.

```bash
git add index.html
git commit -m "Added index.html"
```

---

### 5. Push Changes to the New Remote

Pushed the `master` branch to the newly created remote repository.

```bash
git push dev_demo master
```

---

## Commands Used

```bash
cd /usr/src/kodekloudrepos/demo
git remote add dev_demo /opt/xfusioncorp_demo.git
git remote -v
cp /tmp/index.html .
git add index.html
git commit -m "Added index.html"
git push dev_demo master
```

---

## Git Concepts Learned

- Adding a new Git remote using `git remote add`
- Verifying configured remotes with `git remote -v`
- Copying project files into a repository
- Staging files using `git add`
- Creating commits with `git commit`
- Pushing a branch to a specific remote repository

---

