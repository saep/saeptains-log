# Building a prototype

This is the second post describing my progress on this project. I'm actually
enjoying this experience more than I anticipated. While starting to move
things around and creating the first set of modules, I actually started to
change some of the general structure of the project.

## I changed my mind

I don't insist on limiting myself to a git repository as I found the
[filestore](https://github.com/jgm/filestore) library. Now git, darcs and
mercurial can be chosen as blog entry backends. Well, at least the brief
look at the documentation showed that it provides me with the information
I need. If someone wants to implement it, other repository types could work,
too. The library provides a convenient interface to retrieve the version
information I need, so it seems to be a perfect fit for the job.

I also ditched the notion of a required repository layout. As those version
control systems can handle the number of files I'm expecting in a somewhat
wort-case analysis quite well, I will just scan the whole repository for
supported files on startup. This should suffice for this early development
stage.

## I played around with CSS

I also started working on my personal style sheet. It's definitely not done,
but it renders my previous post pretty enough for a first draft. I even had
to google around for hacks to make the navigation bar span the whole display
with while keeping the content smaller. I already start to fear the days
when I want to make this application look good on my mobile phone... I think
I'm getting carried away now.

## The project structure -- Part 2

I now have essentially three modules. One is just a nice wrapper with some
extensible data types to store configuration data. Another one is the entry
serving the blog, which also has some configuration data structures as well
as some drafty data types to do filtered searches on blog content. I think
that I'm getting carried away again... The third module is an HTML template
for the blog part of this web application. There is also the executable, but
I may some day replace it with
a [dyre](https://github.com/willdonnelly/dyre) replacement. But for now

> cabal run saeplog --entry-path "~/git/myblog" --resources "~/git/blog/resources

suffices for my development needs.


## Next steps

* Scan the blog entry path for entries and blog about writing the code for
  it.
* After the entry from the previous task is done, I will probably have to
  create a code highlighting style sheet for my embedded Haskell code.
* I definitely should create a test-suite.
* Make this application build on the travis continuous integration which is
  somewhat built in to GitHub.

I hope to get a reasonably structured project up and running very soon, so
that I can upload a working prototype on [GitHub](https://github.com).
