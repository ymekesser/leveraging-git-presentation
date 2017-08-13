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
* Build infrastructure

---

# Introduction

```
$ git init
```


```sql
SELECT *
FROM table
WHERE table.col LIKE '%a';
```

* Professional software development relies on source control
* Especially for
  * Big teams
  * Agile development
  * Release Management

* In short: Source control is essential for, but not limited to, multi-developer software projects.

(but it is not limited to software development)

---

class: center, middle

# A bit 'bout git

---

# History
## The dark, centralized ages
(excerpt)

* Concurrent Versions System (CVS), 1990
  * xxxx
* Subversion (SVN), 2000
  * “CVS done right”
* Visual Source Safe (VSS), 2005
  * File locks, occasionally corrupts files
* Team Foundation Server (TFS), 2006
  * SVN but you have to pay for it

---

# History
## The distributed age
(excerpt)

* Bitkeeper, 2000
* **Git**, 2005
* Mercurial, 2005
* Bazaar, 2005

---

# Distributed Source Control

* Obvious benefit: Offline Working
* Improves collaboration
  * Commit changes without disturbing others
  * Branching is inherent
* Performance
  * Operations are local
* Trust
* Release Engineering
* Security


Trust your data
Without having to implicitly trust everybody else
Without having to implicitly trust your hosting
Release Engineering
Trust and Security
No single point of failure
Natural replication of data
Everything is checksumed with a strong hash (relative)
Sha1 is mostly a consistency feature
You can keep your master copy behind 3 firewalls

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

# Links
* Official Website: https://git-scm.com

---

# Sources

* Git Logo by [Jason Long](https://twitter.com/jasonlong) is licensed under the [Creative Commons Attribution 3.0 Unported License](https://creativecommons.org/licenses/by/3.0/). 
