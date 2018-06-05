Version Control System (VCS)
============================

*Preference: Git*

Overview
--------

A Version Control System (VCS) is used to maintain a history of changes to a collection
of information.  It is especially useful when writing software because it allows one to
protect effort that has been committed from being lost due to desructive or additive
edits.  The three most common systems are Git, Mercurial (Hg), and Subversion.

Why not Subversion?
-------------------

Subversion is fine for simple projects with linear workflows, but it does not enable one
to take advantage of the version control system for local development and compels users
to either forego committing often or commit an excessive amount of noise to the central
repository.

Why not Mercurial (Hg)?
-----------------------

Mercurial has many paradigms similar to Git and is easier to use and learn than Git in
certain respects.  That said, there are a few differences which make Git more attractive:
- Re-writing history.  The ability to squash and amend commits lowers the bar to
committing substantially as developers know they can dispose of the intermediate commits
once work is complete.
- Reference log.  Nothing is ever actually deleted in Git (immediately)-- everything
goes into a reference log where it is not garbage collected for 30 days, ensuring that
even if you rebase a branch or delete/squash a commit you can find and recover the
since abandoned commit (see git: reflog).
