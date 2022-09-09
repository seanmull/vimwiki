## Git ignore
.gitignore will prevent untracked files from being added (without an add -f) to the set of files tracked by Git. However, Git will continue to track any files that are already being tracked.

To stop tracking a file, we must remove it from the index:

```
git rm --cached <file>
```
To remove a folder and all files in the folder recursively:

```
git rm -r --cached <folder>
```
The removal of the file from the head revision will happen on the next commit.

WARNING: While this will not remove the physical file from your local machine, it will remove the files from other developers' machines on their next git pull.

Make sure to install dependencies on dependencies not in dev for the package.json
https://stackoverflow.com/questions/18875674/whats-the-difference-between-dependencies-devdependencies-and-peerdependencies
