# A Quick Reference to Git

### 1. Initialize a git repo

Inside the directory in which you want to initialize a repo-

	
	git init


### 2. Check Status
	git status
	
Will show all untracked file status


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
	
	

