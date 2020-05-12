# A Quick Reference to Git

### 1. Initialize a git repo [ git init ]

Inside the directory in which you want to initialize a repo-

```bash	
git init
```

### 2. Check Status [ git status ]

```bash
git status
```

Will show all untracked file status

There is another option called short git status

```bash
git status -s
```

or
```bash
git status --short
```
	
In the result-
?? means - Untracked files
A means - files added to staging area
M means - modified files

### 3. Adding File/Files to Staging Area [ git add ]

-Adding by file name

```bash
git add <filename1 filename2 ....  filenamen>
```

-Adding all files

```bash
git add .
```	
	
### 4. commit [ git commit ]

-Initial Commit

```bash
git add <filename ....>
git commit -m "commit message"
```
	
-Later commit
--option 1: (by filename)

```bash
git commit -m "commit message" <filename>
```
	
--option 2: (commit all files)

```bash
git commit -am "commit message"
```
	
If just use git commit the default editor configured will be opened and you can enter the commit message there.
To add commit message in editor commit you change in the following way-

```bash
git add <files>
git commit
```	
	
### 5. Check Difference [ git diff ]

```bash
#Difference between working directory and staging area
git diff
#Difference between stating area and last commit
git diff --staged
```
	
This command will display what have been changed in the repository after the last commit.



### 6. List All Commits [ git log ]

a. this command will list all the commits with commit hash, author and summary

```bash	
git log
```

-git log command supports the following parameters

|Option | Description|
----------|----------------
-p | Show the patch introduced with each commit.
--stat | Show statistics for files modified in each commit.
--shortstat | Display only the changed/insertions/deletions line from the --stat command.
--name-only | Show the list of files modified after the commit information.
--name-status | Show the list of files affected with added/modified/deleted information as well.
--abbrev-commit | Show only the first few characters of the SHA-1 checksum instead of all 40.
--relative-date | Display the date in a relative format (for example, “2 weeks ago”) instead of using the full date format.
--graph | Display an ASCII graph of the branch and merge history beside the log output.
--pretty | Show commits in an alternate format. Options include oneline, short, full, fuller, and format (where you specify your own format).
--oneline | Shorthand for --pretty=oneline --abbrev-commit used together.
	
	
b. To view the differences introduced in each commit, we can run git log with the parameter called patch. We can also pass the number of patch we want to view-

```bash
git log -p -2
```
	
c. Another usefull parameter with git log is the --stat  parameter. It displayes the commit logs with a summary of how many lines were changes, how many lines inserted and how many lines removed. 

```bash
git log --stat
```	
	
d. Another usefull parameter is --pretty. It can be used in two or more ways

```bash
git log --pretty=oneline
# this will list all the commits, one line for each commit
```

e. --pretty=format: 

```bash
git log --pretty=format:"%h - %an, %ar - %s"
```
	
supported paramter in format are-
	
|Option| Description of Output|
|---------|-----------------------------|
|%H| Commit hash|
%h | Abbreviated commit hash
%T | Tree hash
%t | Abbreviated tree hash
%P | Parent hashes
%p | Abbreviated parent hashes
%an | Author name
%ae | Author email
%ad | Author date (format respects the --date=option)
%ar | Author date, relative
%cn | Committer name
%ce | Committer email
%cd | Committer date
%cr | Committer date, relative
%s | Subject


f. --graph

```bash
git log --pretty=format:"%h - %an" --graph
# the graph parameter displayes a nice ASCII graph of flow
```	
	
g. Limiting commit log display
-we already have seen the -p -n paramter to limit the number of commit log to display. There are several more options. E.g. --since, --before etc. 

	#to view commit logs or last 2 weeks
	git log --since=2.weeks
	
	#this command accepts values like a specific data  "yyyy-mm-dd"
	
	or a relative data like "2 years 1 day 3 minutes ago"
	
	# can filter by the --author parameter
	
	# also can apply the --grep filter by passing a string that will be matched with commit message
	
	
-Avaliable options for git log

