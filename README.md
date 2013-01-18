SVN Tools
=========

Scripts to help manage an SVN repository. 
Each script is stored in an appropriate folder based off of the language the script was written in. In general, the Ruby scripts are more full featured, since I prefer writing in Ruby.

Scripts
-------

### svndiff

A script that will compare two branches or the trunk and branch and give list of files modified or missing from the compared SVN repo.

To view the parameters available, type: `svndiff` without any parameters.

#### Python

Edit the base variable in the file to point to your SVN repository.

	param			description
	-----			-----------
	--old XXXX		The old branch that should be compared against. (i.e. --old sprint8). If missing, assumes trunk.
	--new XXXX		The new branch that should be compared against. (i.e. --new sprint8-stage). If missing, assumes trunk.
	--file XXXX		A file that should be compared (i.e. web/index.php). Sets --details flag automatically.
	--folder XXXX		A folder that should be compared (i.e. web/). Never sets --details flag.
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

#### Ruby

Create a `.svndiff.yml` file in your user's home directory. Create a default section with a base key pointing to the root of your SVN repository (the directory your trunk resides in). You can also set up additional repositories by creating additional sections.

##### YAML:
   
    default:
      base: http://my-svn-repository
    another-repo:
      base: http://another-svn-repository
      
##### To use:
   
	param			description
	-----			-----------
	-c (--colorizer) XXXX	A diff coloring app like diffc, colordiff. If one of these exist, it will choose automatically. If specified, it will use the specified app.
	-d (--folder) XXXX	A folder that should be compared (i.e. web/). Never sets --details flag.
	-f (--file) XXXX	A file that should be compared (i.e. web/index.php). Sets --details flag automatically.
	-o (--old) XXXX		The old branch that should be compared against. (i.e. --old sprint8). If missing, assumes trunk.
	-n (--new) XXXX		The new branch that should be compared against. (i.e. --new sprint8-stage). If missing, assumes trunk.
	-p (--repository) XXXX  Use the repository defined in the config file.
	-r (--revision) XXXX	Compare the differences between revisions rather than branches (i.e. -r 10301 or -r 10200:10301). Sets the --details flag automatically.
	-s (--sub) XXXX		A file (or folder) that should be compared (i.e. web/).
				If the param has a trailing forward slash, it is assumed that it is a folder. Otherwise it sets --details flag automatically.
	--details		Get the diff details instead of summary of all the changes.
	--summary		Force summary mode.
	
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
	
	To get a detailed view of changes between revisions:
	svndiff -r 10210:10301
	svndiff --revision 10210:10301
	
	To get a summary of difference between revisions:
	svndiff --revision 10301 --summary
