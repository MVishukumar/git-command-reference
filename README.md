# Useful Git usecases

## Set up our Git globally

```sh
git config --global user.name "Your name"
git config --global user.email "Your email"
```

## How to cache your login credentials in Git
You can store login credentials in the cache so you don't have to type them in each time. Just use this command:
```
git config --global credential.helper cache
```

## Initializing your Repository

Then type in `git init` and hit enter.

## Making Your First Commit in Git

`git add name-of-files` or `git add .`

```sh
git commit -m "commit message"
```

## How to commit changes (and skip the staging area) in Git:
You can add and commit tracked files with a single command by using the -a and -m options.
```
git commit -a -m"your commit message here"
```

## Checking the Status of Your Files

```sh
git status
```

## Ignoring Files

You can create a file listing patterns to match them named `.gitignore`.

## Skipping the Staging Area

Adding the `-a` option to the `git commit` command makes Git automatically stage every file that is already tracked before doing the commit, letting you skip the `git add` part.

```sh
git commit -a -m 'Add new benchmarks'
```

## How to see changes made before committing them using "diff" in Git:
You can pass a file as a parameter to only see changes on a specific file.
`git diff` shows only unstaged changes by default.

We can call diff with the `--staged` flag to see any staged changes.
```
git diff
git diff all_checks.py
git diff --staged
```

## Removing Files

To remove a file from Git, you have to remove it from your tracked files and then commit. The `git rm` command does that, and also removes the file from your working directory so you don’t see it as an untracked file the next time around.

Use --cached option to retain files in hard drive but ignore from git tracking software.

```sh
git rm --cached README
```

## Moving Files or Renaming files

```sh
git mv file_from file_to
```

## Viewing the Commit History

```sh
git log
```

One of the more helpful options is `-p` or `--patch`, which shows the difference (the patch output) introduced in each commit. You can also limit the number of log entries displayed, such as using `-2` to show only the last two entries.

```sh
git log -p -2
```

Another really useful option is `--pretty`. This option changes the log output to formats other than the default. A few prebuilt option values are available for you to use. The `oneline` value for this option prints each commit on a single line, which is useful if you’re looking at a lot of commits.

```sh
git log --pretty=oneline
git log --pretty=format:"%h - %an, %ar : %s"
git log --pretty=format:"%h %s" --graph
```

## Limiting Log Output

```sh
git log --since=2.weeks
```

## Undoing Things

One of the common undos takes place when you commit too early and possibly forget to add some files, or you mess up your commit message. If you want to redo that commit, make the additional changes you forgot, stage them, and commit again using the --amend option:

```sh
git commit --amend
```

This command takes your staging area and uses it for the commit. If you’ve made no changes since your last commit (for instance, you run this command immediately after your previous commit), then your snapshot will look exactly the same, and all you’ll change is your commit message.

## Unstaging a Staged File

```sh
git reset HEAD <file>...
git reset HEAD CONTRIBUTING.md
```

## Unmodifying a Modified File

```sh
git checkout -- CONTRIBUTING.md
```

## Creating Branches in Git

To create a new branch in git, use the command, `git branch nameOfBranch`.
To check out (switch) to the new branch, use `git checkout nameOfBranch`.

The above 2 commands can be done simultaneously using the command: `git checkout -b nameOfBranch`.

## What does "origin" mean?

Origin is a shorthand name for the remote repository that a project was originally cloned from. More precisely, it is used instead of that original repository's URL, and makes referencing it easier.‌‌

## Add Remote Repositories

When you clone a repository, Git implicitly adds that repository as the origin remote for you. To add a new Git repository, you use this command:

```sh
git remote add <shortname> <url>
```

where `shortname` is a unique remote name and url is the url of the repository you want to add.

For example, if I want to add a repository with the shortname `upstream`, I can do this:

```sh
git remote add upstream https://github.com/sarahchima/personal-website.git
```