|Option | Description|
----------|-----------------
-< n > | Show only the last n commits
--since, --after | Limit the commits to those made after the specified date.
--until, --before | Limit the commits to those made before the specified date.
--author | Only show commits in which the author entry matches the specified string.
--committer | Only show commits in which the committer entry matches the specified string.
--grep | Only show commits with a commit message containing the string
-S | Only show commits adding or removing code matching the string


For example,  

	git log --pretty="%h - %s" --author='Junio C Hamano' --since="2008-10-01" \ --before="2008-11-01" --no-merges -- t/
	

	
### 7. View Details of a Commit [ git show ]

	#in commit list by git log command there is a long value called the commit hash.
	git show <hash value, at least 4 or 5 chars from the left side>
	

### 8. Move to a Specific Commit [git checkout]

	git checkout hash_value [at least 4- 5 chars of the commit hash]
	

### 9. Move to the HEAD or the latest commit [git checkout]

	git checkout master
	
	
### 10. View Commit logs of a specific file [git log]

	git log file_name
	
	
### 11. Move to a Commit of a specific file [git checkout]

	git checkout hash_value  file_name
	
	
### 12. Get back to HEAD after moving to a specific version of specific file [git checkout]

	git checkout master -f
	
	
	
### 13. Reset a commit [git reset]
After doing a commit mistakenly it can be reset and removed from the commit log. But once a commit is pushed, it should not be reseted. 
-There are two reset
1. soft reset - commit will be removed, but changes in files will still be there
2. hard reset - commit will be removed and changes in files will be removed also

	git reset --soft


	git reset --hard
	
	
### 14. Get back the commit after reset [git reflog, git reset]
After reset there will be no log in git log for that commit. So to get what have been done until then in that repository, run the bellow command

	git reflog
	
From the list of log, pick the reset point as   HEAD@{somenumber}

Then run the following command

	git reset HEAD@{somenumber}
	git reset --hard/soft
	
use hard or soft based on the type of reset you want to recover from.



### 15. Git Amend [ git commit --amend]
After doing one commit if you think that some other changes need to be commited in the same commit and you do not want to make another commit for that change, then yo can amend to the previous commit--

	git add file_name
	git commit --amend
	
	

### 16. Git stash and clear [git stash]
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



### 17. Git clean [git clean]
Sometimes we need to create some helper files that are not part of the project. After one commit we need to remove those untracked files. 
	
-git clean -f -->this command will remove all the untracked files. But this command is risky, because untrcaked files onece deleted can ot be undone

	git clean -f 
	
so we can run a dry run of the command and can check which files will be deleted...
git clean -f -n -->this command will show the list of files that would be deleted]

	git clean -f -n
	
if you are sure, then run the 

	git clean -f 

above command will now delete the untracked files.




### 18. Remote Repository [git push, git pull ]
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


-Renaming remote

	git remote rename <old_name> <new_name>
	
-Removing remote

	git remote remove <remote_name>
	



### 19. .gitignore file
Sometimes there are certains files that we want to exclude from commit or we do not want git to track those files. These type of file may include any zip file or binary file, technically any type of files.

To notify git to ignore certain files, we need to create a .gitignore file. And in the .gitignore file we need to list all the files and folders we want git to ignore and not to keep track.

For example, if there is a file named   hello.zip and we want to ignore that file, then add the following in the gitignore file

	hello,zip
	
This will ignore the hello.zip file.
We also can use widlcard. 

For example if we want to ignore all zip files, then we can add the following line in the gitignore file

	*.zip
	
	
### 20. Cloning a repository [git clone]
-A remote repository can be cloned using different protocol. 
-Copy the link of the repository

	#clone with the default repo name
	git clone <repository_link>
	#give the cloned repo a different name
	git clone <repository_link>  <new name>
	
	

### 21. Configure difftool [git difftool]
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


