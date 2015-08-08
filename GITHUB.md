Quickref Series @ Planet Jekyll

[Jekyll](https://github.com/planetjekyll/quickrefs/blob/master/JEKYLL.md) • 
[Octopress](https://github.com/planetjekyll/quickrefs/blob/master/OCTOPRESS.md)  • 
[GitHub Pages](https://github.com/planetjekyll/quickrefs/blob/master/GITHUB.md) • 
[YAML (for Datafiles)](https://github.com/planetjekyll/quickrefs/blob/master/YAML.md) •
[WordPress](https://github.com/planetjekyll/quickrefs/blob/master/WORDPRESS.md)


# GitHub Pages Quick Reference (Cheat Sheet)

## Table of Contents

- GitHub Pages (`site.github`, sitemap, ...)


## GitHub Pages

- [`pages.github.com`](https://pages.github.com/)

What Jekyll version and plugins get used?

- [`pages.github.com/versions`](https://pages.github.com/versions), for example (update Jan/2015):

Library               | Version
--------------------- | -----------
jekyll                | 2.4.0
jekyll-coffeescript   | 1.0.1
jekyll-sass-converter | 1.2.0
kramdown              | 1.5.0
liquid                | 2.6.1
pygments.rb           | 0.6.0
jemoji                | 0.4.0
jekyll-mentions       | 0.2.1
jekyll-redirect-from  | 0.6.2
jekyll-sitemap        | 0.6.3
github-pages          | 32
ruby                  | 2.1.1


### `site.github` Variables

```
site.github.contributors    -- A list of your project's contributors (*)
site.github.public_repositories    -- A list of your public repositories (*)
site.github.organization_members   -- A list of your organization's public members (*)
...
```
(*) as returned through the contributors/repositories list/organization members API

Each of these new variables let you use the complete user/repository objects in Jekyll, thus,
you no longer need any client-side JavaScript API calls when showcasing
your projects on GitHub. For more information on displaying metadata
within your Jekyll site, see [Repository metadata on GitHub Pages](https://help.github.com/articles/repository-metadata-on-github-pages/).

(Source: [`jekyll-github-metadata` gem](https://github.com/jekyll/github-metadata))


### Sitemap Plugin

By simply adding the plugin to your site's configuration (`_config.yml`) e.g.

```
gems:
- jekyll-sitemap
```

Jekyll will automatically generate a `sitemaps.org`-compliant sitemap,
making it easier for search engines to index your site's content.

Note: The sitemap plugin is already added (and white-listed) on GitHub Pages.

(Source: [`jekyll-sitemap` gem](https://github.com/jekyll/jekyll-sitemap))

### How-To: Use Single `gh-pages` Branch; Delete `master` Branch

Step 1a) Already has `gh-pages` branch:

```
git checkout gh-pages   
git merge master
git push
```

Step 1b) Create `gh-pages` branch:

````
git checkout -b gh-pages
git merge master
git push origin gh-pages
````

Step 2) Make `gh-pages` branch default branch on GitHub via settings tab

Step 3)  Delete `master` branch on GitHub

```
git push origin :master     # will delete master branch on remote (that is, github)
    
git branch -d master        # will delete master branch in local remote
```

Step 4) Delete local git repo and get a fresh clone from GitHub

```
rm -rf <repo>
git clone <repo-remote-url>
```

That's it.

**Bonus: Check if remote is setup with `git remote show <repo-remote-shorthand>`**

```
$ git remote show origin
# => * remote origin
       Fetch URL: https://github.com/openbeer/book.git
       Push  URL: https://github.com/openbeer/book.git
       HEAD branch: gh-pages
       Remote branch:
          gh-pages tracked
       Local branch configured for 'git pull':
          gh-pages merges with remote gh-pages
       Local ref configured for 'git push':
          gh-pages pushes to gh-pages (up to date)
```



## Meta

**License** 

The GitHub Pages Quick Reference (Cheat Sheet) is dedicated to the public domain. 
Use it as you please with no restrictions whatsoever.

**Questions? Comments?**

Post them to the [wwwmake forum](http://groups.google.com/group/wwwmake). Thanks!