Remember that your `shortname` can be anything, it just has to be unique, that is different from what the names of the remote repositories you already have.

To view the list of remote URLs you have added, run the following command:

```sh
git remote -v
```

## Change remote repositories

```sh
git remote set-url <an-existing-remote-name> <url>
```

Using the example above, if I want to change the remote URL, I'll do this:

```sh
git remote set-url upstream git@github.com:sarahchima/personal-website.git
```

Remember to run `git remote -v` to verify that your change worked.

## Fetching and Pulling from Your Remotes

To get data from your remote projects, you can run:

```sh
git fetch <remote>
```

If your current branch is set up to track a remote branch, you can use the `git pull` command to automatically fetch and then merge that remote branch into your current branch.

## Renaming and Removing Remotes

You can run `git remote rename` to change a remote’s shortname. For instance, if you want to rename `pb` to `paul`, you can do so with `git remote rename`:

```sh
$ git remote rename pb paul
$ git remote
origin
paul
```

## Delete a branch both locally and remotely

To delete a branch locally, make sure you are not on the branch you want to delete. So you have to checkout to a different branch and use the following command:

```sh
git branch -d <name-of-branch>
```

So if I want to delete a branch named `fix/homepage-changes`, I'll do the following:

```sh
git branch -d fix/homepage-changes
```

You can run git branch on your terminal to confirm that the branch has been successfully removed.

To delete a branch remotely, you use the following command:

```sh
git push <remote-name> --delete <name-of-branch>
```

If I want to delete the branch `fix/homepage-changes` from `origin`, I'll do this:

```sh
git push origin --delete fix/homepage-changes
```

## Merge a file from one branch to another

First, checkout to the right branch (the branch you want to merge the file) if you've not already done so. In our case, it's the development branch.

```sh
git checkout development
```

Then merge the file using the `checkout --patch` command.

If you want to completely overwrite the index.html file on the development branch with the one on the master branch, you leave out the `--patch` flag.

```sh
git checkout master index.html
```

Also, leave out the `--patch` flag if the `index.html` file does not exist on the development branch.

## Undo a commit

#### How to undo a local commit

One way you can undo a commit locally is by using git reset. For example, if you want to undo the last commit made, you can run this command:

```sh
git reset --soft HEAD~1
```

The `--soft` flag preserves the changes you've made to the files you committed, only the commit is reverted. However, if you don't want to keep the changes made to the files, you can use the `--hard` flag instead like this:

```sh
git reset --hard HEAD~1
```

Note that you should use the `--hard` flag only when you are sure that you don't need the changes.

If you want to undo a commit before that, you can use git reflog to get a log of all previous commits.

```sh
git reset --soft 9157b6910
```

#### How to undo a remote commit

```sh
git reflog
```

```sh
git revert 9157b6910
```

Finally, push this change to the remote branch.

## How to check remote branches that Git is tracking:
This command shows the name of all remote branches that Git is tracking for the current repository:
```
git branch -r
```

## How to fetch remote repo changes in Git:
This command will download the changes from a remote repo but will not perform a merge on your local branch (as git pull does that instead).
```
git fetch
```

## How to check the current commits log of a remote repo in Git
Commit after commit, Git builds up a log. You can find out the remote repository log by using this command:
```
git log origin/main
```

## How to merge a remote repo with your local repo in Git:
If the remote repository has changes you want to merge with your local, then this command will do that for you:
```
git merge origin/main
```

## How to push a new branch to a remote repo in Git:
If you want to push a branch to a remote repository you can use the command below. Just remember to add `-u` to create the branch upstream:

```
git push -u origin branch_name
```

## Listing Your Tags

```sh
git tag
```

You can also search for tags that match a particular pattern. The Git source repo, for instance, contains more than 500 tags. If you’re interested only in looking at the 1.8.5 series, you can run this:

```sh
git tag -l "v1.8.5*"
```
