name: title
class: center, middle

# Leveraging Git
## for your development workflow
.title-logo[![Right-aligned image](img\Git-Icon-1788C.png)]

---

name: agenda
# Agenda

1. Introduction
2. A bit about Git
  * History
  * Fundamentals
3. Tips for daily use
  * Preparing your commits<br>
    `git add`, `git commit`
  * Digging in the past <br>
    `git log`
  * Adapting Git to your needs <br>
    `git config`
  * Rewriting History <br>
    `git commit --amend`, `git rebase`
4. The bigger picture
  * Centralized Workflow
  * Feature Branches
  * GitFlow
  * Forking Workflow
5. Further pointers

---

class: middle

What are the 3 most important tools for modern software development?

???

* Editor
* Source Control
  * .addendum[also known as: Version Control, Revision Control, Source Control Managment]
* Build infrastructure

---

# Introduction

```
$ git init
```

<br>

* Professional software development relies on source control
* Especially for
  * Big teams
  * Agile development
  * Release Management

* In short: Source control is _essential_ for, but not limited to, multi-developer software projects.

???
A modern software project deserves a modern Source Control

---

class: center, middle

# A bit 'bout git

---

# History
## The dark, centralized ages

* Concurrent Versions System (CVS), 1990
  * Was very widespread, esp. in OSS community
* Subversion (SVN), 2000
  * “CVS done right”
* Visual Source Safe (VSS), 2005
  * File locks, occasionally corrupts files
* Team Foundation Server (TFS), 2006
  * SVN but you have to pay for it

???

* CVS Development stopped in 2008
* SVN tried to fix mistakes from CVS, but failed to update its broken core principles
* VSS was hell
* TFS is more than Source Control. Huge step from VSS, but __TFVC__ is still bad, makes the same mistakes as SVN.
  * Also: the default Source Control for TFS is now git.
---

# History
## The distributed age

* Bitkeeper, 2000
  * Proprietary, but was used for Linux kernel
* **Git**, 2005
  * Developed by Linus Torvalds to replace Bitkeeper
* Mercurial, 2005
  * Also tried to replace Bitkeeper for Linux. Now used e.g. by Facebook and Mozilla
* Bazaar, 2005
  * A mix of distributed and centralized concepts

???

* The first three are all a bit related.
* Bitkeeper was proprietary, but a free community version existed and was catered for linux
  * Bitkeeper finally became Open Source in 2016
* There were concerns about using proprietary software for a flagship OSS project.
  * Torvalds was not quite happy with Bitkeeper anyway and decided to "do it right"
* At the same time, Matt Mackall implemented Mercurial for use with the Linux Kernel
  * Technically, the systems are quite similar
* Mercurial vs. Git was a holy war in hacker culture
  * In the end, the Linux Kernel Project chose Git.

* Mercurial:
  Mozilla, Facebook


---

# Distributed Source Control
## Concepts

* Peer-to-peer approach instead of single, central repository
* Every clients copy is a complete repository, including full History
  * You can still have a 'main' repository - but its not different from your local one
* Common operations are local
* Communication is only necessary when sharing changes amongst peers.

.full-width[![Centered image](img/centralized_vs_distributed.PNG)]

---

# Distributed Source Control
## Benefits

* Obvious benefit: Offline Working
* Improves collaboration
  * Commit changes without disturbing others
  * Branching is inherent
* Performance
  * Operations are local

???

* Offline Working:
  * Be in a plane or wherever, you can access the whole log, commit, etc
  * But it's much more

* Collaboration:
  * Not talking about feature branches. Everybody has his own branch by design, branched from the origin one.
  * Branching is more inherent when being distributed

* Performance:
  * SC should help you, not slow you down. So it _has_ to be fast.

---

# Distributed Source Control
## Benefits

* Trust
  * You can trust your data
    * Without trusting everybody else
    * Without trusting your hosting
* Release Engineering
  * Managing versions was never easier
* Security
  * No single point of failure
  * Natural data replication
  * Everything is checksummed
  * Keep your master copy behind 3 firewalls

???

* Trust:
  * You are the master of your repository
  * People can have read access and do their work incl. branching and commit - but they can't read
  * Which hoster would you trust the _master copy_ of your source code with?

* Security
  * SHA-1 is not as secure anymore
  * The hash is mostly a consistency feature, but has security benefits

