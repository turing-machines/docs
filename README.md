# blog

## Loading the blog and submodules

```bash
git clone git@github.com:kubedge/blog.git
git submodule add -b master git@github.com:kubedge/kubedge.github.io.git public
git submodule add git@github.com:jpescador/hugo-future-imperfect.git themes/hugo-future-imperfect
git submodule add git@github.com:Vimux/Mainroad.git themes/mainroad/
```

```bash
git clone --recurse-submodules git@github.com:kubedge/blog.git
```

```bash
git rm -fr themes/mainroad/
git rm -fr themes/hugo-future-imperfect/
git rm -fr public/
git submodule add https://github.com/jpescador/hugo-future-imperfect themes/hugo-future-imperfect
git submodule add https://github.com/vimux/mainroad themes/mainroad
git submodule add -b master git@github.com:kubedge/kubedge.github.io.git public
```
