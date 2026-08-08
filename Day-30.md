Day 30 – Git Cherry-Pick Task

📌 Task

Nautilus team had two branches in the ecommerce repository:

master

feature

The requirement was to take only the commit Update info.txt from the feature branch and apply it to master.

⚠️ Problem

The feature branch had multiple commits, but we did not want to merge the complete branch.

Using:

git merge feature

could bring all the changes from feature.

So, we needed to use Git Cherry-Pick.

✅ Solution

First, entered the actual repository:

cd /usr/src/kodekloudrepos/ecommerce

Checked branches:

git branch

Found:

* feature
  master

Checked the commit history:

git log --oneline --all

Found the required commit:

cecd176 Update info.txt

Switched to master:

git checkout master

Cherry-picked the required commit:

git cherry-pick cecd176

The commit was successfully applied:

[master 96e1649] Update info.txt

Finally, pushed the changes:

git push origin master

🎯 Result

The required commit from feature was successfully added to master without merging the entire feature branch.

💡 Key Learning

git merge → merges branch changes.

git cherry-pick <commit-hash> → applies only a specific commit.