
> Web App

```zsh
# ggpullall
git checkout master && git pull --rebase && git checkout develop && git pull --rebase

git flow hotfix start {{ version + 0.0.1 }}

# if the branch is from another one, cherry pick in git graph

# check version in `package.json` and `meta.json` and bump the version (0.0.1)

git add .
git commit -m "build: version bump"

git push upstream
# wait for others to review
# after merged

git flow hotfix finish {{ version + 0.0.1 }}

## ggpushall
git push origin master && git push origin develop && git push --tags

git checkout master

make beta
make production
```