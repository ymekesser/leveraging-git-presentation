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
  * Digging in the past <br>
    `git log`
  * Preparing <br>
    `git status`, `git add`
  * Rewriting History <br>
    `git commit --amend`, `git rebase`
4. The bigger picture
  * GitFlow
  * rebase vs merge
5. Further pointers
  * Git LFS

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
  * (but it is not limited to software development)

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
## Setting up the stage

Git knows three areas where your changes can be:

.areas[![Centered image](img/areas.png)]

.addendum[The stash can be viewed as a fourth area] 

---

# Preparing your commits
## xxx

```
$ git commit -a -m "Added some stuff"
```
If you want to keep it simple this time. .addendum[Note: This does not add untracked files!]

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
$ git <since>..<until>
```
Allows you to show commits in a range between two _commit references_.
This is especially great to compare branches:

```
$ git master..feature
```
Shows you the commits which are in the feature branch, but not in the master branch. .addendum[If you switch it to feature..master you will see what commits are missing from feature]

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
    | grep -v " ${1-master}$" 
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
## Aliases for recurring tasks

```
[alias]
cma = !git add -A; commit -m
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
## The history is written by winners

---

class: center, middle

# The bigger picure

---

# GitFlow
## A way to make modern software development manageable

---

class: center, middle

# Further pointers

---

# Links
* Official Website: https://git-scm.com

---

# Sources

* Git Logo by [Jason Long](https://twitter.com/jasonlong) is licensed under the [Creative Commons Attribution 3.0 Unported License](https://creativecommons.org/licenses/by/3.0/).
* [Stack Overflow Developer Survey Results 2017](https://insights.stackoverflow.com/survey/2017#overview)
* [Tips and Tricks: Gotta Git Them All - GitHub Universe 2016](https://www.youtube.com/watch?v=LsxDxL4PYik)
* [Git Aliases of the Gods! - Git Merge 2017](https://www.youtube.com/watch?v=3IIaOj1Lhb0)