# My Personal Git & Version Control Cheatsheet

Hey there! These are my personal, simple notes and cheat sheet for learning Git. It covers what Git is, why we use it, our terminal practice review, and handy tricks to undo mistakes.

## Part 1: What is Git & Version Control?

* **Version Control:** Think of it like a Google Doc history for your code. It tracks every change so you can go back in time if something breaks.

* **Git:** A free, open-source tool that runs locally on your computer to keep track of file changes.

* **GitHub / GitLab:** Websites hosted in the cloud where you can store your code online and collaborate with friends or teammates.

### 3 Virtual Zones in Git:

1. **Working Directory:** Where you write, edit, and save files normally on your computer.

2. **Staging Area (Index):** The waiting room where you select which modified files are ready to be saved. (`git add`)

3. **Local Repository:** The permanent history database where changes are saved forever. (`git commit`)

### Essential Setup Commands:

```bash
# Check if Git is installed
git version

# Set up your identity (Git embeds this in every commit)
git config --global user.name "Your Name"
git config --global user.email "youremail@domain.com"

# View your settings
git config --list
```

## Part 2: Review Questions & Terminal Output Walkthrough

Here is how we did our review assignment step-by-step in the terminal:

### 1. Initialize Git repository & Add first file (`a.txt`)

```bash
mkdir git-review
cd git-review
git init -b master
```

*Output:*
```text
Initialized empty Git repository in /home/jyothish/git-review/.git/
```

Now let's create `a.txt`, stage it, and commit it:

```bash
touch a.txt
git add a.txt
git commit -m "Add a fileA"
```

*Output:*
```text
[master (root-commit) d68608c] Add a fileA
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a.txt
```

### 2. Create a branch called `leaf` and add `b.txt`

```bash
git branch leaf
touch b.txt
git status
```

*Output:*
```text
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	b.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Let's check our branch name and log history:

```bash
git branch --show-current
git log --oneline
```

*Output:*
```text
master
d68608c (HEAD -> master, leaf) Add a fileA
```

### 3. Switch to `leaf`, commit `b.txt`, and merge into `master`

```bash
git checkout leaf
git branch --show-current
```

*Output:*
```text
Switched to branch 'leaf'
leaf
```

Now commit `b.txt` on the `leaf` branch:

```bash
git add b.txt
git commit -m "Add a fileB"
```

*Output:*
```text
[leaf a15087f] Add a fileB
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 b.txt
```

Finally, switch back to `master` and merge `leaf`:

```bash
git checkout master
git merge leaf
git log --oneline
```

*Output:*
```text
Switched to branch 'master'
Updating d68608c..a15087f
Fast-forward
 b.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 b.txt
a15087f (HEAD -> master, leaf) Add a fileB
d68608c Add a fileA
```

## Part 3: Checking Understanding

* **What is the staging area?**
  It is a temporary holding area (index) where you place files using `git add` before committing them permanently to your project history.

* **Where is the HEAD right now?**
  `HEAD` points to your current active branch or commit. In our final step, it pointed to `master`, which contains all merged updates.

## Part 4: Undoing Changes

Suppose we have a project folder structure like this:

```text
my-project/
├── index.html
├── style.css
└── secret.txt  <-- (accidentally added or committed)
```

Here are quick commands to fix common issues:

### 1. You committed with the wrong message

```bash
git commit --amend -m "My corrected commit message"
```

*Why:* It updates your latest commit message without changing your files.

### 2. You forgot to include a file in your last commit

```bash
touch forgotten.txt
git add forgotten.txt
git commit --amend --no-edit
```

*Why:* It sneaks the new file into your previous commit immediately.

### 3. You accidentally committed on `master` instead of a new branch

```bash
# 1. Save your work into a new branch
git branch my-new-branch

# 2. Reset master back one commit safely
git reset --hard HEAD~1

# 3. Switch to your new branch where your work is safe
git checkout my-new-branch
```

### 4. You want to undo uncommitted changes to a specific file

```bash
git checkout -- index.html
```

*Why:* It discards local edits and restores the file back to the last saved commit.
