---
layout: post
title: "My #TidyverseDevDay and #RStudioConf 2019 Reflections!"
fb-img: https://i.imgur.com/1vHPksG.jpg
share-img: https://i.imgur.com/1vHPksG.jpg
tags: [rstudioconf, community, tidyversedevday, open-source, tidyverse, r-bloggers]
---

This was my second **RStudio Conference** following last year’s edition
in San Diego! In addition, at **Tidyverse Developer Day** I got a really
cool chance to work on issues and contribute to making the Tidyverse
better. This post won’t be a complete overview of the talks at the
conference (others have already released some good blog posts on that
note: [Julia Silge](https://juliasilge.com/blog/rstudio-conf-2019/),
[Brooke Watson](https://blog.brooke.science/posts/rstudio-conf-2019/),
[Zev
Ross](https://www.zevross.com/blog/2019/01/22/15-new-ideas-and-new-tools-for-r-gathered-from-the-rstudio-conference-2019/),
etc.) and will be more of a reflection on how I contributed to the
Tidyverse at \#TidyverseDevDay and how I felt being at the conference.

As usual I collected a bunch of hex stickers at this conference, many of
them that I already own… I seem to have a weird thing about collecting
them but never using them (from Twitter I can see this isn’t something
that’s exclusive to me however). Talking about hex stickers…for
**Tidyverse Developer Day** each participant got a shiny Tidyverse hex
medallion!

|                           Front side                          |                           Back side                           |
|:-------------------------------------------------------------:|:-------------------------------------------------------------:|
| <img src = "https://i.imgur.com/1vHPksG.jpg" width = "350" /> | <img src = "https://i.imgur.com/YSND5RZ.jpg" width = "350" /> |

Too bad it’s not like the Dumbledore’s Army galleon, or Hadley could
just send a covert message to all the participants, like “TidyDevs,
Assemble!” Maybe next year, I suppose.

Anyways, let’s get started!

Tidyverse Developers’ Day
=========================

The day following **RStudio::Conf** those lucky people that got a ticket
gathered at the “Sunset Room” to contribute to the Tidyverse. After
grabbing a quick coffee and breakfast taco, Hadley made a small
introduction outlined exactly what and how the day was going to go and
then we all got to work. There was a large list of tagged issues ready
for us but we could also choose our own and ask a RStudio member to tag
it as “tidy-dev-day” for us.

After finding an issue I wanted to work on here was my basic workflow:

-   Fork the repo of the package I needed to work on.
-   Go into RStudio: File &gt; New Project &gt; Version Control &gt;
    Git &gt; Paste the `.git` link from your forked repository on GitHub
    (click on the big green “Clone or download” button)
-   Once you’ve opened up the project, make sure to create a new branch
    through the Git tab (click on the icon with two purple boxes next to
    the gear icon)
-   You’re all set to start coding!

There is another way to do most of this through the Git Bash terminal,
which you can learn from Tony’s blog post
[here](https://tonyelhabr.rbind.io/post/making-first-pull-request/).

The main things I focused on were improving documentation and providing
additional examples. For these tasks I found it important to do a lot of
research first. Thankfully I was able to find many Stack Overflow posts
of people explaining the issues that I wanted to write about as well as
\#rstats blog posts/tutorials that could provide me with ideas on how to
phrase things and write good small examples!

An important thing that I learned was that it’s good practice to create
a different branch for working on a Pull Request for different issues on
the same package! When you’re changing documentation in a package it’s
important to make sure you use `roxygen2` package’s `roxygenize()`
function to update changes. Don’t forget to run the R CMD Check as well
(the “Check” icon in the `Build` tab). After you’re done with all of
that, it’s time to commit, push, then create a pull request (PR) to
merge your proposed changes with the master branch!

When you write a commit message you can use a hashtag and then number to
refer to issues in the Github repo as well as use a number of
[keywords](https://help.github.com/articles/closing-issues-using-keywords/)
to close these issues automatically (in our case when the PR is merged).
<center>
<img src = "https://i.imgur.com/NQZJEDG.jpg" width = "350" />
</center>
If you check Github you can see that it automatically prepended the repo
name and a link to the issue being referenced.
<center>
<img src = "https://i.imgur.com/532Ari6.jpg" width = "350" />
</center>
Then I waited to see if those changes were approved or if there were
still a few things that needed changing:

|                            forcats                            |                             purrr                             |
|:-------------------------------------------------------------:|:-------------------------------------------------------------:|
| <img src = "https://i.imgur.com/6b874kK.jpg" width = "550" height = "800" /> | <img src = "https://i.imgur.com/ZVwGyPa.jpg" width = "550" height = "800" /> |

OK! After reading the comments from Hadley (!) and Lionel (!) I go back
into my branch in RStudio and fix those changes. When I commit and push
to my forked repo again, it is automatically tracked in the PR. I
usually make the comment, “edits to comply with PR review” when pushing
again.

|                            forcats                            |                             purrr                             |
|:-------------------------------------------------------------:|:-------------------------------------------------------------:|
| <img src = "https://i.imgur.com/gMS7y12.jpg" width = "550" height = "800" /> | <img src = "https://i.imgur.com/fB2wP27.jpg" width = "550" height = "800" /> |

There we go, I have now officially contributed to the Tidyverse!

<center>
<img src = "https://media2.giphy.com/media/l4JySAWfMaY7w88sU/source.gif" width = "450" />
</center>

Another good resource for contributing to open-source is [Nic
Crane’s](https://twitter.com/nic_crane) step-by-step [blog
post](https://thisisnic.github.io/2018/11/28/ten-steps-to-becoming-a-tidyverse-contributor/)
(she also presented at RStudio::Conf on building a Shiny app for genomic
medicine) and [Tony El-Habr’s](https://twitter.com/TonyElHabr) [blog
post](https://tonyelhabr.rbind.io/post/making-first-pull-request/) also
on \#TidyverseDevDay (whom I actually met at the Sports Analytics
Birds-of-a-Feather session!).

I felt this was a fantastic opportunity for people of all skill levels
to experience contributing to open source. The RStudio team were very
helpful buzzing around the event space and for those extremely new to
programming or git it was a valuable lesson as you were guided along the
process from start to finish. For myself, I have had previous experience
contributing to open source packages as well as creating, testing,
bug-squishing R packages at my workplace but this was a great way for me
to give back to the R community in what little way that I could. I
actually still have a few more issues from **Tidyverse Developer Day**
that are a work-in-progress and I hope to continue contributing in the
future!

RStudio::Conf 2019
==================

To get to Austin I had a long flight in from Japan with a 5 hour layover
in Minneapolis. Bored, I decided to do some
[\#TidyTuesday](https://github.com/rfordatascience/tidytuesday) to pass
the time. It turned out
[alright](https://twitter.com/R_by_Ryo/status/1085901682507243520) in
the end but jet lag does not make for very interpretable code… While I’m
still on the topic of \#TidyTuesday… apparently, [Thomas
Mock](https://twitter.com/thomas_mock) had some TidyTuesday hex stickers
but unfortunately I couldn’t get my hands on them!

Here were some of my highlights from Day One:

-   [Joe Cheng’s](https://twitter.com/jcheng) keynote on `shinytest`,
    `cranwhales`, `shinyloadtest`, `rendercachedplot`, and **RStudio
    Connect** showing how Shiny can be completely used for production.
    ([Slides](https://speakerdeck.com/jcheng5/shiny-in-production))

-   An **awesome** \#DataForGood type of presentation by [Brooke
    Watson](https://twitter.com/brookLYNevery1) who talked about using R
    to tidy data on families separated at the US border.

-   [Tyler Morgan-Wall](https://twitter.com/tylermorganwall) on
    `rayshader`: I’ve been casually keeping up with developments on
    twitter but I was still wowed by the presentation, especially 3D
    printing. If I had that kind of tech when I was a kid I would’ve won
    ALL the science fairs with the most realistic looking baking soda
    volcano!

-   [Thomas Pedersen](https://github.com/thomasp85) came out with
    another `gganimate` presentation showing all the new features
    introduced since his last `gganimate` talk at UseR 2018. This is
    definitely a talk that you need to watch for all the examples!
    ([Slides](https://www.data-imaginist.com/slides/rstudioconf2019/assets/player/keynotedhtmlplayer#0))

All in all **Day One** was great but I was still pretty exhausted from
my long trip so I didn’t get to talk to as many people as I liked.

**Day Two** began with a great talk on teaching programming by
[Felienne](https://twitter.com/felienne), her talk was so good I
realized she didn’t say anything about R until after she finished! My
biggest take-away from her was “You don’t become an expert by doing
expert things!” which I agreed with as a self-taught R user. For me it
was really about starting with the basics, integrating what I already
knew outside of R into what I did with R (ex. bringing my love of soccer
into creating [World Cup
visualizations](https://github.com/Ryo-N7/soccer_ggplots) with `ggplot2`
and `gganimate`), and incrementally building up my skills through
reading blog posts and tutorials.

One of the most informative talks from my perspective was by [Jim
Hester](https://twitter.com/jimhester_) on dependencies. He talked about
how “not all dependencies are created equal” due to differences between
dependencies in install times, package sizes, and the system
requirements. He also talked about the “illusionary superiority” problem
every package developer gets in regards to overestimating their own
abilities and underestimating the probability of introducing new bugs
from adding dependencies. To address these concerns Jim introduced the
`itdepends` package which acts as a toolbox for dependency
decision-making. This package allows one to assess usage, measure
weights, visualize proportions, and assist in the removal of
dependencies through a series of `dep_*()` functions. As I help develop
and maintain all the R packages that my [NGO](https://www.acdivoca.org)
uses for data processing/visualization, this talk and package will be
extremely useful for me to do some code “auditing” and find ways to
reduce technical debt.
([Slides](https://speakerdeck.com/jimhester/it-depends))

Several other highlights from **Day Two** were:

-   [Rich Iannone](https://twitter.com/riannone) formally introducing
    the `gt` package: this looks like a great alternative to using
    `kable` or `DT` for creating well-formatted tables!
    ([Slides](https://github.com/rich-iannone/presentations/tree/master/2019_01-19-rstudio_conf_gt))

-   [Jenny Bryan](https://twitter.com/JennyBryan) and [Lionel
    Henry](https://twitter.com/_lionelhenry) both separately presented
    on the various use cases and associated challenges of tidyeval.
    [Jenny Bryan::Slides](https://rstd.io/tidy-eval-context), [Lionel
    Henry::Slides](https://speakerdeck.com/lionelhenry/selecting-and-doing-with-tidy-eval)

-   [Jesse Sadler](https://twitter.com/vivalosburros) talked about
    tackling problems dealing with accounting/inheritance data from 16th
    Century Europe using R. Along the way he created the `debkeepr`
    package to help himself analyze non-decimal currencies!
    ([Slides](https://github.com/jessesadler/rstudioconf-2019-slides))

On **Day Two** I mustered up the courage and energy to go to two
different Birds-of-a-Feather sessions, Public Sector/Government and
Sports Analytics. At lunch I was able to meet R users from places like
the Federal Reserve and the Federal Aviation Administration. I heard
stories on how hard it was to convince people, especially non-technical
higher-ups, to give them the green light to switch to R as well as more
recent success stories of running workshops and tutorials within their
departments. Even though I work for a NGO I felt comfortable talking to
these people and it was a great way to exchange knowledge with people in
a somewhat similar industry (especially since I was unable to attend the
“Data for Good” Birds-of-a-Feather session). The shadow that hung over a
lot of the people I met was that they were unable to work due to the
government shutdown, I can only hope that the conference provided some
good cheer and that they can get back to work soon.

In the afternoon break was the Sports Analytics Birds-of-a-Feather
session in the main conference lounge area. While I was there I finally
got to meet [Mara](https://twitter.com/dataandme) in-person for the
first time and I had an enjoyable time talking with her and the
surrounding group of baseball and hockey team analysts on the latest
trends and topics like fantasy sports and analytics in the betting
industry. Overall these Birds-of-a-Feather groups were a great way to
mingle with people in industries you’re interested in but I thought it
was a shame how some were longer/shorter depending on which slot the
event happened in. Understandably it is quite hard to schedule so many
different groups equally, but maybe a dedicated “industry” session block
could be worked in next year?

To wrap the conference up [David Robinson](https://twitter.com/drob)
gave a great keynote on spending time on contributing to open-source,
“public work”. Whether through answering questions on SO or on Twitter,
writing up a blog post, to giving a talk at a conference/meetup, David
talked about the many ways to contribute to the knowledge pool in not
just R and data science, but also for your respective research domain as
well. His words really resonated with me as he was the one back about a
year-and-a-half ago that gave me confidence to start my own blog and
share my stuff with the \#rstats community. Since then I got a job doing
R stuff and even gave a
[talk](http://rpubs.com/Ryo-N7/visualize_world_cup_with_R) at the
[TokyoR](https://tokyor.connpass.com/) meetup last summer! One of my
goals for this year is to try to do a talk in Japanese while a long-term
goal is to present at one of the big R conferences.
([Slides](https://bit.ly/drob-rstudio-2019))

Conclusion
==========

Throughout the conference I managed about four-five hours of sleep on
average, which seemed to have been a thing for other people as well:

<center>
<img src = "https://i.imgur.com/KinXTxS.jpg" width = "450" />
</center>

For me it was mostly jet lag but also I was kept up by looking up all
the cool stuff I learned and how I could apply it at work and for my own
personal projects… well, and looking up taco places to eat at on the
next day too!

This conference was the one I talked to people the most up until now as
I’ve slowly gained confidence in working in R and being a member of this
community. I was even recognized by some people for my soccer-related
blog posts, which is a first! I almost feel stupid for being rather
timid in the past and I want to try and be more outgoing in future
conferences (possibly [UseR](http://user2019.r-project.org/) in Toulouse
this year)!

For those who missed out, RStudio will be throwing all the recordings up
on Youtube in the coming weeks and you can see most of the slides
courtesy of [Karl Broman’s](https://twitter.com/kwbroman) RStudio::Conf
Github repo [here](https://github.com/kbroman/RStudioConf2019Slides)!

For next year I already grabbed a SuperFan ticket so I hope to see some
old faces and new faces next year in San Francisco. It’s going to be
nice to go back to the Bay!