---

# What Professional Developers use in 2017
![image](img/version_control_so_survey.PNG)

.addendum[Source: Stack Overflow Developer Survey 2017]

---

# Who uses Git

Some important players:
* Linux Kernel project
* Google
* facebook
* Microsoft is migrating Microsoft Windows development to git
  * They're developing the Git Virtual File System (GVFS)
* Twitter
* LinkedIn
* Netflix
* Eclipse Foundation
* Android
* etc...


---

# Key points

Git is
  * distributed
  * fast
  * powerful
  * widespread
  * well-proven
  * free

So you should probably use it!

---

class: center, middle

# Fundamentals

---

# Git in a nutshell

* History: A one-direction graph
* Git: A set of tools to manipulate it

---

# Primitives

Data structures:
  * _blob_: content of a file
  * _tree_: Hierarchy of blobs, a directory
  * _commit_: Contains a tree (the top-level directory), a timestamp, a message and reference 0-2 parents.

Note: Everything is identified via its SHA-1 hash!

References:
  * _heads_: Refers to an object locally
    * _HEAD_: Refers to the currently checked out commit
    * _branches_: Refer to a commit, 'follows' commits when checked out
  * _remotes_: Refers to an object in a remote repository
  * _stash_: Refers to an uncommitted object
  * _tags_: Refers to a fixed point in history

---

# Tooling
## Basic Setup

My personal setup for Windows:
* Git for Windows
* cmder
  * Unix-like shell based on ConEmu
  * comes with Git for Windows
* VS Code

???

TODO: Decide where to put this

* Git for Windows
  * Brings their own bash
* cmder
  * Looks nice
  * Unix-commands are easier and more versatile than windows cmd
  * Integrates better with git, which is a linux tool
* VS Code
  * lightweight and nice

---

# Tooling
## Graphical User Interfaces

* Nice to visualize History
* Can help with some operations
* Never as powerful or precise as the CL
* May hide or rename operations
* Examples:
  * Tortoise Git
  * Sourcetree
* Note: git comes with gitk

???
TODO: Decide where to put this

* Why not GUI:
  * Use CL at the beginning to really understand what you are doing
  * After that, you are probably quicker in the CL already
  * Allows for more customization

* Tortoise Git
  * Based on Tortoise SVN
  * Looks a bit dated, but is quite powerful
* Sourcetree
  * By Atlassian

---

# Tooling
## Hook your tools of choice into git

You can define the default editor via the config too:
```
$ git config --global core.editor code
```

The same goes for individual diff/merge tools:
```
$ git config --global diff.tool bc
$ git config --global difftool.bc.path "C:\Program Files\Beyond Compare 4\BComp.exe"
```

Tip: Beyond Compare lets you compare images as well

---

class: center, middle

# Tips for daily use

---

# The basics
## you probably already know
```
$ git pull
```
To sync your local repository

```
$ git add
```
To stage files for a commit

```
$ git commit
```
To commit the staged files

```
$ git push
```
To sync your changes to your main repository

.center[But Git can do __so much__ more!]

---

# Preparing your commits
## Of course there's also a layer diagram

Git knows three areas where your changes can be:

.areas[![Centered image](img/areas.png)]

.addendum[The stash can be viewed as a fourth area] 

---

# Preparing your commits
## Setting up the stage

```
$ git add <file or directory>
```
To add a specific file.

```
$ git add -A
```
Adds all unstaged files, including untracked (new) ones. 

```
$ git add -i
```
Opens an interactive environment to add files.

---

# Preparing your commits
## Have full control

```
$ git add -p
```
`-p` initiates 'patch mode'. This allows you to
* Select which _parts_ of your changes you want to stage
* Review your work!


* Git slices your changes into separate 'hunks'
* You can edit them with `e`
  * If you want to exclude a line, just comment it out

```python
+def my_new_function(a, b) {
#+  a = a * 2;
+  return a + b;
+}
```

---

# Preparing your commits
## If that's too much fuss for you

If you want to keep it simple:
```
$ git commit -a -m "Added some stuff"
```
.addendum[Note: This does not add untracked files!]

We will shorten this later.

???

Oftentimes, it's enough to just add all files and commit them right away

---

# Digging in the past
## The log command

