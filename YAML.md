Quickref Series @ Planet Jekyll

[Jekyll](https://github.com/planetjekyll/quickrefs/blob/master/JEKYLL.md) •
[Octopress](https://github.com/planetjekyll/quickrefs/blob/master/OCTOPRESS.md)  •
[GitHub Pages](https://github.com/planetjekyll/quickrefs/blob/master/GITHUB.md) •
[YAML (for Data Files)](https://github.com/planetjekyll/quickrefs/blob/master/YAML.md) •
[WordPress](https://github.com/planetjekyll/quickrefs/blob/master/WORDPRESS.md)


# YAML Quick Reference (Cheat Sheet) for Jekyll Data Files, Front Matter and Collections 

_YAML Ain't Markup Language - a human friendly data serialization standard for all programming languages_


## Table of Contents

- Data File Examples
    - [List of Key/Value Records e.g. books.yml](#list-of-keyvalue-records)
    - [Nested List of Key/Value Records e.g. nav.yml](#nested-list-of-keyvalue-records)
    - [Hash (Dictionary) of Key/Value Records e.g. authors.yml](#hash-dictionary-of-keyvalue-records)
    - [Multi-File List of Key/Value Records e.g. orgs/jekyll.yml,octopress.yml](#)
- Front Matter Examples
    - [List of Key/Value Records e.g. portfolio.html](#)
    - [Multi-File List of Key/Value Records w/ Collections e.g. _albums/josquin.html,hayden.html](#)
- More
    - [Multi-Line Strings](#multi-line-strings)
    - [Inline Style a.k.a. JSON-Style](#)
    - [Literal Keys](#literal-keys)
    - [More Gotchas](#more-gotchas)
        - No Tabs (\t) for Indentation - Use Spaces, Period
        - Predefined Boolean and No Value Constants - True/False, Yes/No, On/Off, ~/Null
    - [Tools](#tools)
    - [References](#references)



## What's human friendly?

#### Let's you use comments or blank lines or spaces


Example - `themes.yml`:

``` yaml
#########################################
# Dr Jekyll's Themes - Add Your Theme!

- title:     Bootstrap
  github:    drjekyllthemes/jekyll-bootstrap-theme
  branch:    gh-pages
  author:    Edward Hyde
  thumbnail: drjekyll-bootstrap.png
  license:   Public Domain

# Another (Possible) Formatting Style

- title     : Classics Book     # Todo: Rename to World Classics - Why? Why Not?
  github    : drjekyllthemes/jekyll-book-theme
  branch    : gh-pages
  author    : Edward Hyde
  thumbnail : drjekyll-book.png
  license   : Public Domain  
```

is the same as:

``` yaml
- title: Bootstrap
  github: drjekyllthemes/jekyll-bootstrap-theme
  branch: gh-pages
  author: Edward Hyde
  thumbnail: drjekyll-bootstrap.png
  license: Public Domain
- title: Classics Book
  github: drjekyllthemes/jekyll-book-theme
  branch: gh-pages
  author: Edward Hyde
  thumbnail: drjekyll-book.png
  license: Public Domain
```

Note: The colon (`:`) key/value separator MUST (only) be followed by a space, thus,
you can use `title  :  Classics Books` and so on. 

Note: The number sign / hash (`#`) used for inline end-of-line comments MUST
have both a leading and trailing space e.g. `some text here  # comment starts here`,
otherwise the number sign / hash is just part of the string
e.g. `Jekyll - The #1 Static Site Generator` works as expected.



#### Let's you use strings or keys without (requiring) quotes

``` yaml
title:   Bootstrap
github:  drjekyllthemes/jekyll-bootstrap-theme
author:  Edward Hyde
```

is the same as:

``` yaml
"title": "Bootstrap"
"github": "drjekyllthemes/jekyll-bootstrap-theme"
"author": "Edward Hyde"
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



## Data File Examples

List of Key/Value Records  •
Nested List of Key/Value Records •
Hash (Dictionary) of Key/Value Records •
Multi-File List of Key/Value Records


Note: You can browse the examples live in action at the Sandbox Example Site @ Planet Jekyll.
See the [start page](http://planetjekyll.github.io/sandbox)
or the [sandbox site sources](https://github.com/planetjekyll/sandbox).


### List of Key/Value Records

Book List Example -`books.yml`:

``` yaml
- title:     "Text Processing with Ruby: Extract Value from the Data That Surrounds You"
  author:    Rob Miller
  cover:     2015/text-processing-with-ruby.jpg
  publisher: Pragmatic Bookshelf
  date:      Nov 2015
  pages:     200 pages (est)
  book_url:  https://pragprog.com/book/rmtpruby/text-processing-with-ruby

- title:     "Learn Ruby the Hard Way"
  subtitle:  A Simple and Idiomatic Intro to the Imaginative World Of Computational Thinking with Code
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



### Nested List of Key/Value Records

Navigation Menu Example -`nav.yml`:

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
    {% if nav.subcategories %}
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


### Hash (Dictionary) of Key/Value Records

Author List Example - `authors.yml`:

``` yaml
henry:
  name:    Dr Henry Jekyll
  twitter: henryjekyll

edward:
  name:    Edward Hyde
  twitter: edhyde
```


Use like:

Example 1) Lookup author info in a post

``` html
---
title:  A Strange Case
author: henry
---

{% assign author = site.data.authors[ page.author ] %}

<a href="http://twitter.com/{{ author.twitter }}">
   {{ author.name }}
</a>
```


### Multi-File List of Key/Value Records

Note: You can place data files in (sub)folders
of the `_data` folder.
Each folder level will get added to the variable's namespace e.g. `site.data.orgs`.


Org Example #1 - `orgs/jekyll.yml`:

``` yaml
name:   Jekyll
github: jekyll

members:
- name:   Parker Moore
  github: parkr
- name:   Jordon Bedwell
  github: envygeeks
```

Org Example #2 - `orgs/octopress.yml`:

``` yaml
name:   Octopress
github: octopress

members:
- name:   Brandon Mathis
  github: imathis
```

Use like:

``` html
<ul>
{% for org_hash in site.data.orgs %}
{% assign org = org_hash[1] %}
  <li>
    <a href="https://github.com/{{ org.username }}">
      {{ org.name }}
    </a>
    ({{ org.members | size }} members)
  </li>
{% endfor %}
</ul>
```



## Front Matter Examples

List of Key/Value Records  •
Multi-File List of Key/Value Records w/ Collections


### List of Key/Value Records 

Portfolio Example, Part 1/2 (Front Matter) - `portfolio.html`:

``` yaml
---
layout: default
title:  Histories, Tragedies and Comedies
portfolio:
- title:     Richard II
  category:  History
  cover:     richard-ii.jpg
- title:     Henry VI, Part 1
  category:  History
  cover:     henry-vi-1.png
- title:     Romeo and Juliet
  category:  Tragedy
  cover:     romeo-n-juliet.jpg
- title:     Hamlet
  category:  Tragedy
  cover:     hamlet.gif
- title:     Antony and Cleopatra
  category:  Tragedy
  cover:     antony-n-cleopatra.jpg
- title:     All's Well That Ends Well 
  author:    Comedy
  cover:     alls-well-that-ends-well.jpg
- title:     A Midsummer Night's Dream 
  author:    Comedy
  cover:     a-midsummer-nights-dream.jpg
---
``` 

Use like:

Portfolio Example, Part 2/2 (Continued) - `portfolio.html`:

``` html
<h1>{{ page.title }}

<div class='porfolio'>
{% for work in page.portfolio %}

  <div class='work'>
    <img src="{{site.url}}/i/portfolio/{{work.cover}}">
    {{ work.title }} // {{ work.category }}
  </div>

{% endfor %}
</div>
```

Note: The portfolio is defined inside the page (in the front matter), thus,
use `page.portfolio` instead of ~~`site.data.portfolio`~~ to reference (e.g. loop over) the list.



### Multi-File List of Key/Value Records w/ Collections


Albums Example #1 - `_albums/josquin.html`:

``` yaml
---
title: "Josquin: Missa De beata virgine and Missa Ave maris stella"
artist: "The Tallis Scholars"
director: "Peter Phillips"
works:
- title: "Missa De beata virgine"
  composer: "Josquin des Prez"
  tracks:
  - title: "Kyrie"
    duration: "4:25"
  - title: "Gloria"
    duration: "9:53"
  - title: "Credo"
    duration: "9:09"
  - title: "Sanctus & Benedictus"
    duration: "7:47"
  - title: "Agnus Dei I, II & III"
    duration: "6:49"
---
```

Albums Example #2 - `_albums/hayden.html`:

``` yaml
---
title: "Hayden: ??"
artist: "??"
director: "??"
works:
- title: "??"
  composer: "??"
  tracks:
  - title: "??"
    duration: "4:25"
  - title: "??"
    duration: "9:53"
---
```

Use like:

Example Catalog - `catalog.html`:

``` html
---
layout: default
title:  Album Catalog
---
{% for album in site.albums %}
  <h2>{{ album.title }}</h2>
  Performed by {{ album.artist }}{% if album.director %}, directed by {{ album.director }}{% endif %}
  {% for work in album.works %}
    <h3>{{ work.title }}</h3>
    <p>Composed by {{ work.composer }}</p>
    <ul>
    {% for track in work.tracks %}
      <li>{{ track.title }} ({{ track.duration }})</li>
    {% endfor %}
    </ul>
  {% endfor %}
{% endfor %}
```

Note: Using collections you can access **ALL** front matters from all files
from anywhere (not just inside a collection page) using the collection name e.g. `site.albums`.


## More


### Multi-Line Strings

#### Unfolded (e.g. Keep Newlines) - `|`

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



#### Folded (e.g. Strip Newlines) - `>`

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

### Inline Style a.k.a. JSON-Style

Note: As an alternative syntax you can use the inline style for lists (e.g. JSON arrays)
and hashes/dictionaries (e.g. JSON objects). Example:

``` yaml
[{ "title":     "Bootstrap",
   "github":    "drjekyllthemes/jekyll-bootstrap-theme",
   "author":    "Edward Hyde",
   "thumbnail": "drjekyll-bootstrap.png" },
 { "title":     "Classics Book",
   "github":    "drjekyllthemes/jekyll-book-theme",
   "author":    "Edward Hyde",
   "thumbnail": "drjekyll-book.png" }]
```

is the same as:

``` yaml
[
 { "title": Bootstrap", "github": "drjekyllthemes/jekyll-bootstrap-theme", "author": "Edward Hyde", "thumbnail": "drjekyll-bootstrap.png" },
 { "title": "Classics Book", "github": "drjekyllthemes/jekyll-book-theme", "author": "Edward Hyde", "thumbnail": "drjekyll-book.png" }
]
```

or the same as:

``` yaml
- title     : Bootstrap
  github    : drjekyllthemes/jekyll-bootstrap-theme
  author    : Edward Hyde
  thumbnail : drjekyll-bootstrap.png
- title     : Classics Book
  github    : drjekyllthemes/jekyll-book-theme
  author    : Edward Hyde
  thumbnail : drjekyll-book.png
```

Yes, the JavaScript Object Notation (JSON) is a just another (welcome and working)
formatting style for datafiles. 



### Literal Keys

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

**No Tabs (\t) for Indentation - Use Spaces, Period**

Note: Always use spaces for indentation, period. 
Make sure no tabs (`\t`) have somehow ended up in your datafile leading to
unexpected results.



**Predefined Boolean 'n' No Value Constants - True/False, Yes/No, On/Off, ~/Null**

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
recommend: Yes       # note: will become => true (boolean)
```

make sure you use a quoted version e.g.:

``` yaml
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
- [YAML Tutorial @ Spacelift](https://spacelift.io/blog/yaml)



## Meta

**License** 

The YAML Quick Reference is dedicated to the public domain. 
Use it as you please with no restrictions whatsoever.

**Questions? Comments?**

Post them to the [wwwmake forum](http://groups.google.com/group/wwwmake). Thanks!

