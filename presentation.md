name: title
class: center, middle

# Leveraging Git for your development workflow
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

What are the 3 most important tools for software development?

--

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
* Git: A set of commands to manipulate it

---

# Links
* Official Website: https://git-scm.com

---

# Sources

* Git Logo by [Jason Long](https://twitter.com/jasonlong) is licensed under the [Creative Commons Attribution 3.0 Unported License](https://creativecommons.org/licenses/by/3.0/). 
