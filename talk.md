class: center, middle

<img src="img/dirac-bw.jpg" style="height: 200px;"/>
<img src="img/dirac-bw.jpg" style="height: 200px;"/>
<img src="img/dirac-color.jpg" style="height: 200px;"/>
<img src="img/dirac-bw.jpg" style="height: 200px;"/>

# DIRAC goes LGPL

## What it means for developers and users

## Radovan Bast [@\_\_radovan](https://twitter.com/__radovan)

## Text is CC-BY

---

## Outline

- Summary of what happened
- What others can do and cannot do
- Remaining steps
- Changes in our day to day
- Changes in the release process
- Timeline
- Steps we can take once the code is public

---

## Summary of what happened

- 2019: Decided to move to LGPL
- All authors have agreed
- We decided to not clean up Git history


### What it means

- Copyright stays with authors
- Only copyright holders can change the license
- Software license and citations are two different things

---

## What others can do and cannot do

### Anybody can modify the code and redistribute their versions

- This is important because if they cannot redistribute their modifications (as part of a publication),
  they may choose a different code to base their modifications on
- .emph[Open source does not make contributing or maintenance any easier] but it simplifies sharing


### Others cannot modify the license

- DIRAC can be redistributed together with a closed-source code (as a component/library in a larger code)
- However, the DIRAC modifications must be redistributed under same license terms as ours
- Since we allow modifications under LGPL, we cannot be locked out from reusing modifications shared
  by others

---

## Remaining steps

### Done
- Update LICENSE and copyright headers
- Remove "make release", MOD_UNRELEASED, and related

### Left to do
- Create public repo https://gitlab.com/dirac/dirac/ and move `master` and `release-*` into there
- Update README in public and private repos
- Protect `master` and `release-*` on https://gitlab.com/dirac/dirac/
- Remove push protection from https://gitlab.com/dirac/dirac-private/
- Remove `master` and `release-*` from https://gitlab.com/dirac/dirac-private/
- Announce: website, Twitter, mailing list

---

## Changes in our day to day (1/2)

We will now work with more than one remote repository.


### Public repo: https://gitlab.com/dirac/dirac/

- `master` and `release-*` branches
- Anything that is on `master` is meant to become the next release


### Private repo: https://gitlab.com/dirac/dirac-private/

- Nothing is public, you decide when to share
- No `master` branch, no `release-*` branches

---

## Changes in our day to day (2/2)

### Updating your development with upstream changes

- You fetch upstream changes from the public repo

```console
$ git remote add upstream https://gitlab.com/dirac/dirac.git
$ git fetch upstream
$ git checkout myownbranch
$ git merge upstream/master
```


### Contributing your changes upstream

- Push the branch to https://gitlab.com/dirac/dirac.git
- Create merge request towards `master`
- This code will be in the next release (no more code removal in the release process)
- Then delete the branch on https://gitlab.com/dirac/dirac-private/ (or keep it, up to you)

---

## Changes in the release process

### We will still create releases

- Release branches will live on the public repository


### Release process is simpler

- No "make release"
- Easier to test
- Probably also less to do on a release branch since the release code is closer to `master`
- Tarball can be downloaded directly from GitLab


### Problems

- Git submodules/ external code: previously we downloaded and packaged them as part of "make release"
- They would now be fetched as part of configuration or build: risk that external repositories move/disappear
  and that in future we may break the past

---

## Timeline

- Can be done this week
- I recommend to not couple this to the DIRAC22 release
- .emph[But this is up to us to decide]

---

## Steps we can take once the code is public

- **Definitely:** Move Sphinx documentation from own server to [Read the Docs](https://readthedocs.org/)
  - This will allow us to disband the web server we run

- **Suggestion:** Use [GitHub Actions](https://github.com/features/actions) for testing (in addition to [GitLab CI](https://github.com/features/actions)):
  - Linux, macOS, and Windows testing infrastructure for free (within some time limit)
  - At least a subset of tests

- **Maybe:** Move from DokuWiki (own server) to anything Markdown-based
  and serve via GitLab pages (there are many tools which render Markdown to HTML)
  - Easy to set up
  - But less easy to migrate what we have, but doable (thankfully DokuWiki stores data as plain text)
  - We can still have an internal wiki (but better use GitLab wiki close to where the rest is)
