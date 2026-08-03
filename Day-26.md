# Day 26 - Fork a Git Repository Using Gitea

## Scenario

A new developer named **Jon** joined the Nautilus project team and needed access to an existing project. The task was to fork the repository `sarah/story-blog` into Jon's account using the Gitea web interface.

---

## Objective

- Log in to the Gitea server as `jon`
- Locate the repository `sarah/story-blog`
- Fork the repository under the `jon` user
- Verify that the fork was created successfully
- Capture a screenshot for submission

---

## Steps Performed

### 1. Opened Gitea

- Clicked the **Gitea UI** button from the top navigation bar.

### 2. Logged In

Credentials used:

```text
Username: jon
Password: Jon_pass123
```

### 3. Located the Repository

Searched for the repository:

```text
sarah/story-blog
```

### 4. Forked the Repository

- Opened the repository.
- Clicked the **Fork** button.
- Selected **jon** as the repository owner.
- Created the fork.

### 5. Verified the Fork

Confirmed that the new repository was available as:

```text
jon/story-blog
```

### 6. Captured Screenshot

Took a screenshot of the successfully forked repository for verification.

---

## Result

Successfully forked the repository **sarah/story-blog** into **jon/story-blog** using the Gitea web interface.

---

## Key Concepts Learned

- Git Repository Forking
- Gitea Web Interface
- Repository Ownership
- Open Source Contribution Workflow
- Difference between Fork and Clone

---



## Interview Questions

### What is Fork in Git?

A **Fork** creates a copy of an existing repository under your own Git account. It allows you to work independently without affecting the original repository.

### Difference Between Fork and Clone

| Fork | Clone |
|------|-------|
| Creates a copy on the Git server | Downloads a repository to the local machine |
| Used for contributing to external repositories | Used for local development |
| Repository exists under your account | No new repository is created |

---

