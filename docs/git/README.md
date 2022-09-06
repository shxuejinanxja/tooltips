# Git and GitHub

## Git

> How to include other git repo in current repo?

[git submodule](https://git-scm.com/book/en/v2/Git-Tools-Submodules)

- Add submodule to current repo `git submodule add https://github.com/chaconinc/DbConnector`
- commit the change to current repo
- clone a project with submodule `git clone --recurse-submodules https://github.com/chaconinc/MainProject`
- update the submodule `git submodule update --remote`

## github

[github](./github.md)

[github actions](./github-actions.md)

## git command

- compare diff between main and linux branch `git diff main..linux`
