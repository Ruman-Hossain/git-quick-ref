# A Quick Reference to Git

### 1. Initialize a git repo

Inside the directory in which you want to initialize a repo-

	
	git init


### 2. Check Status
	git status
	
Will show all untracked file status

There is another option called short git status

	git status -s
	or
	git status --short
	
In the result-
?? means - Untracked files
A means - files added to staging area
M means - modified files

### 3. Adding File/Files to Staging Area

-Adding by file name

	git add <filename1 filename2 ....  filenamen>

-Adding all files

	git add *
	
	
### 4. Commiting Change

-Initial Commit

	git add <filename ....>
	git commit -m "commit message"
	
-Later commit
--option 1: (by filename)

	git commit -m "commit message" <filename>
	
--option 2: (commit all files)

	git commit -am "commit message"
	

	
### 5. Check Difference

	#Difference between working directory and staging area
	git diff
	#Difference between stating area and last commit
	git diff --staged
	
This command will display what have been changed in the repository after the last commit.



### 6. List All Commits

	#this command will list all the commits with commit hash, author and summary
	git log
	
	
### 7. View Details of a Commit

	#in commit list by git log command there is a long value called the commit hash.
	git show <hash value, at least 4 or 5 chars from the left side>
	

### 8. Move to a Specific Commit

	git checkout hash_value [at least 4- 5 chars of the commit hash]
	

### 9. Move to the HEAD or the latest commit

	git checkout master
	
	
### 10. View Commit logs of a specific file

	git log file_name
	
	
### 11. Move to a Commit of a specific file

	git checkout hash_value  file_name
	
	
### 12. Get back to HEAD after moving to a specific version of specific file

	git checkout master -f
	
	
	
### 13. Reset a commit
After doing a commit mistakenly it can be reset and removed from the commit log. But once a commit is pushed, it should not be reseted. 
-There are two reset
1. soft reset - commit will be removed, but changes in files will still be there
2. hard reset - commit will be removed and changes in files will be removed also

	git reset --soft


	git reset --hard
	
	
### 14. Get back the commit after reset
After reset there will be no log in git log for that commit. So to get what have been done until then in that repository, run the bellow command

	git reflog
	
From the list of log, pick the reset point as   HEAD@{somenumber}

Then run the following command

	git reset HEAD@{somenumber}
	git reset --hard/soft
	
use hard or soft based on the type of reset you want to recover from.



### 15. Git Amend
After doing one commit if you think that some other changes need to be commited in the same commit and you do not want to make another commit for that change, then yo can amend to the previous commit--

	git add file_name
	git commit --amend
	
	

### 16. Git stash and clear
If you want to create mutliple version of your experimental work but do not want to commit the experimental code, you can add the temporary version to the git stash area.

-make initial commit with the template file or the starting code
-make some change to do an experiment
-git stash -this command will save this verion in stash and make the code clean to the initial version so that you can do further experiment

	git stash
	
-make another change or update in the same experiment and run git stash to save this version temporarily
-to get the latest stashed version from the stash

	git stash pop/apply

-after making multiple stash, to see the stash list

	git stash list

-To get back to a specifi stash version, see the stash id in git stash list

	git stash pop stash@{somenumber id}

-If you are satisfied with certain version of your experiment, make a commit. to clean the stash area
git stash clear



### 17. Git clean
Sometimes we need to create some helper files that are not part of the project. After one commit we need to remove those untracked files. 
	
-git clean -f -->this command will remove all the untracked files. But this command is risky, because untrcaked files onece deleted can ot be undone

	git clean -f 
	
so we can run a dry run of the command and can check which files will be deleted...
git clean -f -n -->this command will show the list of files that would be deleted]

	git clean -f -n
	
if you are sure, then run the 

	git clean -f 

above command will now delete the untracked files.




### 18. Remote Repository
There are many remote repository services like github, bitbucket, getmeat.io, gitlab etc. you can also host your own remote repository in your intranet or internet server.

-create a repo, copy the link
-If you want to start from the new repo, then

	git clone <remote repo link>

-If you already have a local repo, then 

	git remote add <a name, normally origin is given> <remote repo link>

-To view the remote of any repo

	git remote show

-To view the details of any repo remote info
	
	git remote show <remote name, mostly origin>

-Now, after commit, you can push your commits to the remote repo

	git push <remote name, mostly origin> <branch name, master or some other branch name>

-Before you start working, you can get the latest update from other user, devs to you local repo by

	git pull <remote name, mostly origin> <branch name, master or some other branch>




### 19. .gitignore file
Sometimes there are certains files that we want to exclude from commit or we do not want git to track those files. These type of file may include any zip file or binary file, technically any type of files.

To notify git to ignore certain files, we need to create a .gitignore file. And in the .gitignore file we need to list all the files and folders we want git to ignore and not to keep track.

For example, if there is a file named   hello.zip and we want to ignore that file, then add the following in the gitignore file

	hello,zip
	
This will ignore the hello.zip file.
We also can use widlcard. 

For example if we want to ignore all zip files, then we can add the following line in the gitignore file

	*.zip
	
	
### 20. Cloning a repository
-A remote repository can be cloned using different protocol. 
-Copy the link of the repository

	#clone with the default repo name
	git clone <repository_link>
	#give the cloned repo a different name
	git clone <repository_link>  <new name>
	
	

### 21. Configure difftool
So far we have checked the difference in between files using git diff command. But the difference was displayed in stdout in terminal. We can use a visual tool for comparing files. There are several tools available. 

You can use the following command to check the available tools

	git difftool --tool-help
	
We will use "meld" as a visual difftool
To install meld in ubuntu-

	sudo apt-get update
	sudo apt-get install meld

First get the path of "meld" using the following command-

	which meld
	
Now to configure "meld" as the difftool, run the following commands for configuration-

	git config --global diff.tool meld
	git config --global difftool.meld.path "/usr/bin/meld"
	git config --global difftool.prompt false

Now we can see the difference by running the command

	git difftool
	
But git diff will perform as usual even though difftool is configured.


### 22. Configure mergetool
If there is any merge conflict, then a visual tool will be very helpfull to resolve the conflict by comapring files.
We will be using "meld" as a mergetool. Run the following commands to configure "meld" as  a mergetool

	git config --global merge.tool meld
	git config --global mergetool.meld.path "/usr/bin/meld"
	git config --global mergetool.prompt false





### 23. 




































