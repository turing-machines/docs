# blog

## GitHub blog load

```bash
git clone git@github.com:kubedge/blog.git
git submodule add -b master git@github.com:kubedge/kubedge.github.io.git public
git submodule add git@github.com:jpescador/hugo-future-imperfect.git themes/hugo-future-imperfect
git submodule add git@github.com:Vimux/Mainroad.git themes/mainroad/
```

or 

```bash
git clone --recurse-submodules git@github.com:kubedge/blog.git
```

## GerritHub blog load

```bash
git clone ssh://GITHUBID@review.gerrithub.io:29418/kubedge/blog && scp -p -P 29418 GITHUBID@review.gerrithub.io:hooks/commit-msg blog/.git/hooks/
git rm -fr themes/mainroad/
git rm -fr themes/hugo-future-imperfect/
git rm -fr public/
git submodule add https://github.com/jpescador/hugo-future-imperfect themes/hugo-future-imperfect
git submodule add https://github.com/vimux/mainroad themes/mainroad
git submodule add -b master git@github.com:kubedge/kubedge.github.io.git public
```

## Reync GerritHub and GitHub

To resync gerrit and github

```bash
git clone ssh://GITHUBID@review.gerrithub.io:29418/kubedge/blog && scp -p -P 29418 GITHUBID@review.gerrithub.io:hooks/commit-msg blog/.git/hooks/
cd blog
git push -f https://GITHUBID@github.com/kubedge/blog
```
