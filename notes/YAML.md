# YAML Notes


todo:

add some notes about quotes
e.g. ' in unquotes strings
how to use " - possible? e.g. use 'Jack "Notron" Atom'

add more notes about boolean
check for values ??  - are boolean or string?



commans work: e.g.

author: Charles O Nutter, Thomas Enebo, Nick Sieger, Ola Bini, Ian Dees

todo: Double check.

If you string includes a comma (`,`) you MUST quote your string. Otherwise, the comma is interpreted as a value list seperator (e.g. _key: value, value, value_). Example:

``` yaml
title: "Sinatra: Up and Running - Ruby for the Web, Simply"
title: ""
```

