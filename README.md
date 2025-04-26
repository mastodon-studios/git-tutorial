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

git config --global user.name "Your Name"
git config --global user.email "your@email.com"

Check your setup:

git config --list

## Create or Clone a Repo

Our projects are within the GitHub Organization, Mastodon Games. You will either:

### Clone an existing repo:

`git clone https://github.com/our-organization/project-name.git`

### Create a new repo:

1. Go to the Organization's GitHub page.

2. Create a new repository.

3. Then clone it as shown above.

## Basic Workflow (Always Follow This!)

Every time you want to work on the project, you should:
a. Pull the latest changes: 

By moving to the project folder on your system: `cd project-name`

Then pull: `git pull origin main`. (Replace main with your branch name if you're on another branch)

b. Create a New Branch (for any new feature)

NEVER work directly on main.
Always create a branch:

`git checkout -b your-branch-name`

Examples:

`git checkout -b add-new-level`
`git checkout -b fix-bug-42`

c. Work and Save Changes

After editing files, check what changed:

`git status`

Add changes you want to save:

`git add <filename>`

Or to add everything:

`git add .`

Then commit with a message:

`git commit -m "Short clear message about what you did"`

d. Push Your Branch

Push your branch to GitHub:

`git push origin your-branch-name`

e. Create a Pull Request (PR)
- Go to the GitHub repo in the browser
- Click the "Compare & Pull Request" button
- Review your changes and submit the PR
- Someone else should review it and merge

## Merging Branches and Resolving Conflicts

Two people editing the same part of a file can cause a merge conflict.

To handle it properly:
When merging:

1. make sure your local branch is up to date with `git pull origin main`

If there’s a conflict, Git will tell you which files are conflicting.

Open the conflicting file — you will see sections like:

<<<<<<< HEAD
your changes
=======
their changes
>>>>>>> main

Edit the file manually to fix it — keep the correct code and delete the <<<<<<<, =======, and >>>>>>> lines.

After fixing:

git add filename
git commit

Then push again:

    git push origin your-branch-name

Your PR will now be clean and ready to merge.

## Good Habits

    Always pull before you start working (git pull).

    Always create a new branch for each feature or bugfix.

    Small commits with clear messages are better than giant ones.

    Communicate if you're about to touch big files that others might also be editing!

    Review Pull Requests carefully — double-check code before approving.

## Extra Commands You Might Need
Command	Purpose
git branch	List all local branches
git branch -r	List remote branches
git checkout branch-name	Switch to a different branch
git merge branch-name	Merge another branch into your current branch
git log --oneline	See a simple list of past commits
git remote -v	See which remote repo you’re connected to

## Helpful Git GUI Tools (Optional)

If you prefer a visual interface over the terminal, you can install and use GitHub Desktop

## TL:DR
1. git pull origin main
2. git checkout -b feature-branch
3. Make some changes
4. git add .
5. git commit -m "your message"
6. git push origin feature-branch
7. go to GitHub and create a PR
