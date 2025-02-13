
# Git Workflow  

*"Git is a fast, distributed version control system."*  

This is not a definitive guide to *Git*. There’s extensive documentation available online, and none better than the official Git documentation.  

However, this talk will focus on how I use Git *for now*. My approach isn't perfect, but my goal is to demonstrate Git’s effectiveness and the powerful tooling it provides for managing projects ranging from simple applications to complex ones like the *Linux Kernel*.  

I will cover essential commands, focusing on the command line (CLI) for its simplicity and universality. GUI-based solutions ultimately run the same commands in the background.  

The first section covers local development commands, and the second focuses on collaboration across teams.  

Let’s get started.  

---

## Local Commands  

### Initializing a Repository  

A repository (repo) is a container for everything needed to manage a software project. To create a new repository, run:  

```bash
git init -b <branch_name>
```

This initializes a repo with `<branch_name>` as the default branch. The current convention is *main*, but you can name it *master*, *new*, or anything else.  

---

### Tracking Files  

Git helps developers track changes, prevent mistakes, and recover from errors. One of the most frequently used commands is:  

```bash
git status
```

This provides an overview of the repo’s current state, showing tracked, untracked, and staged changes.  

#### Adding Files to Tracking  

To track a specific file, run:  

```bash
git add <file_name>
```

To track all changes in the working directory:  

```bash
git add .
```

Running `git status` again will show that the files are staged.  

#### Committing Changes  

Once you're satisfied with the changes, commit them:  

```bash
git commit -m "Short description of the changes"
```

---

### Stashing and Discarding Changes  

If you don’t want to commit changes yet but also don’t want to lose them, stash them:  

```bash
git stash
```

This stores the changes safely so you can apply them later.  

To discard changes before committing:  

```bash
git restore --staged <file>
```

To discard **all** unstaged changes:  

```bash
git restore .
```

---

### Ignoring Files  

Some files (e.g., environment variables, compiled files) should not be tracked. Use a `.gitignore` file to specify these:  

```.gitignore
.env
*.pyc
node_modules/
```

This prevents Git from tracking the specified files.  

---

### Untracking Tracked Files  

If you accidentally tracked a file that should be ignored, remove it from version control:  

```bash
git rm --cached <file>
```

To remove all previously tracked `.pyc` files:  

```bash
git rm -r --cached *.pyc
```

---

### Branching  

Branches allow experimentation without affecting the main codebase. Creating a new branch is simple:  

```bash
git branch <branch_name>
```

To switch to the branch:  

```bash
git switch <branch_name>
```

Or create and switch to a new branch in one step:  

```bash
git switch -c <branch_name>
```

**Difference between `switch` and `checkout`**:  
- `switch` is more user-friendly and recommended for changing branches.  
- `checkout` is older and also used for checking out files.  

---

### Merging  

After making changes in a branch, merge them into the main branch:  

```bash
git merge <branch_name>
```

To create a new commit showing the merge history (instead of a fast-forward merge):  

```bash
git merge --no-ff <branch_name>
```

---

### Viewing History and Changes  

To see commit history:  

```bash
git log --oneline --graph --all
```

To see differences between commits or working state:  

```bash
git diff
```

---

## Collaborating with Git  

### Cloning a Repository  

To copy a remote repository to your local machine:  

```bash
git clone <repo_url>
```

This creates a local copy of the repo with all its branches and history.  

---

### Fetching Remote Changes  

To update your local repository with changes from the remote without merging them:  

```bash
git fetch
```

To fetch and merge changes into your current branch:  

```bash
git pull
```

---

### Branching Strategies  

Two common strategies for integrating changes:  

#### **Merge**  

Merging keeps all commit history but creates extra commits:  

```bash
git merge <branch_name>
```

#### **Rebase**  

Rebasing applies changes on top of another branch, creating a cleaner history:  

```bash
git rebase <branch_name>
```

---

### Fixing Mistakes  

To undo the last commit but keep the changes unstaged:  

```bash
git reset --soft HEAD~1
```

To undo the last commit and remove the changes:  

```bash
git reset --hard HEAD~1
```

To undo a pushed commit without rewriting history:  

```bash
git revert <commit_hash>
```
