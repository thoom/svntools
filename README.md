SVN Tools
=========

Scripts to help manage an SVN repository. 
Each script is stored in an appropriate folder based off of the language the script was written in. The Ruby scripts are more full featured, since I prefer writing in Ruby.

Ruby Scripts
------------

All of the ruby scripts utilize a `.svntools.yml` file. If this file exists in the folder you call the script from, it will use that file (so you could keep a `.svntools.yml` file in each of your working directories); otherwise it will look for the file in your user's home directory. 

In the file, create a default section with a base key pointing to the root of your SVN repository (the directory your trunk resides in). You can also set up additional repositories by creating additional sections.

### .svntools.yml
   
    colorizer: colordiff
    repositories:
      default:
        base: http://my-svn-repository
        trunk: trunk (default, so unnecessary)
        branch: branch (default, so unnecessary)
      another-repo:
        base: http://another-svn-repository
        trunk: trunk/my-app2
        branch: branches/my-app2

### svntools

This script is a container script for the others. If you'd rather use it than the individual scripts below, feel free.

To use:

	command				description
	-------				-----------
	help {command}		Brings up help documentation for the specific command
	diff				Provides diff between revisions, branches, trunk, etc
	switch				Switch the svn repository for the current working copy
	merge				Merge the repository on to the working copy
	
	param             		description
	-----             		-----------
	-p (--repository) XXXX	Use the repository defined in the config file.
	--debug					Prints various debug statements
	
	examples
	--------
	svntools diff		Same as svndiff
	svntools help diff	Displays the svndiff help
 

### svndiff

Displays diffs between trunk, branches, and revisions. Can color code diff details. Organizes diff summaries.

To color code the diffs, I recommend something like [diffc](https://code.google.com/p/diffc) or [colordiff](http://www.colordiff.org).

To use:
   
	param					description
	-----					-----------
	-c (--colorizer) XXXX	A diff coloring app like diffc, colordiff. If one of these exist, it will choose automatically. If specified, it will use the specified app.
	-d (--folder) XXXX		A folder that should be compared (i.e. web/). Never sets --details flag.
	-f (--file) XXXX		A file that should be compared (i.e. web/index.php). Sets --details flag automatically.
	-o (--old) XXXX			The old branch that should be compared against. (i.e. --old sprint8). If missing, assumes trunk.
	-n (--new) XXXX			The new branch that should be compared against. (i.e. --new sprint8-stage). If missing, assumes trunk.
	-p (--repository) XXXX	Use the repository defined in the config file.
	-r (--revision) XXXX	Compare the differences between revisions rather than branches (i.e. -r 10301 or -r 10200:10301). Sets the --details flag automatically.
	-s (--sub) XXXX			A file (or folder) that should be compared (i.e. web/).
							If the param has a trailing forward slash, it is assumed that it is a folder. Otherwise it sets --details flag automatically.
	
	--debug					Prints various debug statements
	--details				Get the diff details instead of summary of all the changes.
	--summary				Force summary mode.
	
	examples
	--------
	To get a summary of changes between branches:
	svndiff -o sprint9 -n sprint10
	svndiff --old sprint9 --new sprint10
	
	To get detailed changes for all files between branches:
	svndiff -o sprint9 -n sprint10 --details
	svndiff --old sprint9 --new sprint10 --details
	
	To get a summary of changes between the trunk and a branch:
	svndiff --new sprint9
	svndiff --old trunk --new sprint9
	
	To get detailed changes for a file between branches:
	svndiff --old sprint9 --new sprint10 --file lib/class/MyClass.php
	svndiff --old sprint9 --new sprint10 --sub lib/class/MyClass.php
	
	To get a summary of changes between a sub folder between branches:
	svndiff --old sprint9 --new sprint10 --folder lib/class
	svndiff --old sprint9 --new sprint10 --folder lib/class/
	svndiff --old sprint9 --new sprint10 --sub lib/class/
	
	To get a detailed view of changes between a sub folder between branches:
	svndiff --old sprint9 --new sprint10 --folder lib/class --details
	svndiff --old sprint9 --new sprint10 --folder lib/class/ --details
	svndiff --old sprint9 --new sprint10 --sub lib/class/ --details
	svndiff --old sprint9 --new sprint10 --sub lib/class (notice the lack of trailing forward slash)
	
	To get a detailed view of changes between sequential revisions:
	svndiff -r 10301 (same as svndiff -r 10300:10301)
	svndiff --revision 10301
	
	To get a summary of changes between revisions:
	svndiff -r 10210:10301
	svndiff --revision 10210:10301
	
	To get a detailed view of changes between revisions:
	svndiff --revision 10301 --details

### svnmerge

Merge a working copy with another repository

To use:

	param					description
	-----					-----------
	-p (--repository) XXXX	Use the repository defined in the config file.
	--debug					Prints various debug statements

	
	examples
	--------
	svnmerge trunk      Merges trunk on to this working copy
	svnmerge sprint17   Merges sprint17 on to this working copy

### svnswitch

Switches the current SVN repository to another branch.

To use:

	param					description
	-----					-----------
	-p (--repository) XXXX	Use the repository defined in the config file.
	--debug					Prints various debug statements
	
	examples
	--------
	svnswitch trunk      Switches the working copy to the trunk
	svnswitch sprint17   Switches the working copy to sprint17


Python Scripts
--------------

### svndiff

A script that will compare two branches or the trunk and branch and give list of files modified or missing from the compared SVN repo. Edit the `base` variable in the file to point to your SVN repository.

To view the parameters available, type: `svndiff` without any parameters.

	param			description
	-----			-----------
	--old XXXX		The old branch that should be compared against. (i.e. --old sprint8). If missing, assumes trunk.
	--new XXXX		The new branch that should be compared against. (i.e. --new sprint8-stage). If missing, assumes trunk.
	--file XXXX		A file that should be compared (i.e. web/index.php). Sets --details flag automatically.
	--folder XXXX	A folder that should be compared (i.e. web/). Never sets --details flag.
	--sub XXXX		A file (or folder) that should be compared (i.e. web/). 
					If the param has a trailing forward slash, it is assumed that it is a folder. Otherwise it sets --details flag automatically.
	--details		Get the diff details instead of summary of all the changes.
	--summary		Force summary mode.
	
	examples
	--------
	To get a summary of changes between branches:
	svndiff --old sprint9 --new sprint10
	
	To get detailed changes for all files between branches:
	svndiff --old sprint9 --new sprint10 --details
	
	To get a summary of changes between the trunk and a branch:
	svndiff --new sprint9
	svndiff --old trunk --new sprint9
	
	To get detailed changes for a file between branches:
	svndiff --old sprint9 --new sprint10 --file lib/class/MyClass.php
	svndiff --old sprint9 --new sprint10 --sub lib/class/MyClass.php
	
	To get a summary of changes between a sub folder between branches:
	svndiff --old sprint9 --new sprint10 --folder lib/class
	svndiff --old sprint9 --new sprint10 --folder lib/class/
	svndiff --old sprint9 --new sprint10 --sub lib/class/
	
	To get a detailed view of changes between a sub folder between branches:
	svndiff --old sprint9 --new sprint10 --folder lib/class --details
	svndiff --old sprint9 --new sprint10 --folder lib/class/ --details
	svndiff --old sprint9 --new sprint10 --sub lib/class/ --details
	svndiff --old sprint9 --new sprint10 --sub lib/class (notice the lack of trailing forward slash)