```
$ git log [file]
```
Shows you the commit logs, most recent at top

```
$ git log -3
```
Shows you only the 3 most recent commits

```
$ git --after="2017-08-21" --before="2017-09-02"
```
Shows you only commits between those two dates.
Great to list commits from a specific sprint or search for a bug.

```
$ git --author="Johnny"
```
Shows only the commits where the author contains "Johnny". Allows for Regular expressions too!

---
# Digging in the past
## More filters

```
git log --grep="JRA-1983"
```
Filters commits by their message. Very useful if you include your issue-ID in the message (which you should)
```
$ git log -L <start>,<end>:<file>
$ git log -L 42,50:MyFile.cs
```
Tracks the history of the code on line 42 - 50 in your file. Shows you e.g. how a method evolved.


---
# Digging in the past
## Comparing your branches

```
$ git log <since>..<until>
```
Allows you to show commits in a range between two _commit references_.

This is especially great to compare branches:
```
$ git log master..feature
```
Shows you the commits which are in the feature branch, but not in the master branch.

If you switch it to `feature..master` you will see what commits are missing from feature

---

# Digging in the past
## Formatting the output

```
$ git log --oneline
```
Shows you a much quicker summary

```
$ git log --stat
```
For each commit, list all changed files and how many lines changed

```
$ git log --patch
```
If you want to see the whole diffs for each commit

```
$ git log --graph
```
Draws your history as an ASCII graph. Look at your history as the graph it really is.

---

# Digging in the past
## Going crazy with formatting

By combining formatting and including some _pretty_ formatting, you can get really nice outputs:
```
$ git log --graph --abbrev-commit --decorate --pretty=format:"%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)" --all
```

It's not quite easy to type though...

---

# Adapting Git to your needs
## Aliases

Aliases allow you to save complex commands under a simpler name.

They can save you time:

```
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
```

Or nerves:
```
$ git config --global alias.gerp grep
```

Use aliases to adapt the default behaviour in a way that suits you:
```
$ git config --global alias.stash stash --include-untracked
```

.addendum[Without the `--global` flag, the alias is only applied to the current repository]

???

* There is no specific alias command in git
* You do it via git config, which updates the local or global git config (just a file .git/config)

* The stash command by default only works on unstaged and staged changes, but ignores untracked files (e.g. new ones) 

---

# Adapting Git to your needs
## Aliases for chained commands

The `!` prefix lets git execute the command in the shell. This allows you to
* chain multiple git commands
* include shell commands
* use parameters

```
$ git config alias.findBranch = "!git branch | grep -i"
$ git findBranch JIRA-123
```
This helps you find the correct feature branch for an issue.

Tip: Wrap more complex commands into a shell function: 
```
[alias]
bclean = "!f() {
    git branch --merged ${1-master} 
    | grep -v \" ${1-master}$\" 
    | xargs -r git branch -d; }; f"
```
This cleans up all merged branches.

???

* First snippet
  * Note that Parameters are appended to the end!
* Second snippet
  * lists all branches which are merged into a branch (argument)
  * grep to exclude the branch itself
  * then delete them
  * $n is the nth argument
  * note that $0 is the script itself
  * ${1-master} means that the default value for the first argument is "master"

---

# Adapting Git to your needs
## Aliases for providing structure

