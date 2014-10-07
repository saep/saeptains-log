# Writing this blog

This blog post is the first that I actually do and it is about writing the
blog software that I am (hopefully) publishing this post from. I did try to
do this some time ago, but I never really got around to actually do it.

This post is structured in a few different sections. First
I will describe my [intentions](#intentions) for writing this piece of
software. Then I will describe the rationales behind the basic [tools and
libraries](#tools) that I chose. In the passing years, these might change,
though. Then I will describe the basic [project structure](#structure) that
I am planning to use.

## Intentions {#intentions}

I like using my good old vim for text editing and I really hate those
limited browser-based editing windows. I realize that I do not gain a lot by
using vim for a task such as writing a blog post, but I **just want to do it
that way**! I also want to strife away from my part-time day job for which
I mainly write `Java` code and I think that I miss these cute Compile-time
errors that free me from a lot of debugging. The only things that
I currently do in Haskell are the occasional [project
Euler](https://projecteuler.net) riddles and some work for my master thesis.
A major part of my motivation is to try out some of the Haskell libraries
for everyday tasks, such as `JSON`-processing, file conversion, web
development, testing and project design. To combine all these, I need
a non-trivial extensible project and that is what a web presentation, which
might initially just be a blog, can fulfill.

The workflow of writing blog posts should be kept quite simple. I want to
write [(pandoc's)
markdown](http://johnmacfarlane.net/pandoc/README.html#pandocs-markdown) or
eventually literate Haskell into a simple text file and commit it to a git
repository. I kind of did such a year or two back with
[pyblosxom](https://pyblosxom.github.io/), but I wasn't really happy with
it.

Another motivation for writing blog posts is my recent transition to the
[Colemak](http://colemak.com) keyboard layout, which I might blog about if
I've gotten used to it a bit more.

## Tools and libraries {#tools}

### The web framework

Initially, I wanted to use the [Yesod Web
Framework](http://www.yesodweb.com) as it seemed to be high-quality piece of
software with incredible benchmarks and it includes all the bells and
whistles you might need. There are however a few key moments that kept me
away from using it. At two points in time somewhere in the last 4 years,
I was tempted to write a web application and tried using Yesod. I was quite
inexperienced and I couldn't get it to install the first time within an hour
and then I gave up. The second time, I was able to set it up, but the book
diverged to far from the library and it was to annoying to synchronize that.
Hence I gave up after an hour again. The urge to actually create a web
application war probably not big enough.

The other alternatives that I looked at were
[Snap](http://snapframework.com) and [Happstack](http://happstack.com). Snap
kind of scared me away with yet another piece of a web-specific language,
namely [Heist](http://hackage.haskell.org/package/heist).

Happstack seemed to be the simpler one to learn and so I chose it. The site
seemed eledant and yet simple and the tutorial link thew tiny numbers at me:

> Tutorials

> A good starting point is the happstack-lite tutorial. It's less than 2000
> words long, yet contains everything you need to create a full-featured
> website:
> [..]

Only 2000 words! That is marketing I like. And another important appraisal
was this sentence from the title page:

> If you are looking for a lightweight, simple solution we recommend
> starting with happstack-lite. happstack-lite provides everything you need to
> implement a web application with out relying on template haskell, external
> preprocessors, or complex types. It is possible to seamlessly transition
> into from happstack-lite into the full happstack ecosystem -- so you are not
> limiting yourself by starting with happstack-lite.

If the lite version isn't enough, I can just upgrade. That seems to be
great.

### The file conversion

Pandoc has become the tool of choice concerning document conversion for me.
It supports a lot of typical markup languages as well as literal Haskell to
quickly create documents in the format I want. I used Emacs with the
fabulous [orgmode](http://orgmode.org) which is a great piece of software
and it was second in the tools to use, but as I do not use the org-mode
anymore, especially since I moved back to vim, it fell to the second place.
I do not (yet) have any use cases for the advanced features of orgmode
except for throwaway `TODO`-lists whose elements are not worthy to be raised
in the existence of a ticket in a ticket system like
[Redmine](http://www.redmine.org). For these, a small markdown list is
sufficient enough anyway.

### The persistence

For the blog entries I plan to use a simple Git repository with a specific
layout. The top-level folders are the years in which I wrote the entries.
In these folders are all entries of the year. I don't expect to write a lot
of these, so indexing should be almost instantaneously. I first thought
about doing a full folder hierarchy down to days, but that seems to be
overkill for the  occasional blog post that I will probably write. As
I sometimes remove typos or fix broken links in documentation at work on
a very regular basis, using the timestamps of last edit and such are not
really useful, so I need some metadata somehow. As I started this section,
I thought about generating a `JSON` metadata file together with the content
file, but as I am already using git to store the files, I can also just use
the metadata stored within the repository. It at some point, I want to
support comments, I should probably create a folder for each blog post
I make. Alternatively, I could use a data base for that. I think I will go
for databases as it is another technology to test out in Haskell and it is
still a feature I haven't planned yet. As nobody may be reading these posts
anyway, a manual email is probably a reasonable starting point.

### The things I did not think about

Yeah, I don't think about a lot of things. Whole libraries are actually
filled with it! ;-)

## Project structure {#structure}

I suppose the term *modular* should be sufficient to describe the project
structure. As I'm testing out various libraries, I should be able to simply
replace a module and be done with it. In this case, I might at some point
start to write factor things out into separate cabal modules.  The whole
project should be usable as a library in the end, so I will have to think
about the exported functions and decide how configurable the software should
be. As blogging should just be a starting point for this project, every
component should essentially be a composable object and hence a configurable
library function or module. To start of, I will hence need a Template
module for the blog entries and its metadata that will be inserted into
a highly personal general web layout. As I am just starting and nothing is
release-worthy, I will keep everything within one cabal project for.