### 22. Configure mergetool [git mergetool]
If there is any merge conflict, then a visual tool will be very helpfull to resolve the conflict by comapring files.
We will be using "meld" as a mergetool. Run the following commands to configure "meld" as  a mergetool

	git config --global merge.tool meld
	git config --global mergetool.meld.path "/usr/bin/meld"
	git config --global mergetool.prompt false





### 23. Removing files [git rm]
If you want to remove files from git track, you need to use git rm command. If you remove the file using shells rm command, then git will show untracked changes. So you need to use git rm command.

	git rm <filename>
	
will remove the file from staging area as well as working directory in the next commit.


But sometimes we might want to remove the file from staging area, and want to keep it in working directory. Then run the following command-

	git rm --cached <filename>
	


### 24. Moving files [git mv]
Git does not keep track of moving files, i.e. git rm will be tracked as rename operation.

	git mv file_from   file_to
	


### 25. Unstaging file [ git reset ]
After adding file to the staging area, if you think that the file is not for this commit or you just simply want to unstage the file from staging area, then run

	git reset HEAD <filename>
	
git reset is a dangoreous command, but running git reset without --hard or --soft or any other paramter is not dangarous.



### 26. Unmodifying modified file
Unmodifying simply means, you pulled a fresh copy or after doing a commit you have changes/updated some content of a file and now want to get back to the previous cleaned version upto last commit. you can do such by check out command.

	git checkout -- <filename>
	
this command will get you back the clean file upto last commit.



### 27. Tagging your project [git tag]
Usually people tag their project upto a specific point as important, for examle, release version or some other points..

-Listing tags: you can list all the existing tags simply by git tag with (-l or --list) optional parameters. 

	git tag
	
-Filtering tags in list: you can filter or search for specific tags by adding wildcard or string by -l or --list parameter. For example, if you want to list all the tags with "1.5.8" then run-

	git tag -l "1.5.8*"
	
-Two types of tagss: a) annotated tags   b) lightweighted tags

-annotated tags: keeps every information.

##### 27.1. Creating tag:

	#annotated tag by -a parameter
	git tag -a <tag_name>  -m "tag commit message"


	#lightweigthed tag
	git tag <tag name>
	

To view a tag information:

	git show <tag name>
	
##### 27.2 Tagging later:
If you have passed through your current commit and want to tag a previous commit as an important version. you can do so by providing the commit hash

	git tag -a <tagname> <commit hash> -m "tag commit message"
	
	
##### 27.3 Sharing tags:
In normal push, tags are not shared to the remote repo. So, if you want to share the tags to remote, you need to push that tag explicitely as a branch to the remote..

	#to push a single tag
	git push <remote name> <tag name>
	
	e.g.
	git push origin v1.0
	
	
	#to push all the tags
	git push <remote name> --tags
	
	e.g.
	git push origin --tags
	
	
##### 27.4 Deleting tags:
To delete a tag, run
	
	git tag -d <tagname>
	
but the above command does not delete tag from remote repo. To delete tag from remote repo run

	git push <remote name> --delete <tagname>
	
	e.g.
	git push origin --delete v1.0
	


##### 27.5 Checking out a tag:
You can get the verion of files as was in a specific tag version by simply checking out like a commit-

	git checkout v1.0


But this one detach the HEAD so has some ill sides.

The better option to checking out to a tag is creating a separate branch-

	git checkout -b <branch name> <tag name to checkout>
	
	
	e.g. git checkout -b v1.1 v1.0
	
	# this will create and switch to the new branch v1.1
	
	
	
### 28. Git Aliases
We can shorten the git commands by creating git aliases in git config
For example

	git config --global alias.st status
	
Now if you run

	git st
	
This will be equivalent to 

	git status
	
	
You can create alias for long commands to reduce typing -

For example,

	git config --global alias.unstage "reset HEAD --"
	
Now the bellow two commands will be equivalent-

	#orignal long command
	git reset HEAD -- file1.txt
	
	#shortened using alias
	git unstage file1.txt



### 29. Git Branch
we can work on different ideas or features in different branches and it will not affect our master branch. There are several workflows people follows to maintain branches.

#### 29.1 Creating branch































































































