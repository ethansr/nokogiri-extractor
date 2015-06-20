= nokogiri-extractor

http://github.com/ethansr/nokogiri-extractor

== DESCRIPTION:

Decorates Nokogiri with methods to extract text from nodes and
their attributes. 

This gem handles a very common case in extracting information
from structured documents where the required information is
most easily acquired through the pattern of:

```
extract : document -> selector -> text
```

This has some suprising pitfalls, especially when elements and
their attributes may or may not exist and when a series of
operations are neccesary to coerce the text within an element
into the desired format.

In these cases, we've found it useful to specify an entire path
to the required data which can succeed or fail as a unit, rather
than writing a series of defensive conditional statements.

```ruby
#this

if image = document.at_css('img')
  if alt_text = image[:alt]
    if image.match(/(\d*) kittens/)
      return m[1]
    end
  end
end

#can become

document.extract('img', :alt, /(\d*) kittens/))

```
== SYNOPSIS:

  require 'nokogiri/extractor'
  doc = Nokogiri::XML.parse('<this is="cool">that</this>')
  doc.extractor!

  doc.extract('this') # => 'that'

  doc.extract('this', attr: :is) # => 'cool'

  doc.extract('this', regexp: /th(.*)/) # => 'at'

  doc.extract('this') {|text| text.upcase} #=> 'THAT'

== REQUIREMENTS:

* nokogiri
* andand

== INSTALL:

* rake install_gem
* gem install nokogiri-extractor (Some Day).

== DEVELOPERS:

Gem creation is handled by the hoe gem.

After checking out the source, run:

  $ rake newb

This task will install any missing dependencies, run the tests/specs,
and generate the RDoc.

== LICENSE:

(The MIT License)

Copyright (c) 2013 gap intelligence

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.