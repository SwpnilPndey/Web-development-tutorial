# How to push code from local repo to remote repo

1) Create a project folder 
2) Make project files using VS code
3) Initialise git using git init 
4) Add changes in project to staging area using git add .
5) Commit those changes : git commit -m "Message"
6) Configture username and email using git config user.name "Swapnil Pandey" and git config user.email "swpnil.pndey@gmail.com"
7) Create a remote repo in github 
8) Create SSH key in local computer :- 
  - : Write following on terminal : ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
  - Press enter twice
  - A message will be displayed giving the location where the SSH key has been generated : <some address>/.ssh/
  - Use cat ~/.ssh/id_rsa.pub to display the SSH key on terminal
  - Goto Github > Developer settings > Generate SSH and GPG keys > Create new Key >paste the SSH key from terminal and save it 
8) Add remote using SSH URL : git remote add origin <SSH URL of github repo>
9) Push the changes to remote repo using : git push origin <name of the branch> {# this is now globally master, unless specified}

The code has been pushed. 

If we make some changes in remote repo, we can sync our local repo using : git pull origin master




# How to do open source contribution using PRs

1) Go to the the upstream repo and fork it
2) Use SSH (or HTTPs) to clone the project from your repo 
  - Make a project folder in local computer 
  - Open terminal (or git bash) here and use : git clone <SSH of forked copy of repo>
  - No need to use git init as the git clone command is already doing it for us 
3) Now we can check git commits using : git status and git log
4) Now I will create a new branch for the changes : git checkout -b <name of test branch>
5) Make changes in files as per need 
6) Then commit these changes using git add . and git commit -m "<Message>"
7) Then push the changes to new remote using : git push origin <name of test branch>. As there will not be any such branch on remote, git will create it by itself 
8) As soon as we do it, we can go to github, and we will see an option saying : Compare and Pull Request
9) We can keep pushing our code to github test branch till we feel our feature is addedd or the bug is removed 
10) But, before raising a PR request, it is important that our code base is up to date with the upstream master branch 
11) For this, we add new remote URL for the upstream : git remote add upstream <SSH or HTTP of upstream repo>
12) Now we fetch the changes in upstream as : git fetch upstream
13) Then we shift to master branch using : git checkout master
14) Now we will merge the changes in upstream master to origin master using : git merge upstream/ master (this master is master of upstream)
15) We will update the changes to remote master in our remote repo using : git push origin master
15) Then we will merge the changes in local master to local test using : git checkout test and then git merge master
16) Now, we can check for conflicts if any and then add our code (the bug removal or feature addition) to this test branch 
17) Then we push it to remote test branch  
18) After that we can use : Compare and Pull Request. It will open a window where we can provide description of the PR and where are we raising the PR to (upstream branch) and from where are we raising PR (test branch of forked copy)
19) After that the owner can accept the PR and merge the code into master codebase
20) If there are some recommendations, we can change our test branch code and push to remote again. The PR request is updated automatically
21) Finally after PR is accepted, update your master branch (both local and remote) using : git fetch, git merge and git push 
22) After few days, the test branch can be deleted both local repo and the remote repo 

This is the whole process of Pull Request