Aliases for (semantic commit messages)[https://seesparkbox.com/foundry/semantic_commit_messages] including Issue ID:
```
[alias]
feat     = "!f() { git commit -m \"$1 - feat: $2\" }; f"
docs     = "!f() { git commit -m \"$1 - docs: $2\" }; f"
chore    = "!f() { git commit -m \"$1 - chore: $2\" }; f"
fix      = "!f() { git commit -m \"$1 - fix: $2\" }; f"
refactor = "!f() { git commit -m \"$1 - refactor: $2\" }; f"
```

```
$ git chore JRA-123 "updated build script"
[master 2ff195d] JRA-123 - chore: updated build script
```

???

Semantic commit messages:
  * Add the type of task you did to your commit messages
  * Goal: Don't mix different tasks into commits
    * E.g. bugfixes and features shouldn't be in one commit

Having the Issue Id in there is always a good idea

Could be more sophisticated of course
If one thinks this further, maybe you could parse the issue id from the feature branch

---

# Adapting Git to your needs
## Aliases for recurring tasks

```
[alias]
cma = !git add -A; git commit -m
caa = commit -a --amend -C HEAD
```

For your daily standup:
```
[alias]
standup = !git log --all --author=$USER --since="9am yesterday" --format=%s
```

.addendum[Source: Tim Pettersen from BitBucket]

--
```
lazy-standup = !git standup | say
```

???
* standup:
  * shows commits from all branches
  * filters by my user (just hardcode it if $USER is not supported)
  * filters only commits since the last daily
    * not the amazing datetime parsing
  * formats it to only show the subject

* lazy-standup
  * pipes the output to a speech synthesyzer (say on macos)
  * great if your working from remote!

---

# Adapting Git to your needs
## Sharing Aliases in your project

Use git of course!

Store them e.g. in a separate repository

Then link them in your local or global config via `[include]`
```
[include]
./path/to/your/repository
```

.addendum[Note: do not include random stuff - it's code you execute locally]

---

# Rewriting History
## Things can get messy

.guitar-hero[![image](img/guitar_hero.png)]

???
  * if your history looks like a guitar hero level on hard, then it's time to clean up

---

# Rewriting History
## Erasing your mistakes

```
$ git commit --amend 
```
To _add_ the staged changes to the latest commit.

Lets you update the commit message too.

---

# Rewriting History
## The catch

.half-width.center[![image](img/amend_1.png)]

--

```
$ git commit --amend 
```
.half-width.center[![image](img/amend_2.png)]

???

* actually copies the commits
  * also mention show reflog
* show graph with example

---

# Rewriting History
## An alternative to merging

```
$ git rebase <branch>
```

* goes to the common ancestor
* takes all commits which are not in `<branch>`
* applies them on `<branch>`

Primary reason: maintaining a __linear__ project history

Rebasing is saying

.center[ “I want to base my changes on what everybody has already done.” ]

---

# Rewriting History
## Merging example

.fixed-height-300[![image](img/rebase_initial.png)]

Initial state

---

# Rewriting History
## Merging example

.fixed-height-300[![image](img/rebase_merged.png)]

```
$ git checkout master
$ git merge feature
```
Results in a merge commit

---

# Rewriting History
## Merging example

.fixed-height-300[![image](img/rebase_initial.png)]

Let's try this again

---

# Rewriting History
## Rebasing example

.fixed-height-300[![image](img/rebase_rebased.png)]

```
$ git checkout feature
$ git rebase master
```
Reapplies the change in `feature` onto `master`

---

# Rewriting History
## Rebasing example

.fixed-height-300[![image](img/rebase_fastforwarded.png)]

```
$ git checkout master
$ git merge feature
```
`master` can now be _fast forwarded_ to `feature` 

---

# Rewriting History
## Merging vs. Rebasing example

.center[
.fixed-height-200[![image](img/rebase_mess.png)]

vs

.fixed-height-200[![image](img/rebase_fastforwarded.png)]

]

???

TODO: The graphic in this slide is wrong
feature is at the wrong place
master would get fastforwarded to E 

* Let's say you wanted to merge master into feature first
  * to sync them
  * to be able to integrate on your branch
  * this results in a huge mess
* rebase is easy
  * it just takes what you did
  * and it applies it somewhere else
* note: you can still have merge conflicts

---

# Rewriting History
## Interactive Rebase: Refactor your history

```
$ git rebase -i HEAD~3
```

```
pick f7f3f6d JRA-123 set up basic skeleton
pick 310154e JRA-123 implemented parts of the feature
pick a5f4a0d JRA-123 added some documentation

# Rebase 710f0f8..a5f4a0d onto 710f0f8
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

???

* git hides some of its most powerful features behind just one small option
* git rebase -i HEAD~3
  * rebases HEAD~3 onto HEAD
  * just use HEAD~n if you want to edit the last n commits
  * opens an editor window
* you can edit this like a script now
* this script runs from top to bottom

---

# Rewriting History
## Interactive Rebase: Example

```
pick    f7f3f6d   JRA-123 set up basic skeleton
reword  310154e   JRA-123implemented the feeture
edit    a5f4a0d   JRA-123 added some documentation
pick    98fea92   JRA-123 started with some performance improvements
squash  21aa923   JRA-123 finished performance improvements
pick    9e18af3   JRA-123 refactored the main class
fixup   872fd88   JRA-123 fixed bug introduced during refactoring

# Rebase 710f0f8..872fd88 onto 710f0f8
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
```

```
f7f3f6d   JRA-123 set up basic skeleton
310154e   JRA-123 implemented the feature
a5f4a0d   JRA-123 added some documentation
98fea92   JRA-123 performance improvements
9e18af3   JRA-123 refactored the main class
```

???

* Also allows you to reorder commits!

---

# Rewriting History
## The history is written by winners

Changing your log is actually encouraged!

Git offers powerful tools to do so:
  * `git commit --amend`
  * `git rebase`
  * `git rebase -i`

This allows you to get rid of all those _"added comment"_, _"fixed typo"_, _"stylecop"_ commits

Important: only update the history of your __private__ branches

???

Git offers powerful tools to do so:
  * Amending commits with `git commit --amend`
  * Rebasing your branch onto another one with `git rebase`
  * Shaping your history with `git rebase -i`

Get rid of all the clutter in your history
This makes it easier to
  * understand your projects history
  * undo features
  * find bugs

---

class: center, middle

# The bigger picture

---

# Centralized Workflow
## A good start

Git can be used similar to a centralized VCS:
* One central repository
* Only one development branch `master`
* Devs clone the central repository
* They make local commits etc.
* Changes are rebased onto `origin/master`, then pushed

To keep history linear, always pull with
```
$ git pull --rebase origin master
```
.addendum[You want to "add your changes to what they already did"]

---

# Centralized Workflow
## Example

.full-width[![image](img/centralized_workflow_1.png)]

???
initial state, we just cloned the central repository
repository has only a master branch
---

# Centralized Workflow
## Example

.full-width[![image](img/centralized_workflow_2.png)]

???
Some work was done on the master in the central repository
We fetched those, they are reflected on origin/master

meanwhile, we also did some local work ourselves
---

# Centralized Workflow
## Example

.full-width[![image](img/centralized_workflow_3.png)]

???
instead of merging into origin/master, we rebase our work on it.

the last two steps can be achieved with `git pull --rebase`

---

# Centralized Workflow
## Example

.full-width[![image](img/centralized_workflow_4.png)]

???
when we push, master will be fast forwarded

---

# Centralized Workflow
## Conclusion

Ideal for teams coming from a centralized VCS
* Requires only a handful of commands
* Only one main branch (or _trunk_)
* Results in a linear history

Advantages over SVN/TFS:
* Every developer has his own local copy of the project
* Profit from Git's robust branching and merging model

---

# Feature Branches
## Streamline communication between developers

Feature development only on dedicated branches instead of the master
  * Feature branches can be pushed anytime

When a feature is done, create a _Pull Request_
  * Like _"Please pull my changes into master"_

Only when reviewed and accepted, merge it into master

<br>
__Pull Requests__:
  * Not a Git feature per se
  * Use Gerrit, Bitbucket, Github etc.

???

Feature branches are the logical next step

One of the most important workflows

Feature branches can be pushed anytime
  * so you get a backup for free
  * makes it easy to share code

Pull requests make code reviews convenient
  * you can look at the feature as a whole (by diffing it to `master`)
  * anybody, e.g. the reviewer, can merge it when done, not only the dev who created it

---

# Feature Branches
## Example

.full-width[![image](img/feature_branches_1.png)]

???

no separate client/server view, because the repository can be synced at any time

---

# Feature Branches
## Example

.full-width[![image](img/feature_branches_2.png)]

---

# Feature Branches
## Example

.full-width[![image](img/feature_branches_3.png)]

Feature branch is _merged_ into `master`

---

# Feature Branches
## Example

.full-width[![image](img/feature_branches_4.png)]

Alternatively: Feature branch is _rebased_ onto `master`

???

Pro: You have a more linear history on master
Contra: You have more commits on master, can't revert features as easily

---

# Feature Branches
## Conclusion

Feature branches offer lots of benefits:
  * Work on features never disturbes the main code base
  * `master` never contains broken or unfinished features
  * Easy to work on two features in parallel
  * Sharing WIP features without touching the official code base
  * Allow for pull requests, which are great for code reviews

Tip: Use descriptive names incl. issue number
E.g. JRA-123-log-out-function

Protip: Use your CI infrastructure to build and test feature branches too.

---

# GitFlow
## A way to make modern software development manageable

A strict branching model created by [Vincent Driessen](http://nvie.com/posts/a-successful-git-branching-model/)
* Designed around releases
* No new concepts or commands 
* Robust for managing larger projects

---

# GitFlow
## Example

.full-width[![image](img/gitflow_1.png)]

Two eternal branches:
* __`master`__: The 'official' release history
  * Contains only merge commits
  * Each commit is tagged with a version
  
* __`develop`__: Integration branch for features
  

???

* You could deploy the current release at any time from master
* You'd had a nightly build on develop

---

# GitFlow
## Example

.full-width[![image](img/gitflow_2.png)]

Development happens in __feature branches__ off `develop`.

Merge back into `develop` with
```
$ git checkout develop
$ git merge --no-ff myFeature
```

???

The interaction between develop and feature branches is just the feature branches workflow described before
Note: Feature branches can also 'skip' a version, no problem

The no-ff part is critizised by some, rebasing is an alternative

---

# GitFlow
## Example

.full-width[![image](img/gitflow_3.png)]

When a release is approaching, a __release branch__ is created
  * Only bugfixing and documentation is done on there
  * When done, merge release into `master` and back into `develop`

???

* Once develop has acquired enough features for a release you fork a release branch
* branch is for stabilizing the release, make it ready, without development interfering
* Of course you can (or even should) develop bugfixes in their own feature branches
* makes it possible for one team to polish the current release while another works on new features
---

# GitFlow
## Example

.full-width[![image](img/gitflow_4.png)]

__Hotfix__ branches off `master` to patch production releases
  * Once done, it is merged into `master` and `develop`

???
* similar to a release branch for master
* this way, urgent fixes do not block development
* no need to wait for the next release cycle

---

# GitFlow
## Conclusion
Very strict and robust, but can be hard to follow.

Can be more complex than you need
  * E.g. master branch is kinda redundant
  * History tends to become very complicated

Feel free to tailor it to _your_ project

.full-width[![image](img/gitflow_5.png)]

???
Don't be afraid to adopt some aspects of the workflow and disregard others

E.g. the master branch is kinda redundant, if you don't need to build from it you can also tag `develop`

---

# Forking Workflow
## Going fully distributed

On a developer level .addendum[(the Open Source approach)]
  * Every developer has his own server-side repository
  * _Only_ project maintainer can push to the official repository

On a supplier level
  * Project team works on the official repository
  * Suppliers have their forks, no write-access to offical repository
  * Project team pulls work from suppliers after reviewing them

.fixed-height-300.center[![image](img/forking_workflow.png)]

???

* allows maintainer to accept commits from any developer without giving them write access to the official codebase

 
---

# The bigger picture
## Conclusion

Git allows for a variety of Workflows

There is no one-size-fits-all

Think about what fits _your_ team and project

---

class: center, middle

# Further pointers

---
# Further pointers
## Just a dump of some more stuff

`git rerere`
  * lets you record changes you made during merges and applies them automatically the next time

`git filter-branch`
  * lets you scrub the entire history
  * useful if you e.g. want to
    * remove a file from the entire history
    * change an authors email adress globally 

Git LFS
  * An extension for versioning large files
  * If you need to store huge assets in your repository

???

* git rerere
  * useful if you rebase a lot
* filter-branch
  * be cautios with that
* git lfs
  * replaces files with text pointers and stores the file contents on a remote server
  * e.g. large files such as audio samples, videos, datasets, and graphic
  * also huge data sets in data science

---

# Links
* Official Website: https://git-scm.com

---

# Sources

* Git Logo by [Jason Long](https://twitter.com/jasonlong) is licensed under the [Creative Commons Attribution 3.0 Unported License](https://creativecommons.org/licenses/by/3.0/).
* [Stack Overflow Developer Survey Results 2017](https://insights.stackoverflow.com/survey/2017#overview)
* [Tips and Tricks: Gotta Git Them All - GitHub Universe 2016](https://www.youtube.com/watch?v=LsxDxL4PYik)
* [Git Aliases of the Gods! - Git Merge 2017](https://www.youtube.com/watch?v=3IIaOj1Lhb0)
* [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)