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

class: center, middle

# The bigger picure

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