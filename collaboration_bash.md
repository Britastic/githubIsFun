Collaboration (Bash version)
---------------------------

1. Create a fork of the desired central repository on GitHub (easy as clicking 
the fork button in the top right corner of the webpage).  GitHub will create a copy of 
the repository in your namespace.  This is your fork, where you will "push" your changes and submit pull
requests to the central repository.  

2.  Open your terminal window of choice (for Macs/Linux systems, "Terminal" is 
a basic option; for Windows, you can use GitBash, which was installed with git).  
In the terminal, use the `cd` command to place yourself into the directory where you'd like to copy
the files locally.  Once there, the git clone command will make this local directory for you: 
	~~~
	$git clone <url-of-your-fork>
	~~~

3.  Now you should have a folder (wherever you saved the clone) on your computer 
that contains all the files from your fork on GitHub.  Again in the terminal, `cd` into this local copy.  
Now make your changes; fiddle around with the code; do what you like.  
Once you've made a series of changes you want to "save", use the 
following commands in the terminal:
	~~~
	$git status
	~~~
will show you which files you changed.  
	~~~
	$git add <files changed>
	~~~
"stages" the files, basically creating a list of all the files that you want 
to include when you "commit."  You can use the flag `-A` instead of the filenames to add all changed files.  
Then commit. This command will actually "save" a version of your changes that can then be shared online.   
	~~~
	$git commit -m "put your commit message describing changes here"
	~~~

4.  Once you have made and committed all the changes you want to submit to the master repository, 
type in:
	~~~
	$git push origin master
	~~~ 
This sends your commits (which describe your changes) to your copy of the online repository - the fork created in step 1.  
	
5.  Switch to your internet browser and pull up your fork of the repository.  Submit a pull request from your fork to the original online repository (look for a green button 
somewhere on the repository page).  Add any desired comments and finally click the green "Submit pull request" button.  

6. To update your local copy of the repository from the central repository will require two steps.  First, you must 
add the central repository as a remote to your project, essentially linking your local copy with the central master copy online.  
To do so, type in the terminal: 
	~~~
	$git remote add <name-for-remote> <url-for-master-repo>
	~~~ 
	
The `name-for-remote` could be anything - something simple like "upstream" or "central" is a good choice.  Don't use `master` since that's already a name with a meaning in git.  

To get changes from the central repository, now use the git pull command. 
	~~~
	$git pull <name-for-remote> master
	~~~ 

If you have a merge conflict (hopefully not!), edit the documents listed as being in conflict, then 
add and commit them as in 3.  

###Note on workflow

It is helpful to pull from the central repository 
on a regular basis in order to keep up with 
changes.  
