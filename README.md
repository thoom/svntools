SVN Tools
=========

Scripts to help manage an SVN repository.

Scripts
-------

### svndiff

A script that will compare two branches or the trunk and branch and give list of files modified or missing from the compared SVN repo.

#### To use

Edit the base variable in the file to point to your SVN repository. Future versions may support importing a JSON configuration file instead of editing the file directly.

	svndiff help
	------------
	
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
