
<!--
  todo:
    add some notes about quotes
     e.g. ' in unquotes strings
     how to use " - possible? e.g. use 'Jack "Notron" Atom'
  add more notes about boolean
   check for values ??  - are boolean or string?
  -->


Quickref Series @ Planet Jekyll

[Jekyll](https://github.com/planetjekyll/quickrefs/blob/master/JEKYLL.md) • 
[Octopress](https://github.com/planetjekyll/quickrefs/blob/master/OCTOPRESS.md)  • 
[GitHub Pages](https://github.com/planetjekyll/quickrefs/blob/master/GITHUB.md) • 
[YAML (for Datafiles)](https://github.com/planetjekyll/quickrefs/blob/master/YAML.md) •
[WordPress](https://github.com/planetjekyll/quickrefs/blob/master/WORDPRESS.md)


# YAML Quick Reference (Cheat Sheet) for Jekyll Datafiles

_YAML Ain't Markup Language - a human friendly data serialization standard for all programming languages_


## Table of Contents

- [List of Key/Value Records](#list-of-keyvalue-records)
- [Nested List of Key/Value Records](#nested-list-of-keyvalue-records)
- [Hash (Dictionary) of Key/Value Records](#hash-dictionary-of-keyvalue-records)
- [Multi-Line Strings](#multi-line-strings)
- [Literal Keys](#literal-keys)
- [More Gotschas](#more-gotschas)
- [References](#references)


## What's human friendly?

#### Let's you use comments or blank lines or spaces


Example: `themes.yml`

``` yaml
#########################################
# Dr. Jekyll's Themes - Add Your Theme!

- title:     Bootstrap
  github:    drjekyllthemes/jekyll-bootstrap-theme
  branch:    gh-pages
  author:    Dr. Henry Jekyll et al
  thumbnail: drjekyll-bootstrap.png
  license:   Public Domain

# Another (Possible) Formatting Style

- title    : Classics Book     # Todo: Rename to World Classics - Why? Why Not?
  github   : drjekyllthemes/jekyll-book-theme
  branch   : gh-pages
  author   : Dr. Henry Jekyll et al
  thumbnail: drjekyll-book.png
  license  : Public Domain  
```

is the same as:

``` yaml
- title: Bootstrap
  github: drjekyllthemes/jekyll-bootstrap-theme
  branch: gh-pages
  author: Dr. Henry Jekyll et al
  thumbnail: drjekyll-bootstrap.png
  license: Public Domain
- title: Classics Book
  github: drjekyllthemes/jekyll-book-theme
  branch: gh-pages
  author: Dr. Henry Jekyll et al
  thumbnail: drjekyll-book.png
  license: Public Domain
```


#### Let's you use strings or keys without (requiring) quotes

``` yaml
title:   Bootstrap
github:  drjekyllthemes/jekyll-bootstrap-theme
author:  Dr. Henry Jekyll et al
```

is the same as:

``` yaml
"title": "Bootstrap"
"github": "drjekyllthemes/jekyll-bootstrap-theme"
"author": "Dr. Henry Jekyll et al"
```


**Gotchas**

When to use quotes for your strings?

If your string includes a colon (`:`) you MUST quote your string. Otherwise, the colon is interpreted as a key/value separator (e.g. _key: value_). Example:

``` yaml
title: "Text Processing with Ruby: Extract Value from the Data That Surrounds You"
title: "Sinatra: Up and Running - Ruby for the Web, Simply"
title: "Using JRuby: Bringing Ruby to Java"
```

Note: You can quote your strings using double quotes (`""`) e.g. "Using JRuby: Bringing Ruby to Java" 
or single quotes(`''`) e.g. 'Using JRuby: Bringing Ruby to Java'.



<!--
commans work: e.g.

author: Charles O Nutter, Thomas Enebo, Nick Sieger, Ola Bini, Ian Dees

todo: Double check.

If you string includes a comma (`,`) you MUST quote your string. Otherwise, the comma is interpreted as a value list seperator (e.g. _key: value, value, value_). Example:

``` yaml
title: "Sinatra: Up and Running - Ruby for the Web, Simply"
title: ""
```
-->


## List of Key/Value Records

Book List Example (e.g. `books.yml`):

``` yaml
- title:     "Text Processing with Ruby: Extract Value from the Data That Surrounds You"
  author:    Rob Miller
  cover:     2015/text-processing-with-ruby.jpg
  publisher: Pragmatic Bookshelf
  date:      Nov 2015
  pages:     200 pages (est)
  book_url:  https://pragprog.com/book/rmtpruby/text-processing-with-ruby

- title:     "Learn Ruby the Hard Way"
  subtitle:  A Simple and Idiomatic Introduction to the Imaginative World Of Computational Thinking with Code
  edition:   3rd Edition
  author:    Zed Shaw
  cover:     2014/learn-ruby-the-hard-way.jpg
  publisher: Addison-Wesley Professional (Zed Shaw's Hard Way Series)
  date:      Dec 2014
  pages:     336 pages
  book_url:  http://www.informit.com/store/learn-ruby-the-hard-way

- title:     "Sinatra: Up and Running - Ruby for the Web, Simply"
  author:    Alan Harris, Konstantin Haase
  cover:     2011/sinatra-up-and-running.jpg
  publisher: O'Reilly Media
  date:      Dec 2011
  pages:     122 pages
  book_url:  http://shop.oreilly.com/product/0636920019664.do
```

Use like:

``` html
{% for book in site.data.books %}
  <div>
  <a href="{{ book.book_url }}">
    <img src="{{site.url}}/i/{{book.cover}}">
  </a>
  {{ book.title }}
  {% if book.edition %}
    ({{ book.edition}})
  {% endif %}
  by {{ book.author }};
  {{ book.publisher }}, {{ book.date }}; {{ book.pages}}
  </div>
{% endfor %}
```



## Nested List of Key/Value Records

Navigation Menu Example: e.g. `nav.yml`

``` yaml
- title: Home
  href:  /

- title: Learn
  href:  /learning-resources/
  subcategories:
  - title: Learning topic one
    href:  /learn1/
  - title: Learning topic two
    href:  /learn2/
  - title: Learning topic three
    href:  /learn3/

- title: Tools
  subcategories:
  - title: Tools one
    href:  /tools1/
  - title: Tools two
    href:  /tools2/

- title: About Us
  href:  /about-us/
```


Use like:

``` html
<nav>
  <ul>
    {% for nav in site.data.nav %}
      {% if nav.subcategories != null %}
        <li>
          <a href="{{ site.url }}{{ nav.href }}">{{ nav.title }} ▼</a>
          <ul>
          {% for subcategory in nav.subcategories %}
            <li><a href="{{ site.url }}{{ subcategory.href }}">{{ subcategory.title }}</a></li>
          {% endfor %}
          </ul>
        </li>
      {% else %} 
        <li>
          <a href="{{ site.url }}{{ nav.href }}">{{ nav.title }}</a>
        </li>
      {% endif %}
    {% endfor %}
  </ul>
</nav> 
```


## Hash (Dictionary) of Key/Value Records

Author List Example: e.g. `people.yml`

``` yaml
henry:
  name:    Dr. Henry Jekyll
  twitter: henryjekyll

edward:
  name:    Edward Hyde
  twitter: edhyde
```


Use like:

Example 1) Lookup author info in a post

``` html
---
title:  sample post
author: henry
---

{% assign author = site.data.people[ page.author ] %}
<a href="{{ author.twitter }}">
         {{ author.name }}
</a>
```



## Multi-Line Strings

### Unfolded (e.g. Keep Newlines) - `|`

``` yaml
text: |
   There once was a short man from Ealing
   Who got on a bus to Darjeeling
       It said on the door
       "Please don't spit on the floor"
   So he carefully spat on the ceiling
```

The leading indent (of the first line) and trailing white space gets stripped e.g. becoming:

```
There once was a short man from Ealing\n
Who got on a bus to Darjeeling\n
    It said on the door\n
    "Please don't spit on the floor"\n
So he carefully spat on the ceiling\n
```



### Folded (e.g. Strip Newlines) - `>`

``` yaml
text: >
   Wrapped text
   will be folded
   into a single
   paragraph
   
   Blank lines  denote
   paragraph breaks
```

Folded text converts newlines to spaces
and removes leading whitespaces e.g. becoming:

```
Wrapped text will be folded into a single paragraph\n
\n
Blank lines denote paragraph breaks\n
```



## Literal Keys

Note: You can use upper case letters in your keys (e.g. `Teams`),
add spaces (e.g. `Bundesliga Teams`) and
even start with numbers (e.g. `18 Teams`). Example:

``` yaml
18 Teams:
  - Austria Wien
  - SC Salzburg
  - Sturm Graz
```



## More Gotchas

**No Tabs (\t) for Indentation**

Note: Always use spaces for indentation, period. 
Make sure no tabs (`\t`) have somehow ended up in your datafile leading to
unexpected results.



**Predefined Constants - True/False, Yes/No, On/Off, ~/Null**

Note: The boolean `true` and `false` constants e.g.:

```
true, True, TRUE
y, Y, yes, YES, YES
on, ON, ON
false, False, FALSE
n, N, no, No, NO
off, Off, OFF
```

will become boolean values e.g. `true` or `false`.  If you want end-up with a string e.g.:

``` yaml
survey:
    recommend: Yes      # note: will become => true (boolean)
```

make sure you use a quoted version e.g.:

``` yaml
survey:
    recommend: "Yes"     # note: will become => "Yes" (string)
```


Note: The same holds for the no value null constants e.g.:

``` yaml
~
null, Null, NULL
```

will become => `null` (no value). Note: A key without a value will end-up with a `null` value (and not an empty string, for example). To get an empty string use `""` e.g.:

``` yaml
key1:           # note: value will become => null (no value); same as key1: null  or key1: ~
key2: ""        # note: value will become => "" (string)
```


## Tools

- **YAML Online Linter** (web: [yamllint.com](http://www.yamllint.com)) - paste in your YAML and click "Go" - the linter will tell you if your datafile is valid or not, and print out a nice clean formatted version in UTF-8


## References

**YAML Headquarters**

- YAML (web: [yaml.org](http://yaml.org))
     - [YAML Reference Card](http://yaml.org/refcard.html)

**More**

- [YAML @ Wikipedia](https://en.wikipedia.org/wiki/YAML)



## Meta

**License** 

The YAML Quick Reference is dedicated to the public domain. 
Use it as you please with no restrictions whatsoever.

**Questions? Comments?**

Post them to the [jekyll talk forum](https://talk.jekyllrb.com). Thanks!

