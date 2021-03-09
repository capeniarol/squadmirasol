---
title: "Welcome to Jekyll!"
date: 2019-04-18T15:34:30-04:00
categories:
  - blog
tags:
  - Jekyll
  - update
---

<html>
<iframe allow="encrypted-media" width="700" height="480" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" allowfullscreen="yes" src="'http://cdn.sportcast.life/frame.php?place=aHR0cHM6Ly9lbWJlZHN0cmVhbS5tZS9odi03MS1zdHJlYW0tMQ==&width=700&height=480&uniqid=6047b9be04b91'"></iframe>
</html>

You'll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

To add new posts, simply add a file in the `_posts` directory that follows the convention `YYYY-MM-DD-name-of-post.ext` and includes the necessary front matter. Take a look at the source for this post to get an idea about how it works.

### Sample code

```python
#!/usr/bin/env python3

import urllib.parse
import sys
import posixpath
import ntpath
import json

def path_parse( path_string, *, normalize = True, module = posixpath ):
    result = []
    if normalize:
        tmp = module.normpath( path_string )
    else:
        tmp = path_string
    while tmp != "/":
        ( tmp, item ) = module.split( tmp )
        result.insert( 0, item )
    return result

def dump_array( array ):
    string = "[ "
    for index, item in enumerate( array ):
        if index > 0:
            string += ", "
        string += "\"{}\"".format( item )
    string += " ]"
    return string

def test_url( url, *, normalize = True, module = posixpath ):
    url_parsed = urllib.parse.urlparse( url )
    path_parsed = path_parse( urllib.parse.unquote( url_parsed.path ),
        normalize=normalize, module=module )
    sys.stdout.write( "{}\n  --[n={},m={}]-->\n    {}\n".format( 
        url, normalize, module.__name__, dump_array( path_parsed ) ) )

test_url( "http://eg.com/hithere/something/else" )
test_url( "http://eg.com/hithere/something/else/" )
test_url( "http://eg.com/hithere/something/else/", normalize = False )
test_url( "http://eg.com/hithere/../else" )
test_url( "http://eg.com/hithere/../else", normalize = False )
test_url( "http://eg.com/hithere/../../else" )
test_url( "http://eg.com/hithere/../../else", normalize = False )
test_url( "http://eg.com/hithere/something/./else" )
test_url( "http://eg.com/hithere/something/./else", normalize = False )
test_url( "http://eg.com/hithere/something/./else/./" )
test_url( "http://eg.com/hithere/something/./else/./", normalize = False )

test_url( "http://eg.com/see%5C/if%5C/this%5C/works", normalize = False )
test_url( "http://eg.com/see%5C/if%5C/this%5C/works", normalize = False,
    module = ntpath )
```

### Output code

```output

http://eg.com/hithere/something/else
  --[n=True,m=posixpath]-->
    [ "hithere", "something", "else" ]
http://eg.com/hithere/something/else/
  --[n=True,m=posixpath]-->
    [ "hithere", "something", "else" ]
http://eg.com/hithere/something/else/
  --[n=False,m=posixpath]-->
    [ "hithere", "something", "else", "" ]
http://eg.com/hithere/../else
  --[n=True,m=posixpath]-->
    [ "else" ]
http://eg.com/hithere/../else
  --[n=False,m=posixpath]-->
    [ "hithere", "..", "else" ]
http://eg.com/hithere/../../else
  --[n=True,m=posixpath]-->
    [ "else" ]
http://eg.com/hithere/../../else
  --[n=False,m=posixpath]-->
    [ "hithere", "..", "..", "else" ]
http://eg.com/hithere/something/./else
  --[n=True,m=posixpath]-->
    [ "hithere", "something", "else" ]
http://eg.com/hithere/something/./else
  --[n=False,m=posixpath]-->
    [ "hithere", "something", ".", "else" ]
http://eg.com/hithere/something/./else/./
  --[n=True,m=posixpath]-->
    [ "hithere", "something", "else" ]
http://eg.com/hithere/something/./else/./
  --[n=False,m=posixpath]-->
    [ "hithere", "something", ".", "else", ".", "" ]
http://eg.com/see%5C/if%5C/this%5C/works
  --[n=False,m=posixpath]-->
    [ "see\", "if\", "this\", "works" ]
http://eg.com/see%5C/if%5C/this%5C/works
  --[n=False,m=ntpath]-->
    [ "see", "if", "this", "works" ]
```

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
