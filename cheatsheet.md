
This file contains a list of common commands that will be used throughout the sessions

#Git

Clones a repo to your local git
```
$ git clone git@github.ibm.com:<Username>/<RepositoryName>.git
```
Checks the status of a branch
```
$ git status
```
List all local branches
```
$ git branch
```
Switches over to an existing branch
```
$ git checkout <BranchName>
```
Creates a new branch and switches over to it
```
$ git checkout <BranchName> -b
```
Adds a specific file(s) to the stage
```
$ git add <FileName> <FileName>...
```

Commits any stagged files to your local branch
```
$ git commit -m "Put your commit message in here"
```

Pushes your local branch to a remote repository where the branch does not exists
```
$ git push --set-upstream origin my-new-branch
```

Pushes your local branch to a remote repository
```
$ git push
```

Pulls any changes from a remote into your local branch
```
$ git pull
```

#Linux

List all files in the current folder
```
ls -al
```
List all files in a different folder
```
ls -al <PathToFolder>
```
Make a folder
```
mkdir <FolderName>
```
Remove a folder
```
rmdir <FolderName>
```
Change to a specific folder
```
cd /<path>/<To>/<Directory>/<File>
```

From your $HOME directory typically your user profile
```
cd ~/<path>/<To>/<Directory>/<File>
```

Creates an empty file in the current directory
```
Touch <FileName>
```

Removes a specific files
```
rm <FileName>
```

Opens up the file in the nano file editor
```
nano <FileName>
```

<!-- NPM
```
npm init
```

```
npm install <PackageName> -save
```

```
npm start
```

```
npm test
```

```
npm run <ScriptName>
```

```
npm install
``` -->
