[[Keep/Colour/ORANGE]] [[Keep/Archived]] 

FROM LOCAL REPO TO REMOTE REPO

git init

echo Hello, World! > j.txt

git add .

git commit -m "jh"

git remote add origin https://github.com/aravindhnirmal/j.git
(opt) git remote -v   displays the names and URLs of the remote repositories

git push -u origin master



for show all files
Get-ChildItem -Force


git reset commit id -delete the commits that given commitid after(like stack)

git status
git log


git stash save in other folder that commits also disappears 

 notepad somefile.txt

1.git init
2.  echo hi > j.py
3. PS C:\Users\NIRMAL\Documents\New folder> git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        j.py

nothing added to commit but untracked files present (use "git add" to track
4 .  git remote add origin https://github.com/aravindhnirmal/gitpractice.git
error: remote origin already exists.

5 . git status
On branch main

6. git remote add main https://github.com/aravindhnirmal/gitpractice.git
7. git remote add main https://github.com/aravindhnirmal/gitpractice.git
8. git push

Get-ChildItem -Force for ls -a  OR Get-ChildItem



clone 



 git clone https://github.com/aravindhnirmal/gitpractice.git

ls

cd


notepad j.py
git add.
git log
 git commit -m "second  committied from clonw"
 git push




pull
 git pull


git pull https://github.com/aravindhnirmal/gitpractice.git main




for local to remote push
📌📌📌📌


Certainly! Here's a step-by-step guide to resolving the issue and pushing your local branch `newfeatures2` to the remote repository:

1. Fetch the latest changes from the remote repository:
   ```
   git fetch origin
   ```

2. Switch to your `newfeatures2` branch:
   ```
   git checkout newfeatures2
   ```

3. Merge the remote changes into your local branch:
   ```
   git merge origin/newfeatures2
   ```

4. Resolve any conflicts that may arise during the merge. Open the conflicting files, resolve the conflicts, and save the changes.

5. Commit the merge changes:
   ```
   git commit -m "Merge remote changes into newfeatures2"
   ```

6. Push your local branch to the remote repository:
   ```
   git push origin newfeatures2
   ```

Make sure to carefully follow each step in the given order. If you encounter any conflicts during the merge, resolve them before committing and pushing the changes.


if the github have the readme first u pull next push 

"fatal: refusing to merge unrelated histories" typically occurs when you are trying to merge two branches that have diverged and do not share a common commit history.
git pull origin master --allow-unrelated-histories
git remote add origin link 
git push



