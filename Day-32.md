## Day 31 – Git Stash: Restore and Push Stashed Changes

## Task

The Nautilus application development team had a Git repository on the Storage Server:

/usr/src/kodekloudrepos/media

A developer had stashed some in-progress changes. The task was to restore the changes from stash@{1}, commit them, and push the changes to the origin remote.

## Steps Performed

1. Connect to the Storage Server

ssh natasha@ststor01
sudo su -

Switched to root because the repository and remote Git repository required the appropriate permissions.

2. Navigate to the Repository

cd /usr/src/kodekloudrepos/media

3. Check Available Stashes

git stash list

Confirmed that stash@{1} was available.

4. Restore the Required Stash

git stash apply stash@{1}

The stashed changes restored a new file:

welcome.txt

The restored content was:

These were the initial changes!

5. Verify the Changes

git status

The output showed welcome.txt under changes to be committed.

6. Stage the Changes

git add .

7. Commit the Changes

git commit -m "Committing changes of stash@{1}."

Commit created successfully:

4f173cb Committing changes of stash@{1}.

8. Push to Origin

git push origin master

Push completed successfully:

master -> master

Key Commands

cd /usr/src/kodekloudrepos/media
git stash list
git stash apply stash@{1}
git status
git add .
git commit -m "Committing changes of stash@{1}."
git push origin master

What I Learned

git stash list is used to view saved stashes.

git stash apply stash@{1} restores a specific stash without deleting it.

After restoring a stash, the changes can be staged and committed normally.

git push origin master sends the committed changes to the remote repository.

Repository ownership and permissions can affect Git operations, especially when working with bare repositories.