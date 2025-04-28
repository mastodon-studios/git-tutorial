# Tutorial on Git and GitHub as a team

This guide will help you get started with Git and GitHub so we can all work smoothly together on our project.

## Install Git

### Windows

Download Git: https://git-scm.com/download/win
    
Install it with default settings (important: make sure "Git Bash" and "Git from Command Line" are checked).

### Mac

Ensure that homebrew is installed then use the following command in the terminal:

`brew install git`

### Linux (Ubuntu/Debian)
`sudo apt install git`

## Set Up Git (First Time Only)

After installing, set your name and email (the same email you use for GitHub):

`git config --global user.name "Your Name"`
`git config --global user.email "your@email.com"`

Display and check your current name and email with: `git config --list`

## Create or Clone a Repo

Our projects are within the GitHub Organization, Mastodon Games. You will either:

### Clone an existing repo with:

#### HTTPS
`git clone https://github.com/our-organization/project-name.git`

#### SSH
`git clone git@github.com:mastodon-games/game-idea-2.git`

### Create a new repo:

1. Go to the Organization's GitHub repositories page
2. Create a new repository
3. Initialize it without a README.md to get instructions on the next page on how to clone and make your first commit

## Basic Workflow 

Every time you want to work on the project, you should:

1. Pull the latest changes: 

Make a directory somewhere in your file system: `mkdir <project-name>`

Change directory to the project folder on your system: `cd <project-name>`

Then pull: `git pull origin main` (Replace main with your branch name if you're on another branch)

2. Create a New Branch (for any new feature)

NEVER work directly on main and always create a branch: `git checkout -b <your-branch-name>`

Examples:
`git checkout -b add-new-level`

`git checkout -b fix-bug-42`

3. Work and Save Changes

After editing files, check what changed: `git status`

Add changes you want to save: `git add <filename>`

Or to add everything: `git add .`

Then commit with a message: `git commit -m "Short clear message about what you did"`

4. Push Your Branch

Push your branch to GitHub: `git push origin your-branch-name`

5. Create a Pull Request (PR)
- Go to the GitHub repo in the browser
- Click the "Compare & Pull Request" button
- Review your changes and submit the PR
- Someone else should review it and merge

You should be committing whenever a new feature is added that works as intended and does not break any other code. Examples could include, adding a new working function, fixing typos, or finishing work for the day. Some days you might have 50 commits and some days you might have 1. This is all valid and YMMV. Always ensure to push your commits after you're done working for the day so other developers can view your changes.

## Reverting Changes

In software and game development, sometimes the code can end up broken and it may be easier to start fresh from code you know runs without error. This can be done multiple ways:

Revert to a specific commit and ignore any changes made since that commit: `git reset --hard <commit-id>`

Or you can revert to the previous commit with `git reset --hard HEAD`

There are many other commands that can be used depending on what you want to revert/what you want to keep, but they are out of scope of this tutorial.

## Merging Branches and Resolving Conflicts

Two people editing the same part of a file can cause a merge conflict.

To handle it properly, make sure your local branch is up to date with `git pull origin main`. If there’s a conflict, Git will tell you which files are conflicting. If you open the conflicting file in your text editor, you will see sections like:

`<<<<<<< HEAD`
`your changes`
`=======`
`their changes`
`>>>>>>> main`

Edit the file manually to fix it — keep the correct code and delete the `<<<<<<<, =======, and >>>>>>>` lines.

After fixing, do not forget to git add, commit, and push again.

Your PR should now be clean and ready to merge.

## Good Habits
- Always pull before you start working (git pull)
- Always create a new branch for each feature or bugfix
- Make small commits with clear messages and avoid waiting to make commits where there are multiple significant changes
- Communicate if you're about to touch big files that others might also be editing
- Review Pull Requests carefully and double-check code before approving

## Extra Commands You Might Need

List all local branches: `git branch`

List remote branches: `git branch -r`

Switch to a different branch or commit: `git checkout <branch-name or commit-id>`

Merge another branch into your current branch: `git merge <branch-name or commit-id>`

See a simple list of past commits: `git log --oneline`

See which remote repo you're connected to: `git remote -v`

## Git Graphical User Interface

If you prefer a visual interface over the terminal, you can install and use GitHub Desktop. This is also out of scope of this tutorial but a valid option if you prefer a GUI.

## Workflow TL:DR
1. `git pull origin main`
2. `git checkout -b feature-branch`
3. Make some changes
4. `git add .`
5. `git commit -m "your message"`
6. `git push origin feature-branch`
7. go to GitHub and create a PR

