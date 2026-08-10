Day 31 -- Git Pull Request, Code Review & Merge with Gitea

📌 Task Overview

The goal of this task was to implement a proper Git collaborationworkflow where developers do not push changes directly to the masterbranch. Instead, changes are submitted through a Pull Request (PR),reviewed and approved by another user, and only then merged intomaster.

Scenario

User: Max

Reviewer: Tom

Repository: sarah/story-blog

Feature branch: story/fox-and-grapes

Target branch: master

PR title: Added fox-and-grapes story

🎯 Objectives

Access the existing Git repository on the storage server.

Verify the repository contents and Git commit history.

Confirm Max's story exists on the story/fox-and-grapes branch.

Create a Pull Request from story/fox-and-grapes to master.

Assign Tom as the reviewer.

Review and approve the Pull Request using Tom's account.

Merge the approved Pull Request into master.

🔧 Step 1 -- Verify Repository and Git History

SSH into the storage server as Max and locate the already clonedrepository.

ssh max@<storage-server>

Navigate to the repository and check its status:

cd <repository>
git status
git branch -a

Review the commit history:

git log --oneline --all

For detailed author and commit information:

git log --all --pretty=fuller

To specifically inspect the story branch:

git log story/fox-and-grapes --pretty=fuller

The repository history was checked to verify the author information,commit messages, and the existing story changes.

🌿 Step 2 -- Verify the Feature Branch

The feature branch used for Max's changes was:

story/fox-and-grapes

The story file was:

fox-and-grapes.txt

The branch contained Max's new story and was already pushed to theremote Gitea repository.

🔀 Step 3 -- Create the Pull Request

The Gitea web interface was opened and logged in using Max's account.

A new Pull Request was created with:

PR Title:       Added fox-and-grapes story
Source Branch:  story/fox-and-grapes
Target Branch:  master

The resulting Pull Request was:

Added fox-and-grapes story #1

The PR was initially in the Open state.

👤 Step 4 -- Assign Tom as Reviewer

From the Pull Request page, the Reviewers section was used toassign:

Reviewer: tom

The PR then showed that a review was waiting.

This ensures that the changes are reviewed before they are merged intothe final master branch.

🔍 Step 5 -- Review the Changes

The Gitea Files Changed tab was opened to inspect the changes.

The Pull Request contained:

1 changed file
21 additions
0 deletions

The changed file was:

fox-and-grapes.txt

Tom reviewed the changes and selected:

Approve

The review was successfully submitted.

The Pull Request then displayed:

tom approved these changes

🚀 Step 6 -- Merge the Pull Request

After Tom approved the changes, the PR showed that it could be mergedautomatically.

The merge option was:

Create merge commit

The Pull Request was then merged into:

master

This completed the controlled Git workflow.

🔄 Git Workflow Implemented

Max
 │
 │ Push changes
 ▼
story/fox-and-grapes
 │
 │ Create Pull Request
 ▼
Pull Request
 │
 │ Assign reviewer
 ▼
Tom
 │
 │ Review + Approve
 ▼
Approved PR
 │
 │ Merge
 ▼
master

💡 What I Learned

How Pull Requests are used for controlled code integration.

Why direct pushes to master should be avoided in a collaborativeenvironment.

How to create a PR from a feature branch to master.

How to assign a reviewer in Gitea.

How to review and approve changes.

How an approved Pull Request is merged into the target branch.

How Git history can be inspected using git log.

How branch-based development improves code quality andcollaboration.