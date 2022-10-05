# My git bash cheat sheet

 

## commands
|command name | description |
|--|--|
| git branch -a | show all branches inside repository ( remote and non remote)|
| git branch -r | show all branches inside repository ( remote only)|
| git branch -r | show all branches inside repository ( local only)|
| git switch that-other-local-branch| switch to another local branch|
|git switch -c non-existing-branch | create a branch from current Branch|
| git branch -d localBranchName | delete a branch|

## procedures 

### When you need to add something that you forgot inside .gitignore 
**pre-requisite:** I hope that you updated something inside your gitignore. 

1. commit any outstanding code changes
2. run the following to remove changed files in the index 
   ``` 
   git rm -r --cached .
3. run the following command to stage everything back </br>
   **Note:** The command will stage things excluding new files added inside the *.gitignore*  
   ``` 
   git add .
4. run the  folloming to commit
   ```
   git commit -m "your msg"

## Bibliography 
||_link_|
|--|--|
| Listing of branches commands |http://gitready.com/intermediate/2009/02/13/list-remote-branches.html|
| Switching branches|https://devconnected.com/how-to-switch-branch-on-git/|
| delete a branch | [The link is long .. just click here](https://www.freecodecamp.org/news/how-to-delete-a-git-branch-both-locally-and-remotely/#:~:text=Deleting%20a%20branch%20LOCALLY&text=Delete%20a%20branch%20with%20git%20branch%20%2Dd%20.&text=The%20%2Dd%20option%20will%20delete,branch%20is%20now%20deleted%20locally.)|
| adding already tracked to .gitignore | https://stackoverflow.com/questions/1139762/ignore-files-that-have-already-been-committed-to-a-git-repository|
