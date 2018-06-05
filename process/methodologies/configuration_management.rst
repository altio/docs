Software Configuration Management and Versioning
================================================

Software Configuration Management (SCM)
---------------------------------------

Software Configuration Management is the process umbrella under which versioning and version control fall.
Developers are generally quick to care about the version of the software that is being published and how
cumbersome the version control software is to use without consideration of the nuanced reasons why those
choices have been made. The goal of this section is to provide both preferences and rationales for a given
approach.  That said, the requirements must first be defined.  While this list will surely change in time,
at this juncture we desire a comprehensive approach to versioning that will describe:

1. Finished software made available to customers or the public (e.g. releases)
2. Software made available to contributors (e.g. builds)
3. Both complete applications and components (e.g. libraries)
4. APIs within an application or component
5. Artifacts yielded by various automated build processes.

Using as many modern paradigms as possible, consider a fully automated and complex software system which:

1. Forks a repo, modifies the source for custom needs, and attaches a build process to the fork which builds,
tests, and delivers software components for each of the following:

  OS package source, compiled and packaged into rpm, deb, exe, published to repo or file storage
  Python package made into a wheel and published to internal PyPI repo
  C++ library compiled and built into a dynamic library

2. Maintains several source components with independent versions, for instance:

  A core blogging application that has auth, users, blogs, posts, and media, and exposes a versioned API.
  A web application that extends the core app with custom backend APIs and a frontend single-page app.
  A mobile application that extends the core app.
  Configuration manager runs and yields output files stored in file storage
  Build and coverage reports generated and saved to file storage

3. Leverages components and project source code to yield releases of
development and production containers.


Release Versioning
------------------

*Preference: Semantic Versioning*

Versioning is surprisingly complicated and particular by a team and its needs.  At a high
level, `semantic versioning <https://semver.org>`_ lays out a few rules:

  Given a version number MAJOR.MINOR.PATCH, increment the:

  MAJOR version when you make incompatible API changes,
  MINOR version when you add functionality in a backwards-compatible manner, and
  PATCH version when you make backwards-compatible bug fixes.
  Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

Internal Versioning
-------------------

Extend semantic versions with build numbers or commit hashes.

API Versioning
--------------

* Preference: v1, v2, ... *

These are technically coupled to external versions, so the need to support minor versions is probably excessive.

Artifact Versioning
-------------------

There are (at least) three types of artifacts that ought to be considered.

1. An artifact that is usable by multiple projects or products.  These
   probably ought to be managed in their own build pipelines and under
   their own semantic version.  Then the encapsulating project pins it by
   that external version.  For instance, if you hand-roll a python library
   you would version and build it externally and then pin it in a Pipfile.
2. If the artifact is tied to one or more files changing (as a few, not
   the entire repo, the artifact version can safely be tied to a hash of
   the source files.  An example here might be if you have a production
   server get built in a three stages: OS requirements, python requirements,
   and finally a copy of collected static assets and source code.  The first
   of these can be skipped if Dockerfile is unchanged (specified the OS reqs),
   the second can be skipped if the Dockerfile and Pipfile.lock are unchanged
   (specified the python reqs).
3. Finally, a perfectly acceptable and appropriate approach for the build
   pipeline is to version artifacts by commit hash.  This ensures that there
   is a 1-1 relationship of successful build to source code, allowing team
   members to pull artifacts down for testings and particular commits to be
   promoted to release candidates and ultimately releases.  A common example
   here might be a backend or complete webapp that needs to be re-built on
   each commit to master to ensure current source and static files.
