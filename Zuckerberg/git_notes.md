# Git Notes

## Setup

Make sure git is installed.  Configure it, following 
the instructions [here](http://swcarpentry.github.io/git-novice/02-setup/)

Download the project zip file from `http://cs.wisc.edu/~ckoch/inflammation_project.zip`.  
Move it to your Desktop and unzip.  

Open a terminal window.  On Mac/Linux, this will be the "Terminal", on Windows, 
it should be "GitBash."  

Navigate to the project folder, by running: 

~~~
cd
cd Desktop
~~~

## Track changes locally

Create the repository by running: 

	git init

To see what files git wants to track, run: 

	git status

To add files (so git will track them in the future), run: 

	git add -A

> Think about privacy!  Once you've added a file, there will be some record that 
it existed forever (even if you later delete it)!  

See what's changed: 

	git status

Finally, commit your changes, with a commit message, and view repository status: 

	git commit -m "initial commit of all files"
	git status

Make a change to the file.  In this case, we're going to add a command-line argument 
to `readings.py` (use `2.7-readings.py` if you have version 2.7 of Python): 

```python
import numpy
import loaddata
import sys

def main():
		filename = sys.argv[1]
        data = loaddata.load(filename)
        print(filename)
        print(data.mean(axis=1))

main()
```

What has happened?  

	git status

To commit our changes, do the following: 

	git add readings.py
	git commit -m "adding filename command line argument"
	
Check our status again: 

	git status

Exercise: make a change to the script (add a comment, make a loop, find the min and max of the data), 
then commit your changes using git.  

Once you have a bunch of commits, you might want to see your history.  To do this, use: 

	git log

or

	git log --oneline`
	
To ignore certain files, create a `.gitignore` file.  Ours will look like this: 

~~~
__pydata__/
~~~

Save and commit this.  What happens in `git status`?  


### Bits and Bobs

* There are `git` versions of the shell commands `mv`, `cp` and `rm`.  Using `git` before 
any of these commands will make the appropriate change + then stage the file, ready for committing.  
* How often to commit?  Your choice, depending on your workflow.  One common saying is "commit early, commit often."  
* The most recent commit is called the `HEAD` commit
* To see a previous version of the file, look up its commit hash, and use the syntax: 
	`git checkout commit_hash file_name`
  To go back to the latest version, use `git checkout HEAD file_name`.  
* If you ever see the "detached HEAD" error message, running: 
	`git checkout master`
	should save you.
* If the command line is not your thing, there are lots of programs out there that 
can be an interface to git.  See [this page](http://happygitwithr.com/git-client.html).  
Also, [RStudio has git integration](http://happygitwithr.com/rstudio-see-git.html).

## Remote Repositories

Now, let's create a copy of our repository on the cloud.  We'll use 
GitHub here, but really any remote service (bitbucket, a private server) will do - 
the same principles apply.  

Make sure you're logged into GitHub.  Look for the + symbol, and use it to 
create a new empty repository.  

Back in your terminal, we need to a) connect the remote repository (in Github) to 
our local one and then b) sync our local copy with the remote one.  We do this 
by the following two commands: 

	git remote add origin http://github.com/yourusername/yourrepositoryname
	git push origin master

That's it!  You have a remote copy.  You can always push changes from your computer to 
this remote copy by using the `git push` command.  

If you want to make another copy of this same repository, on a different computer, 
you can use the "git clone" command.  

	cd ~/Downloads
	git clone http://github.com/yourusername/yourrepositoryname

If you `cd` into this new repository, you should find an exact copy of your online copy.  

Let's make a change in this copy of the respository, and push our changes to github: 

	touch README.md
	git add README.md
	git commit -m "adding README file"
	git push origin master

Switching over to our old local copy, we can pull the changes from GitHub: 

	cd ~/Desktop/inflammation_project
	git pull origin master

Exercise: edit the `README` in the current copy, then commit + push your changes.  Hop over 
to the other copy (in your `Downloads` folder).  Edit *that* copy of the `README`.  Try 
committing + pushing changes.  What happens?  

In the case that you get a "merge conflict" git will tell you if two files have 
competing changes.  Open the file, fix it manually, then do `git add` and `git commit` as usual.  

### Bits and Bobs

* As long as you have an authoritative copy of the repo somewhere, it is perfectly legitimate to: 
	* wipe out a local repo + start over with a `git clone`
	* "force" push to your remote copy (using `git push -f`)
* The git error messages may seem terrifying at first.  They're actually fairly informative.  
* Fun fact!  `git clone` is actually combining several shell + git commands.  Can you guess what they might be?
* Answer: `git clone repository_name` equals: 

~~~
mkdir repository_name
cd repository_name
git init
git remote add origin repository_name
git pull origin master
~~~

## Collaborating

Create a fork of the desired central repository (in this case, 
[http://github.com/ChristinaLK/githubIsFun](http://github.com/ChristinaLK/githubIsFun)
by clicking 
the fork button in the top right corner of the webpage.  GitHub will create a copy of 
the repository in your namespace.  This is *your* copy of the repository, where 
you will "push" your changes and submit pull
requests to the central repository.  

Create a copy of this repository: 

	cd ~/Desktop
	git clone <url-of-your-fork>
	
Move into the repository and look around: 

	cd GithubIsFun

Exercise: create a file in the `participants` folder, where the title of the file is your 
github username. 

	touch username.txt

Commit your changes, and push them to your fork.  

Switch to your internet browser and pull up your fork of the repository.  Submit 
a pull request from your fork to the original online repository (look for a green button 
somewhere on the repository page).  Add any desired comments and finally 
click the green "Submit pull request" button.  

You try: add a line of text to your username file.  Commit changes and push to your 
fork.  What happens to the pull request?  

To update your local copy of the repository from the central repository 
will require two steps.  First, you must 
add the central repository as a remote to your project, essentially 
linking your local copy with the central master copy online.  
To do so, type in the terminal: 

	git remote add <name-for-remote> <url-for-master-repo>
	
The `name-for-remote` could be anything - something simple like "upstream" or "central" 
is a good choice.  Don't use `master` since that's already a name with a meaning in git.  

To get changes from the central repository, now use the git pull command. 

	git pull <name-for-remote> master

### Bits and Bobs

* It is helpful to pull from the central repository 
on a regular basis in order to keep up with 
changes.  
* If you're going to submit lots of pull requests, it's a good idea to use branches.  
See the main readme for a good branching tutorial.  