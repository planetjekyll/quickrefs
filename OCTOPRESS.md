# Octopress Quick Reference (Cheat Sheet)


## Table of Contents

- Octopress Commands (`new`, `new page`, `deploy`, ...)

## Octopress Commands

```
$ octopress --help

octopress 3.0.0 -- Octopress is an obsessively designed toolkit for Jekyll blogging.

Usage:

  octopress <subcommand> [options]

Options:
  -h, --help         Show this message
  -v, --version      Print the name and version
  -t, --trace        Show the full backtrace when an error occurs

Subcommands:
  new         Creates a new site with Jekyll and Octopress scaffolding at the specified path.
  docs        Launch local server with docs for Octopress v3.0.0.rc.31 and Octopress plugins.
  init        Add Octopress's default scaffolding to your site.
  publish     Convert a draft to a normal published post.
  unpublish   Convert a post to a draft. Command accepts path to post or search string.
  isolate     Move all posts not matching selected post to _posts/_exile. Command accepts path to post or search string.
  integrate   Reintegrate posts from _posts/_exile.
  deploy      Deploy your Octopress site.
```

## `new` Command

```
$ octopress new --help

octopress new -- Creates a new site with Jekyll and Octopress scaffolding at the specified path.

Usage:

  octopress new <PATH>

Options:
  -f, --force        Force creation even if path already exists.
  -b, --blank        Creates scaffolding but with empty files.
  -h, --help         Show this message

Subcommands:
  page    Add a new page to your Jekyll site.
  post    Add a new post to your Jekyll site.
  draft   Add a new draft post to your Jekyll site.
```

## `new post` Command

```
$ octopress new post --help

octopress new post -- Add a new post to your Jekyll site.

Usage:

  octopress new post <TITLE> [options]

Options:
  -d,  --date DATE    Use 'now' or a String that is parseable by Time#parse.
  -tm, --template PATH  New post from a template.
  -l,  --lang LANGUAGE  Set a post language (e.g. en, it) for multi-language sites.
  -f,  --force        Overwrite file if it already exists
  -s,  --slug SLUG    Use this slug in filename instead of sluggified post title.
  -d,  --dir DIR      Create post at _posts/DIR/.
  -c,  --config <CONFIG_FILE>[,CONFIG_FILE2,...]  Custom Jekyll configuration file
  -h,  --help         Show this message
```

## `deploy` Command

```
$ octopress deploy --help

octopress deploy 1.0.4 -- Deploy your Octopress site.

Usage:

  octopress deploy [options]

Options:
      --config FILE  The path to your config file (default: _deploy.yml)
  -h, --help         Show this message

Subcommands:
  pull         Pull down the published copy of your site into DIR
  init         Create a configuration file for a deployment method (git, rsync, s3).
  add-bucket   Add a new S3 bucket and configure it for static websites. Name defaults to bucket_name in config file
```

## Octopress Quickstart

```
  $ octopress new my-site
     # => New jekyll site installed in ~/my-site 
     #    Added Octopress scaffold:
     #     + _templates/
     #     +   draft
     #     +   page
     #     +   post
  $ cd my-site
  $ jekyll build
     # => Configuration file: ~/_config.yml
     #                Source: ~/my-site
     #           Destination: ~/my-site/_site
     #          Generating... done.
  $ jekyll serve
     # =>     Server address: http://127.0.0.1:4000/
     #      Server running... press ctrl-c to stop.   
```


## Meta

**License** 

The Octopress Quickreference (Cheat Sheet) is dedicated to the public domain. 
Use it as you please with no restrictions whatsoever.

**Questions? Comments?**

Post them to the [jekyll talk forum](https://talk.jekyllrb.com). Thanks!
