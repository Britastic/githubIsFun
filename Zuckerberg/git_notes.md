# Git Notes

## Setup

Make sure git is installed.  Configure it, following the instructions [here](http://swcarpentry.github.io/git-novice/02-setup/)

Download the project zip file from `http://cs.wisc.edu/~ckoch/inflammation_project.zip`.  
Move it to your Desktop and unzip.  

Open a terminal window.  On Mac/Linux, this will be the "Terminal", on Windows, 
it should be "GitBash."  

Navigate to the project folder, by running: 

~~~
$ cd
$ cd Desktop
~~~

## Track changes locally

Create the repository by running: 

	git init

To see what files git wants to track, run: 

	git status

To add files (so git will track them in the future), run: 

	git add -A

See what's changed: 

	git status

Finally, commit your changes, with a commit message, and view repository status: 

	git commit -m "initial commit of all files"
	git status

Make a change to the file.  In this case, we're going to add a command-line argument 
to `readings.py` (use `2.7-readings.py` if you have version 2.7 of Python): 

~~~
import numpy
import loaddata
import sys

def main():
		filename = sys.argv[1]
        data = loaddata.load(filename)
        print(filename)
        print(data.mean(axis=1))

main()
~~~

What has happened?  

	git status

To commit our changes, do the following: 

	git add readings.py
	git commit -m "adding filename command line argument"
	
Check our status again: 

	git status

You try: make a change to the script (add a comment, make a loop, find the min and max of the data), 
then commit your changes using git.  

### Extras

* How often to commit?  Your choice, depending on your workflow.  One common saying is "commit early, commit often."  
* To ignore certain files, create a .gitignore file
* To see past commits + messages, use `git log` or `git log --oneline`
* To see a previous version of the file, look up its commit hash, and use the syntax: 
	~~~
	git checkout commit_hash file_name
	~~~
* If you ever see the "detached HEAD" error message, running: 
	~~~
	git checkout master
	~~~
	should save you.

## Remote Repositories

Create github repo
Add remote
push
git clone
change (add README)
push
move over
git push

## Collaborating

Fork / clone / make change / PR