git checkout -b latest master
git flow init
Branch name for production releases: [master] latest
Branch name for "next release" development: [master] master
Defaults for: feature, release, hotfix, support
Version tag prefix? [] v

cat .git/config

[gitflow "branch"]
	master = latest
	develop = master
[gitflow "prefix"]
	feature = feature/
	release = release/
	hotfix = hotfix/
	support = support/
	versiontag = v


git flow feature start <name> [<base>]
git checkout master
git checkout -b feature/<name> [<base>]

git flow feature finish <name<
on branch: git flow feature finish
git checkout master
git merge feature/<name>
git branch -d feature/<name>


git flow release start <version>
git checkout master
git checkout -b release/<version> master


git flow release finish <version>

git checkout release/<version>
git tag v<version>
git checkout master
git merge release/<version>
git checkout latest
git merge --no-ff release/<version>
git branch -d release/<version>


after bumping minor or major version, if still supporting verion line:

git flow support start <name> <base>
e.g.
git flow support start 1.0.x v1.0.0
git flow support start 1.x v1.0[.0]

never use release on other than latest
shhhhhhhhhhhhhhould basically never use base for hotfix... dangerous
probably want to release on support branch, then merge into all until to latest, then hotfix
NEVER use a base of a tag for hotfix... should be default of latest, or a support branch



git flow hotfix start <version> [<base>]
git checkout latest
git checkout -b hotfix/<version> [<base>]


git flow hotfix finish <version>

git checkout hotfix/<version>
git tag v<version>
git checkout master
git merge hotfix/<version>
git checkout latest
git merge --no-ff hotfix/<version>
git branch -d hotfix/<version>




alternatively, for multi0version bugfix:

git flow feature start 1.0.1 support/1.0.x
git flow release finish --keep 1.0.1


git flow hotfix start <version> support/<old-version>
git flow hotfix finish --keep <version>

skips delete, can back-merge into other versions?
