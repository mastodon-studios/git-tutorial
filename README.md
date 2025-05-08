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

## Add an SSH key to your GitHub account

### Check for existing SSH keys

Open your terminal and list all the files in your .ssh directory (if they exist): `ls -al ~/.ssh`
The filenames of supported public keys for GitHub are

- id_rsa.pub

- id_ecdsa.pub

- id_ed25519.pub

### Generate a new SSH key

You can skip this if you have an existing SSH key.

Open your terminal and paste the following command, replacing the example email with your GitHub email address `ssh-keygen -t ed25519 -C "example@example.com`

If you are using a legacy system that does not have support for the Ed25519 algorithm, use: `ssh-keygen -t rsa -b 4096 -C "example@example.com"`

These commands will create a new SSH key, associated with the provided email. You will then get the following prompts:

1. Enter a file in which to save the key (/home/YOU/.ssh/id_ALGORITHM):[Press enter]

2. Enter passphrase (empty for no passphrase): [Type a passphrase]

3. Enter same passphrase again: [Type passphrase again]

For our purposes, you can simply press Enter to use the default options for all of the prompts. You can read more about [generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) and [working with SSH key passphrases](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/working-with-ssh-key-passphrases).

### Adding your SSH key to the ssh-agent

Start the ssh-agent in the background: `eval "$(ssh-agent -s)"`

Add your SSH private key to the ssh-agent: `ssh-add ~/.ssh/id_ALGORITHM` which will most likely be `ssh-add ~/.ssh/id_ed25519`

### Add your SSH key to your GitHub account

1. Display the SSH public key in your terminal: `cat ~/.ssh/id_ALGORITHM.pub`

2. Select and copy the contents of your id_ALGORITHM.pub file that was displayed in your terminal

3. Navigate to the GitHub web page

4. Go to your settings by clicking your profile photo in the upper-right corner of the page then clicking Settings

5. Find the "Access" section of the sidebar and click "SSH and GPG keys"

6. Click "New SSH key" or "Add SSH key"

7. In the "Title" field, add a descriptive label for the new key. For example, if you're using a personal laptop, you might call this key "Personal laptop"

8. Set the key type to "Authentication key"

9. In the "Key" field, paste your public key

10. Click Add SSH key

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

Use lowercase and hyphens to separate words in branch names.

Examples:

```shell
# good
$ git checkout -b fix-billboarding

# also good: identifiers to corresponding GitHub issues
$ git checkout -b issue-15

# bad - too vague
$ git checkout -b menu_fix
```

We should avoid working on the same files/features to mitigate the amount of merge conflicts, but if that is unavoidable, you can use the following naming convention:

```shell
$ git checkout -b new-feature/main
$ git checkout -b new-feature/larry
$ git checkout -b new-feature/nicholas
```

Make sure to delete your branch after it is merged. This involves deleting the remote branch, the local branch, and the local remote-tracking branch.

1. Delete the remote branch: `git push origin -d <branch>`
2. Delete the local branch: `git branch -d <branch>` or `git branch -D <branch>` for force delete un-merged branches
3. Delete the local remote-tracking branch: `git branch -dr <remote>/<branch>` i.e. `git branch -dr origin/issue-21`

4. Work and Save Changes

After editing files, check what changed: `git status`

Add changes you want to save: `git add <filename>`

Or to add everything: `git add .`

Then commit with a message: `git commit -m "Short clear message about what you did"` or `git commit` in which you will then edit the first line of the `COMMIT_EDITMSG` file with your commit message.

Commits should be no longer than 50 characters. Examples of commits:

```shell
# good - imperative present tense, capitalized, fewer than 50 characters
Mark huge records as obsolete when clearing hinting faults

# bad
fixed ActiveModel::Errors deprecation messages failing when AR was used outside of Rails.
```

4. Push Your Branch

Push your branch to GitHub: `git push origin your-branch-name`

If the repository has been updated since you last made changes you may need to `git pull --rebase`. This will fetch the updates from the repository and re-apply your local commits on top of those changes. This is assuming that the missing updates are in separate parts of the repository and will help avoid unnecessary merge conflicts.

5. Create a Pull Request (PR)

- Go to the GitHub repo in the browser
- Click the "Compare & Pull Request" button
- Review your changes and submit the PR
- Someone else should review it and merge

You should be committing whenever a new feature is added that works as intended and does not break any other code. Examples could include, adding a new working function, fixing typos, or finishing work for the day. Some days you might have 50 commits and some days you might have 1. This is all valid and YMMV. Always ensure to push your commits after you're done working for the day so other developers can view your changes.

## Reverting Changes

In software and game development, sometimes the code can end up broken and it may be easier to start fresh from code you know runs without error. This can be done multiple ways:

Revert to a specific commit and ignore any changes made since that commit: `git reset --hard <commit-id>`

Or you can revert to the previous commit: `git reset --hard HEAD`

There are many other commands that can be used depending on what you want to revert/what you want to keep, but they are out of scope of this tutorial.

## Merging Branches and Resolving Conflicts

Multiple people editing the same part of a file can cause a merge conflict.

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
7. `git pull --rebase` if the repo has been updated since you last pulled
8. go to GitHub and create a PR

## Resources
