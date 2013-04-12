Surf Web Browser
================

Surf is a web browser from [suckless](http://surf.suckless.org/) for X11
window system based on WebKit.  This repository is contains my local branch.
You will find a nice url bar which works like chrome url bar: you can search
using your custom search engine, define different search engines to use (using
prefixes in the url bar), or open html/local files.  The code contains has
a nice url parser.  It was build based on [search engines
patch](http://surf.suckless.org/patches/searchengines).  Second feature is
an implementation of googlebookmark.  I also use the [home
page](http://surf.suckless.org/patches/homepage) patch.

Build/Install
-------------

See the Surf README file.  Usually it is just enought to run ``make && make
install``.  If you want to use the url bar you need to configure it though,
before you compile Surf.

Configuration & Usage
---------------------

You can add to the ``config.h`` file:

```
static SearchEngine searchengines[] = {
    { "py",     "http://docs.python.org/2/search.html?q=%s&check_keywords=yes&area=default", 1},
    { "py3",    "http://docs.python.org/3.2/search.html?q=%s&check_keywords=yes&area=default", 1},
    { "wiki",   "http://en.wikipedia.org/wiki/%s", 1},
    { "gmail",   "http://mail.google.com/", 1},
};
static const char * defaultsearchengine = "http://www.google.co.uk/search?q=%s";
static const char * googlebookmarkurl = "http://www.google.com/bookmarks/mark?op=add&hl=en_GB&bkmk=%s&title=%s";
```

Then if you hit CTRL-g and you can type:
```
Search Query
```

and Surf will open google search for `Search Query`.  If you type:
```
py cd.open
```
Surf will land on search result page of python 2.7.3 documentation for the
`cd.open` query.  And if you type:
```
gmail
```
you will surf to the gmail page.

Finally add the following definition:
```
#define HOMEPAGE "https://www.google.co.uk"
```
Surf will open this web page when it starts.

And finally add the following code to the hotkeys (``Key keys[]``):
```
    { MODKEY|GDK_SHIFT_MASK,GDK_b,	loaduri,    { .v = "https://www.google.co.uk/bookmarks" } },
    { MODKEY|GDK_SHIFT_MASK,GDK_a,	googlebookmark,  { .v = "" } },
    { MODKEY|GDK_SHIFT_MASK,GDK_h,	loaduri,    { .v = "https://www.google.co.uk/" } },
```
Then hitting CTRL-SHIFT-b (^B) will take you to the google bookmarks page,
CTRL-SHIFT-a (^A) will bookmark the current page in the google bookmark app:
it just opens the form and prefils it with some data for you.  The last
shortcut CTRL-SHIFT-h (^H) opens the HOMEPAGE.
