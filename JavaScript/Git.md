## Create a new repository on the command line

```Bash
echo "# new-test" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/ChrisOnions/new-test.git
git push -u origin main
```

## Push an existing repository from the command line

```bash
git remote add origin git@github.com:ChrisOnions/Project-here.git
git branch -M main
git push -u origin main
```

## Pull Requests

```bash
$git Pull
# $git pull --rebase origin main
$git checkout <existing_branch>
$git checkout -b <new_branch>
# Branch
$git status
$git add .
$commit -m " message"
$git push
Go to github "Pull requests"
new pull request
base: main < compare: "Branch_being_added"
request review
wait for review / approval
delete merged branch and start a new one with a descriptive name.
```

## Hard reset main

```bash
$git reset --hard origin/main
```

## Rename case files

- Github isnt case sensative so you need to mv the file to rename
- Eg. readme.md to README.md
  <br><br>

```Bash
git mv -f readme.md README.md
```

<br>

## Common Cmd line Git

[Docs](https://www.datree.io/resources/git-commands)

```bash
1 – $git create branch
2 – $git force pull
3 – $git remove untracked files
4 – $git unstage
5 – $git undo merge
6 – $git remove file
7 – $git uncommit
8 – $git diff between branches
9 – $git delete tag
0 – $git rename branch
```
