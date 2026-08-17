Day 33 – Git Push & Conflict Resolution with Gitea

Task

The task was to fix Max's story-blog repository and successfully push the changes to the Gitea remote repository.

Main requirements:

Push local changes to the origin repository.

Ensure story-index.txt contains all 4 story titles.

Correct the typo Mooose to Mouse.

Resolve the Git conflict without losing existing changes.

Repository

cd /home/max/story-blog
git status
git remote -v

Remote repository:

http://gitea:3000/sarah/story-blog.git

Step 1: Fix the Typo

The task mentioned a typo in The Lion and the Mooose.

sed -i 's/Mooose/Mouse/g' story-index.txt

Then the file was staged and committed:

git add story-index.txt
git commit -m "Fix story index titles and typo"

Step 2: Pull Remote Changes

Tried to synchronize the local branch with the remote:

git pull --rebase origin master

Git reported a conflict in:

story-index.txt

The conflict happened because local and remote history both contained changes to the same file.

Step 3: Find the Missing Fourth Story

The index initially showed only 3 stories, so Git history was checked instead of guessing the fourth title.

git fsck --no-reflogs --unreachable

An unreachable commit was found:

8699ad8 Fix story index titles and typo

The file from that commit was inspected:

git show 8699ad83:story-index.txt

This revealed the correct fourth story:

The Donkey and the Dog

Step 4: Create the Correct Story Index

The final story-index.txt was set to:

1. The Lion and the Mouse
2. The Frogs and the Ox
3. The Fox and the Grapes
4. The Donkey and the Dog

The conflict was then resolved:

git add story-index.txt
git rebase --continue

During the rebase, another conflict appeared in story-index.txt, so the same correct four-title version was kept and the rebase was continued.

Step 5: Push Changes

After the rebase completed:

git push origin master

The push was successful.

The final verification showed:

Everything up-to-date

and:

On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean

What I Learned

git pull --rebase keeps local commits on top of the latest remote changes.

Git conflicts must be resolved manually when changes overlap.

git rebase --continue continues a rebase after resolving a conflict.

git fsck can help find unreachable commits.

git show <commit>:<file> can recover the contents of a file from a previous commit.