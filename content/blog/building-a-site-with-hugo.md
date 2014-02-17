{
    "Title": "Building a Site with Hugo",
    "Description": "An account of the steps I went through building this site using hugo, html5 boilerplate, Disqus, etc.",
    "Keywords": [
        "Blog",
        "Programming",
        "Hugo",
        "Initializr"
        "H5BP"
    ],
    "Pubdate": "2014-02-03",
    "Section": "blog",
    "Slug": "building-a-site-with-hugo",
    "Tags": [
        "Blog",
        "Hugo"
    ],
    "Thumbnail": "/img/missing.png",
    "Topics": [
        "Blog"
    ]
}

Here's an outline of what I went through to build this blog.  You can
see the live code at [github](http://github.com/jcdny/j3ff.com).

* Fork, checkout, and build [Hugo](http://github.com/spf13/hugo) to do the site generation.
* Create a [github repo for this site](http://github.com/jcdny/j3ff.com).
* Generate the basic site markup from
  [Initializr.com](http://www.initializr.com/) and copy it to j3ff.com/static.
* Set up a [Google Analytics](http://www.google.com/analytics/) account to get basic site statistics.
* Set up a [Disqus](http://disqus.com/websites/) account for comments.
* Cargo cult the basic file structure and templates from [spf13.com](https://github.com/spf13/spf13.com) and [xaprb.com](https://github.com/xaprb/xaprb.com).
* Get lost in a maze of twisty little passages, all alike (and
  gradually work out the Go templating language works and how the layouts are
  applied).  After some fiddling I managed to get pages that were at
  least readable.
* With the local version working I set up the s3 bucket for my domain and DNS with Route 53 as per the
  [AWS static site howto](http://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html).
  and used `s3cmd sync . s3://j3ff.com` to copy the static site up to s3.

At this point I had a sort of working but very ugly site.
{{% img src="/img/2014/website-initial-th.png" alt="The first cut at the site." class="right" %}} 
On the other hand the Disqus comments and Google Analytics both work
as does the tag and topic subindex generation.

Next step is to work through the css and some of the markup to get
something that would not offend a blind dog, unlike the current site.

## Trials and Travails ##

At one point I had `{{ template "chrome/footer.html" }}`
rather than `{{ template "chrome/footer.html" . }}`
and without the last "**.**" the template did not have the variables
available to it and of course I spent entirely too long figuring that
out.

There is a bug with forming canonical URLs and RSS URLs which I felt
compelled to track down (cf. [here](https://github.com/jcdny/hugo/commit/836cf46168b610ed1f2f0857b3eb989e59f00d78)).

There was a panic with a malformed shortcode attribute which was also
annoying to track down
([bugreport](https://github.com/spf13/hugo/issues/193)).  It was not
that bad since I don't really have much content yet but I could see a
larger site being problematic since even `hugo -v` did not really give a
clue to where the parse error was occuring.

The section title is created by programatic pluralization via
`n.Title = strings.Title(inflect.Pluralize(section))`<br>
which gives the title for the blog section as "Blogs" which is pesky.
I think programmatic pluralization like that is almost never a good
idea and it should probably be handled the way indexes are handled
with the plural in the config file.

## So Far, So Good ##

It's been a while since I have done any web development and never
really did static site generation but I'm enjoying hugo so far.  It's
certainly fast and the watch and local regenerate is nice.  I also
like having a Go based generation engine since Go is awesome.




