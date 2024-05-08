#### How to create a branch
```
git branch (branch_name)
```
#### How to delete a branch. Before deleting a branch, make sure you are not on the branch you want to delete. You can switch to a different branch using the git checkout command.
```
git branch -d (branch_name)
```
#### To create a new branch and switch to it
```
git checkout -b new_branch_name
```
### How to clone code from a specific branch from remote repo
 ```
  git clone -b dev git@git.inneedcloud.com.bd:InNeed/Quantlio_Stratus.git
  or
  git clone -b dev https://git.inneedcloud.com.bd/InNeed/Quantlio_Stratus.git

 ```
