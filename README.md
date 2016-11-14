# GHDLproject


GitHubDL


Purpose:

The purpose of the project is a system that can communicate with the github API, search through its repositories and download and update a large number  of repositories that match the search result.

The system is called and recives its arguments through commandline. It has 2 major operations:

*-s | --search : Searches through github repositores based on provided search terms and returns with data 
on each of the matching results, along with a short summary at the end.

Providing –short at the end of the call only returns the short summary as a result of the search.

Takes –key, --datecr, --dateupd, --size, --lang, --short


*-d | --download: Similar to Search but rather than returning data for each matching result it does a git clone (or git pull for already downloaded repositories) on each matching result to the provided filepath.

Takes –key, --datecr, --dateupd, --size, --lang, --dldir


The project is written in Python 3 and primarily intended to be used on a Linux system.


Usage:

GitHubDL.py [-d | -s][--key <keyword>][--datecr <date>][--dateupd <date>][--size <int>][--lang <keyword>][--short][--dldir]


Options:

-s | --search:		

-d | --download:	Note: Requires that you specify a –dldir.

--key:			Takes a string to use as a keyword for the repository search

--datecr:		Takes a date string to filter the search results by only showing repositories 			created after the given date.

--dateupd:		Takes a date string to filter the search results by only showing repositories 			that were last updated after the given date.

--size:			Takes an int and filters the search results by files that exceed the given
			size in 	MB

--lang:			Filters the search by only listing repositories that are listed with the given 			programming language.

--short:			If enabled omits the individual item data for the search operation and instead 			just lists the summary.

--dldir:			Takes a filepath to use as a location for the download operation.
			Note: Required for the download operation.

-h | --help:		Shows some brief help text for the user.


Dependencies:

This project uses and requires PyGithub and the Github executable. These can be found here:

PyGithub:
https://github.com/PyGithub/PyGithub

Can be installed with  -  '$pip install pygithub'

Github executable:
https://desktop.github.com/


Functions:

Main:

Starts off by  defining 'argparse' arguments

Makes a call to the github API using 
The repositories are recieved by the call as a paginated list of repositories.

(Paginated list: http://pygithub.readthedocs.io/en/latest/utilities.html#github.PaginatedList.PaginatedList)

We then iterate through the list and decide on an action depending on if it's a search or download operation.

Search: Print information gathered from each repository object to the screen. Gather a summary of the total size of all the repositories so far.

Download: Pass the repository object onward to dlGitRepo to start downloading.

After this we print a short summary of the result, and done.


dlGitRepo(gitRepo, gitPath):

Takes a repository (link below) object and a filepath.

Checks to see if a directory already exists for the repository name. If true passes arguments for a git pull to git(*args), if false it instead passes a git clone.

(Repository object: http://pygithub.readthedocs.io/en/latest/github_objects/Repository.html)



git(*args):

Takes a list of arguments as strings and passes them to a subprocess commandline call to 'git' (ex: pull, clone).

Returns after executing the subprocess call.



Useful links:

PyGithub documentation:

http://pygithub.readthedocs.io/en/latest/introduction.html

Github page
https://github.com/PyGithub/PyGithub

Github API documentation:
https://developer.github.com/v3/
