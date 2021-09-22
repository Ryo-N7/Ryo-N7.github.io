---
layout: post
title: "76th Tokyo.R Users Meetup Roundup!"
fb-img: https://i.imgur.com/UlstyyS.png
share-img: https://i.imgur.com/UlstyyS.png
tags: [japan, japanr, japan.r, community, tokyor, r-bloggers]
---

<center>
<img src = "https://i.imgur.com/UlstyyS.png" width = "450" />
</center>

The 76th [Tokyo R](https://tokyor.connpass.com/) User Meetup happened on
March 2nd, graciously hosted by DeNA (an entertainment and
e-commerce company) in their lovely headquarters located in Shibuya.

<center>
<img src = "https://i.imgur.com/mwSzXDq.png" width = "550" />
</center>
<center>
(Photo courtesy of Takashi Minoda)
</center>
On this day another R User Meetup was also happening up in Sapporo,
Hokkaido. You can check them out
[here](https://www.urano-ken.com/sapporor/events/sapporor09/). Although
this was the second Tokyo.R of 2019 I wasn’t able to attend the one in
January as I was at the RStudio::Conf in Austin, Texas… a long way from
home! Similar to my [roundup blog
post](https://ryo-n7.github.io/2018-12-06-japanr-conference-roundup-blog-post/)
of the talks at [Japan.R](https://japanr.connpass.com/event/105802/) I
will be going through around half of all the talks. Hopefully, my
efforts will help spread the vast knowledge of Japanese R users to the
wider R community. Throughout I will also post helpful blog posts and
links from other sources if you are interested in learning more about
the topic of a certain talk. You can follow __Tokyo.R__ by searching for the
[\#TokyoR](https://twitter.com/hashtag/TokyoR?src=hash) hashtag on
Twitter.

Unlike most R Meetups a lot of people present using just their Twitter
handles so I’ll mostly be referring to them by those instead. I’ve been
going to events here in Japan for about a year but even now sometimes
I’m like, “Whoahh that’s what
`@very_recognizable_twitter_handle_in_the_japan_r_community` actually
looks like?!” Anyways…

Let’s get started!

Beginner Tutorials
==================

Every __Tokyo.R__ sessions starts off with three talks given by one of the
organizing team members who go over some of the very basic aspects of R for
beginner users. These talks are given by very experienced R users and
are a way to let newbies feel comfortable before diving into real world
applications of R in the main talks and LTs happening later on.

In this edition of Tokyo.R:

-   [ktatyamtema](https://twitter.com/kotatyamtema) gave a talk on R
    basics, from downloading and installing packages, reading in data
    files into R, and saving outputs from R.

-   [Slides](https://speakerdeck.com/kotatyamtema/tokyor76-beginnerssession1)

-   Next, [kilometer00](https://twitter.com/kilometer00) gave a talk on
    data pipelines, specifically focusing on proper coding style and
    thought process behind good programming. He showed some really great
    examples, like in the picture below, of writing code that is easy to
    understand by using the `tidyverse` verbs and pipes. His entire
    slideshow has tons of great images on how to visualize programming
    in R which you really don’t need Japanese to understand so I
    recommend beginners to have a look through them!

-   [Slides](https://speakerdeck.com/kilometer/tokyo-dot-r-number-76-beginnersession-data-pipeline)

<center>
<img src = "https://i.imgur.com/zp6u7Y5.jpg" width = "550" />
</center>
-   Finally, [koriakane](https://twitter.com/koriakane) gave a talk on
    plotting and visualizing data using both base R and `ggplot2`. She
    carefully explained step-by-step the process of creating different
    types of graphs and working with colors and scales. At the end of
    the slides there is a huge list of `ggplot2` resources in Japanese
    that would be very helpful to Japanese R users.

-   [Slides](https://speakerdeck.com/nozomi_miyazaki/tokyo-dot-r-number-75-chu-xin-zhe-setusiyon3)

Talks
=====

[kato\_kohaku](https://twitter.com/kato_kohaku): Model-Agnostic Explanations
----------------------------------------------------------------------------

-   [Slides](https://www.slideshare.net/kato_kohaku/how-to-use-in-r-modelagnostic-data-explanation-with-dalex-iml)

In the first main talk of the day, `@kato_kohaku` dived deep into
model-agnostic explanations using the `DALEX`, `iml`, and `mlr`
packages. One of the problems seen in the ML field is the growing
complexity of models as researchers have been able to push the limits of
what they can do with increased computational power and the consequent
discovery of new methods. The high performance of these complex models
have come at a high cost with interpretability being reduced
dramatically, with many of these newer models being called “black boxes”
for that very reason. A model-agnostic method is preferable to
model-specific methods mainly due to their flexibility, as typically
data scientists evaluate many different types of ML models to solve a
task. A model-agnostic method allows you to compare these types of
models using the same method in a way that a model-specific method
can’t.

<center>
<img src = "https://i.imgur.com/U6t0zE1.jpg" width = "550" />
</center>
`@kato_kohaku` went over the workflow for performing model-agnostic
interpretation and covered partial dependence plots (PDP), individual
conditional expectation (ICE), permutation importance, accumulated local
effects plot (ALE), feature interaction, LIME, Shapley values, and more.

<center>
<img src = "https://i.imgur.com/5q3WauF.jpg" width = "550" />
</center>
The topics he covered are well explained in [Christoph
Molnar’s](https://twitter.com/ChristophMolnar) excellent book,
[Interpretable Machine
Learning](https://christophm.github.io/interpretable-ml-book/) which
`@kato_kohaku` referred to through the presentation. There are a HUGE
amount of slides (146 of them!) filled with a ton of great info that you
can can read (a lot of the slides have explanations taken straight from
the documentation in English) so I highly recommend taking a look
through them if you are interested in what the `DALEX` and `iml`
packages have to offer for interpreting models.

A great code-through explanation of using `DALEX` with `mlr` in English
can be found
[here](https://rawgit.com/pbiecek/DALEX_docs/master/vignettes/DALEX_mlr.html)
using the same data set as seen in `@kato_kohaku's` slides.

[y\_mattu](https://twitter.com/y__mattu): Operators/Objects in R
----------------------------------------------------------------

-   [Slides](https://ymattu.github.io/TokyoR76/slide.html#/)

One of the organizers of Tokyo.R, `@y_mattu`, presented on objects in R.
Specifically he went over using the `pryr` and `lobstr` packages to dig inside R
objects and see what is happening “under the hood” of your everyday R
operations.

> “Every object in R is a function, every function in R is an object”

The above maxim means that even operators such as `+` can be turned into
a function using parentheses to place all the arguments:

<center>
<img src = "https://i.imgur.com/HZY2g5V.jpg" width = "550" />
</center>
Looking deeper `@y_mattu` used the `ast()` function from the `lobstr`
package to see the abstract syntax tree of the R expression that was
shown above, `1 + 2`.

``` r
library(lobstr)
lobstr::ast(1 + 2)
```

    ## o-`+` 
    ## +-1 
    ## \-2

The above shows the exact order in which the functions are being run by
R. To now understand *what* is happening when we run this operation we
need to look at the R environment. To check which environment holds the
`+ ()` operator

``` r
library(pryr)
```

    ## 
    ## Attaching package: 'pryr'

    ## The following objects are masked from 'package:lobstr':
    ## 
    ##     ast, mem_used

``` r
pryr::where("+")
```

    ## <environment: base>

And we find that the `base` package holds this operator and it is called
from the `base` environment. In the final part `@y_mattu` looked into
the `+` operator itself by looking at the `.Primitive()` as well as
`pryr::show_c_source()` to see the C source code used to make R be able
to run `+`.

This was a very technical topic (for me) but it piqued my interest on
what’s actually happening whenever you run a line of R code!

[bob3bob3](https://twitter.com/bob3bob3): `DeNA`
================================================

-   [Slides](https://www.slideshare.net/bob3/tokyor-76-lavaan-plot)

At every Tokyo.R the hosting company is given time to talk about their
own company, how they use R, and hopefully provide some information for
any interested job seekers. For [DeNA](https://dena.com/intl/),
`@bob3bob3` gave this talk and he provided us on some details on what
exactly DeNA does as well as his own LT on SEM using `lavaan`. DeNA is a
entertainment/e-commerce firm that is most well-known for it’s cellphone
platform, `Mobage`. Interestingly, they also took ownership of
[MyAnimeList](http://myanimelist.net/) a few years back (probably one of
the largest anime/manga database communities in the world). For job
seekers he talked about the large variety of positions DeNA have
available in the “Kaggler” category as well as open positions in the
automobile, healthcare, sports analytics, HR analytics, marketing
researcher departments, and more…!

Following his elevator pitch about DeNA he gave a small talk about using
`lavaan` to plot out path analysis for structural equation modeling.
`@bob3bob3` explained how he ended up creating his own plotting function
using the `DiagrammeR` and `Graphviz` packages to visualize the `lavaan`
output as he did not like the default plotting method.

<center>
<img src = "https://i.imgur.com/V4dZi69.jpg" width = "550" />
</center>

Lightning Talks
===============

[flaty13](https://twitter.com/flaty13): Tidy Time-Series Analysis
-----------------------------------------------------------------

-   [Slides](https://docs.google.com/presentation/d/1xDy9WrtcAskGKA5k5hpoIk7xaoFiwyv1u4vjdt45agE/edit#slide=id.p)

`@flaty13`, who has also recently presented at
[Japan.R](https://docs.google.com/presentation/d/1QSm7EDgNk7OeLWb266LZ57787v0tybirQ3Kr5A9cmHA/edit#slide=id.p)
and [SportsAnalyst
Meetup](https://docs.google.com/presentation/d/1WPO_Cc4fpXs3nGLzTvk8PTQlHBU-jswS6oJhu7Hi1f0/edit#slide=id.p)
on tennis analytics, gave a talk on analyzing time-series data with R.
He first talked about how packages like `lubridate` and `dplyr`, while
useful, may not be the best way to handle time series data. The solution
`@flaty13` talked about was the `tsibble` package created by [Earo
Wang](https://twitter.com/earowang). At RStudio::Conf 2019 Earo gave a
talk on this package and using tidy data principles with time series
data which you can watch
[here](https://resources.rstudio.com/rstudio-conf-2019/melt-the-clock-tidy-time-series-analysis).

`@flaty13` used his own pedometer data from a healthcare app on his
iPhone for his demonstration. After reading the data in and performing
the usual tidyverse operations on it, the data frame was turned into a
`tsibble` object and then visualized as a calendar plot using the
`sugrrants` package (also by Earo Wang).

<center>
<img src = "https://i.imgur.com/Ld1jmWp.jpg" width = "550" />
</center>

[saltcooky](https://twitter.com/saltcooky): Organizing a R Study Group at My Company!
-------------------------------------------------------------------------------------

-   [Slides]()

`@saltcooky` took the time to talk to us about something that doesn’t
usually get mentioned at Tokyo.R, as he reported about the success of an
intra-company R workshop he hosted. At `@saltcooky's` company the
majority of his co-workers are *Pythonistas* with only three other
co-workers and him being R users. Hoping to change this dynamic,
especially as their company does a lot of data analytics, `@saltcooky`
set out to create some workshops. What he came up with were three
separate sessions heavily inspired by the Tokyo.R method that I talked
about in “Beginner Tutorial” section.

-   The first session was basically around an hour on R basics and
    talking about what exactly you can do with R, where he got the
    *Pythonistas* to slowly get interested in using R for various
    analytical tasks.
-   Second, was a tidyverse data handling/processing session with some
    hands-on exercises with help from `@y_mattu`.
-   The third session was using `ggplot2` for visualization.

Throughout the workshops `@saltcooky` was asked some peculiar questions
like “Is there a difference in using `.` vs. `_` in separating words in
a function/object name?” and “Why are there so many packages/functions
with the same functionality!?”.

One of the major hurdles that `@saltcooky` faced was in installing R for
all the different OSes that his co-workers used. The solution he came up
with was to use **RStudio Cloud**. This eased the burden for him as he
didn’t need to set up or manage any servers while the students did not
need to install any software at all! There was actually a great talk on
using [“RStudio Cloud for
Education”](https://resources.rstudio.com/rstudio-conf-2019/rstudio-cloud-for-education)
by Mel Gregory at **RStudio::Conference 2019** a few months ago and it’s
a great resource for others thinking about holding workshops.

`@saltcooky` concluded that his workshops were a mild success as he was
able to get a couple more people using R casually at his workplace and
although Python remains dominant he looks forward to convincing more
people to use R in the future.

[moratoriamuo271](https://twitter.com/moratoriamuo271): Topic Modeling Cooking Recipes!
---------------------------------------------------------------------------------------

-   [Slides](https://speakerdeck.com/funain/topitukumoderude1zhou-jian-falsexian-li-worekomendosuru)

Continuing the theme of “tidy” data analysis, `@moratoriamuo271` applied
the concept to text analysis. The motivation for this talk came from the
difficulty and hassle of figuring out a nice set of meals to eat over
the course of a week. To solve this problem he sought to create a
recommendation engine for recipes!

<center>
<img src = "https://i.imgur.com/Rf1sJkm.jpg" width = "550" />
</center>
As seen in the above flowchart `@moratoriamuo271`: 

1. Web scraped recipes using `rvest` 
2. Created some word-clouds for some EDA 
3. Used the `RMeCab` and `tm` to create an organized document term matrix
(`RMeCab` is a package specifically for Japanese text analysis) 
4. Latent Dirichlet Analysis with `topicmodels` and `ldatuning` packages 
5. Finally, splitting recipes into categories with `tidytext`

Before he showed us the results of his work, `@moratoriamuo271` took us
through a crash course on various topic modeling techniques from the
basic uni-gram model, to mixture of uni-gram models, and finally on
Latent Dirichlet Analysis (LDA).

<center>
<img src = "https://i.imgur.com/9W8btEx.jpg" width = "550" />
</center>
He also went over the process in which he decided on the optimal number
of topics for his recommendation engine. This was done by looking at the
perplexity values from the `ldatuning` package.
[Here](http://freerangestats.info/blog/2017/01/05/topic-model-cv) is a
great blog post by [Peter Ellis](https://twitter.com/ellis2013nz) on
using cross-validation on perplexity to determine the optimal number
of topics. Below is the final finished product that gives you recipes
for nutritious and balanced meals for seven dinners!

<center>
<img src = "https://i.imgur.com/yP4MYZK.jpg" width = "550" />
</center>
`@moratoriamuo271` has also released a blog post with ALL the code that
you can check out
[here](http://moratoriamuo.hatenablog.com/entry/2019/03/05/004229)!

Other Talks
===========

I couldn’t go through all of the talks but I will provide their slides
below (if/when they become available)

-   [utaka233: Shrinkage estimators and applications to
    baseball](https://speakerdeck.com/utaka233/suo-xiao-tui-ding-falsehanasi)
-   [katoshoo: Random matrix](https://www.slideshare.net/ShoKato2)
-   [Hioki Ryuji: Trading systems with
    R](https://speakerdeck.com/lyuji282/rdeshi-merusisutemutoredo)
-   [0\_u0: Advantages and Disadvantages of Public/Open data]()

Conclusion
==========

After the talks, everyone got together for a little after-party over
food and drinks. Usually pizza is served but this time was a bit more
fancy with kara-age and cheese-on-crackers being served. As the night
wore on R users from all over Tokyo talked about their successes and
struggles with R.

Unfortunately, there is only so much I can do to translate the talks,
especially as __Tokyo.R__ doesn’t do recordings anymore, but I hope that I
could be of some help and maybe you’ll be inspired by a code snippet
there or a certain package name elsewhere, etc.! __Tokyo.R__ happens almost
monthly and it’s a great way to mingle with Japanese R users as it is
the largest regular meetup here in Japan. Talks in English are also
welcome so if you’re ever in Tokyo come join us!

<center>
<script type='text/javascript' src='https://storage.ko-fi.com/cdn/widget/Widget_2.js'></script><script type='text/javascript'>kofiwidget2.init('Buy Me A Coffee!', '#29abe0', 'O4O342A2A');kofiwidget2.draw();</script> 
<center/>
