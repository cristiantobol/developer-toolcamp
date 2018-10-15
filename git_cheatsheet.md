# Git

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

Commits any staged files to your local branch
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

Compares the unstaged changes on a local branch
```
git diff
```

Lists all the changed files
```
git diff --name-only
```

Compares the current branch against another local branch
```
git diff <BranchName>
```
