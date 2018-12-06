---
layout: post
title: "The JapanR Conference 2018 Round-Up!"
fb-img: https://i.imgur.com/YZXPElx.png
share-img: https://i.imgur.com/YZXPElx.png
tags: [japan, japanr, community, tokyor, r-bloggers]
---

This past weekend was the **9th JapanR Conference** hosted at [LINE
Corporation](https://linecorp.com/en/) in Tokyo, Japan!

I’ve been back in Japan for nearly a year now and I’ve been going to
nearly every one of the R user meetups here,
[TokyoR](https://tokyor.connpass.com/), and it’s been a great experience
to learn about R and its wide variety of uses by Japanese practitioners
and academics. Besides the near-monthly meetup of TokyoR there are
smaller gatherings spread throughout Japan such as
[FukuokaR](https://fukuoka-r.connpass.com/) and
[TsukubaR](https://tsukubar.org/) but the meeting that gathers the
biggest crowd is the [JapanR Conference](http://japanr.net/) held every
December since 2010. Of course, there are outliers such as the [special
TokyoR session](https://tokyor.connpass.com/event/92522/) this past July
when [Joe Rickert](https://twitter.com/RStudioJoe) and [Hadley
Wickham](https://twitter.com/hadleywickham) visited Japan!

-   Want to learn more about **TokyoR** and when the next meeting is?
    Check this [link](https://tokyor.connpass.com/)! (Next meeting is
    January 19th, 2019)
-   Want to learn more about **JapanR**? Check this
    [link](http://japanr.net/)!

This time around I took the time to take notes on the presentations and
write up a little round-up blog post about it. As much as I would like
to write about every single presentation there were a number of topics
where I really wouldn’t have been able to explain well even if the
presentation were done in English! You can watch most of the
presentations on the [JapanR YouTube
channel](https://www.youtube.com/channel/UCXKQBlJczU7YTyVu_wW7yHA).
Although the talks are in **Japanese** maybe you’ll still find something
useful in their slides… or you can read on as I give a summary on around
9 (out of 22) presentations that I found interesting!

**NOTE**: Some people presented using their Twitter/online name only,
it’s just a cultural thing I’ve found here relating to privacy.

**NOTE 2**: There are still several presentations/slides that haven’t
been uploaded yet but I will put more screenshots in as they become
available so please check back in the coming days!

The Presentations
=================

### Creating your own RMarkdown template! - [Kazuhiro Maeda](https://twitter.com/kazutan)

**Kazuhiro Maeda** is well known in the Japanese R community mainly
through his online avatar (an elephant plushie) and his love for R
Markdown. For this conference he presented about creating your own
customized R Markdown template. Maeda-san noted that knowledge of CSS,
JavaScript, and Pandoc are crucial for this task as he first explained
how the `render()` function works to create a document of your choice.
Within this explanation he highlighted how the output from a `render()`
call depends on templates and options set through Pandoc, therefore it
is important to create a template that has options that can be utilized
by Pandoc. As making a template from scratch is extremely difficult,
Maeda-san recommended that you find an existing template and play around
with it to get used to the process involved.

An example template Maeda-san worked on was: having an image pop out
when you click on it in your R markdown document. To do this you need to
use “lightbox” (a JavaScript library) and implement a script in your
Pandoc template that calls on this library at the appropriate time (when
you click on an image). Following a very thorough and technical
explanation he showed us the fruits of his labor in a live-demo that you
can see [here](https://youtu.be/sXXXsb1MNMk?t=5003), where he knits the
R Markdown document and clicks on a plot image, et Voila! It pops up
very nicely!

Since I wasn’t able to translate the template creation process well
enough (live-translating technical stuff is hard!), I will leave some
good links to creating your own R Markdown template in English below:

-   [Document
    Templates](https://bookdown.org/yihui/rmarkdown/document-templates.html)
    chapter from Yihui Xie’s **R Markdown: The Definitive Guide**
-   A [list](http://jianghao.wang/post/2017-12-08-rmarkdown-templates/)
    of R Markdown template packages from Jianghao Wang
-   An example: the R markdown templates used by [Monash University
    Department of Econometrics and Business
    Statistics](https://github.com/robjhyndman/MonashEBSTemplates)
-   A short [tutorial](http://ismayc.github.io/ecots2k16/template_pkg/)
    by Chester Ismay

### Easy and modern data analysis with **“R AnalyticFlow”**! - [Ryota Suzuki](https://www.ef-prime.com/index_en.html)

**Ryota Suzuki**, CEO of
[ef-prime](https://www.ef-prime.com/index_en.html) and author of the
[pvclust](http://stat.sys.i.kyoto-u.ac.jp/prog/pvclust/) package, gave a
talk on [R AnalyticFlow](https://r.analyticflow.com/en/) which is a free
software that his company built that utilizes the R environment for
statistical computing in a GUI format. **R AnalyticFlow** was created in
Java and is compatible with Windows, Mac, and Linux OSs as well as being
available in English, Japanese, Chinese, and many more languages.

<center>
<img src = "https://i.imgur.com/82vTlE6.jpg" width = "750" height = "700" />
</center>
As you can see in the picture above, **R AnalyticFlow** allows you to
represent your data analysis workflow through nodes and edges in a
descriptive flow chart. In previous versions of the GUI, the goal was to
use as much of base R functions as possible but more recently R data
analyses including predictive modeling have been relying heavily on
external packages such as the `tidyverse`, `glmnet`, `xgboost`, etc. So
now the new direction Suzuki-san wants to take is to implement these
packages into **R AnalyticFlow** and provide support to users who want
to install their own packages to use in the GUI. Lastly, in a [live
demonstration](https://youtu.be/sXXXsb1MNMk?t=6563) he showed us a
development version of the GUI as he made some simple `ggplot2` plots
with a simple mouse-and-click. Due to the new direction **R
AnalyticFlow** is taking, Suzuki-san is looking for Java developers to
help contribute to the development of the new versions of the GUI. If
you know your way around Java and want to help, let him know!

### I have completely understood Shiny! - [Med\_KU](https://twitter.com/Med_KU)

In what was a very lively and fun presentation, `@Med_KU` took us
through a very comprehensive tour of Shiny apps. First he talked about
how to create a Shiny app via R Studio, working with the app.R and ui.R
files, and publishing through R Studio Connect. Afterwards, he went
through many examples with `plotly` and `googleVis` showing all the
interactive/reactive capabilities that Shiny apps are known for.
Personally, I’m more of a `ggiraph` fan myself (I use it at work for
flexdashboards and Shiny apps) but `@Med_KU`’s presentation has gotten
me interested in trying `googleVis` out as well!

I recommend watching the
[recording](https://www.youtube.com/watch?v=sXXXsb1MNMk&feature=youtu.be&t=6928)
of the presentation as `@Med_KU` goes through a lot of different
examples!

### DID Analysis with R! - [Yuki Yagi](https://twitter.com/Yagi__Bei)

University student **Yuki Yagi** presented on DID
(Difference-in-differences) analysis and how he utilized it in one of
his research papers. For those unfamiliar, DID is a statistical
technique that observes that differential effect of a treatment
(training program, medication intake, etc.) on a treatment group vs. a
control group. A quick overview of DID can be found
[here](https://www.mailman.columbia.edu/research/population-health-methods/difference-difference-estimation).

<!-- Yagi-san explained the process with an example of a special math training program given to two groups of kids, those who already have good grades and those that have bad grades. He explained the conundrum of finding the actual effect of the training program when there will still obviously be a gap between the smart group compared to the not-as-smart group. This is where DID comes in. DID estimates the difference in the outcome variable between the control and treatment group that would have existed if neither group had experienced the special math program treatment. Then you calculate the actual treatment effect of the training program as the difference between the observed outcome and the estimated outcome for the kids in the treatment group. -->
The main question that Yagi-san investigated in his research paper was:
“What would be the impact on the number of patents produced when
research subsidies were given to companies that were already highly
skilled and had a track record of producing many patents.”

<center>
<img src = "https://i.imgur.com/13MQoUu.jpg" width = "650" height = "600"  />
<center/>
DID is really easy to understand given the above diagram. On the left
hand side is the measurement of the outcome variable, in this case the
number of patents before the treatment while on the right is the
measurement of the number of patents after the treatment (research
subsidies) were given to the treatment group (blue dot is the control
and red dot is the treatment group).

<center>
<img src = "https://i.imgur.com/555oM5Z.jpg" width = "650" height = "600"  />
<center/>
Above is how the model looked like for the research question with the
use of dummy variables for B (subsidy), C (post-treatment), and D
(subsidy + post-treatment).

### Rugby Analytics with R! - [Koichi Kinoshita](https://twitter.com/K_Shoppi)

**Koichi Kinoshita**, a rugby performance analyst for the
[HITO-Communications Sunwolves](https://sunwolves.or.jp/en/) and the
Northland Rugby Union (in New Zealand), gave a presentation on how he
applied his nascent R skills to his favorite sport. After giving a brief
explanation about the state of sports analytics in rugby and his resolve
to improve his data analytics skills in R, he showed us a number of
plots from data he gathered from the Japanese national rugby league
website.

<!-- ![]() -->
Throughout the presentation Kinoshita-san tried to answer several
questions such as “*Is tackling percentage related to lost tries?*”,
“*Do a higher number of tackles help stop line-breaks?*”, “*Can you stop
line-breaks if you have a higher tackle success percentage?*” among
others as he explained his results in thorough detail using plots as a
visual aid. Ultimately, his data showed that those Japanese rugby teams
with over 86% tackle success rate were able to limit line-breaks to 10
or less and were very likely to win matches while those teams with a
tackle success rate below 78% mostly wound up losing.

Armed with this knowledge, Kinoshita-san investigated further and found
that across the entire season around half the teams totaled around
100\~150 tackles in any single game. Assuming an 80% tackle success
rate, a team with 100 tackles will have 20 mistackles while a team with
150 tackles will have 30 mistackles. So, the big question was: “**How
much will this 10 mistackle difference cost a team?**”

Consequently, Kinoshita-san ran a regression analysis on line-breaks
against a mistackles and found that on average you concede 10
line-breaks from 30 mistackles. Coupling this with data presented that
if a team concedes 10 line-breaks or over a team is \~70% likely to lose
a game, a higher number of attempted tackles isn’t necessarily a good
thing, what matters is **preventing line-breaks** with **successful
tackles**!

In his conclusion, Kinoshita-san brought up a really good point in that
it’s not enough to look at pure success/fail percentages and he brought
up pass completion rate in soccer as an example. I concurred with his
statement as in soccer you could naively assume a team being “dominant”
or “good” if they have a really high pass completion rate, but if most
of those successful passes came from the defenders and goalkeeper
passing among themselves you can’t really say that that is a good thing.
In soccer (and in other sports) it’s important to dig a little bit
deeper, for example it might be more insightful to look at a soccer
team’s pass completion rate in the opposition’s third of the pitch!

### Using linear regression to find a new home in Tokyo! - [Kaori Sawamura](https://twitter.com/hana_orin)

This presentation by **Kaori Sawamura** showed off a fun real life case
study using R. One of Sawamura-san’s co-workers wanted to move to Tokyo
and become a “city boy”, so she set out to use some of her newly learned
R skills to take try to find a dream home for him!

Here are the 3 basic requirements that Sawamura-san was given:

-   Somewhere with a gym close by (preferably Tokyo Metropolitan
    Gymnasium)
-   Somewhere close to Sendagaya Station
-   Somewhere with a monthly rent below 200,000 Yen

After filtering out houses above 200,000 Yen monthly rent Sawamura-san
fitted a multiple linear regression as seen below:

<center>
<img src = "https://i.imgur.com/TvsEmpw.jpg" width = "600" height = "550" />
<center/>
After looking at the diagnostic plots for the model she took out a few
outliers that she confirmed was mainly due to incorrect data on the
housing website and was able to cut her list down to around 70 houses!
Then using leaflet Sawamura-san mapped out all the potential houses that
fit her criteria and labelled them with details about the
house/apartment.

<!-- ![]() -->
After doing the analysis, she showed it to her co-worker and got him to
take a look around. Unfortunately, the information provided by the
website didn’t account for things such as construction work, cleanliness
and safety of the neighborhood, along with the added bonus of having to
live with the landlord. So this case study was also a great reminder
about the necessity of doing some field work in addition to analytics!

### Using external C/C++ libraries with R! - [Wataru Iwasaki](https://twitter.com/heavywatal)

-   [Slides (in
    English!)](https://heavywatal.github.io/slides/japanr2018/)

**Wataru Iwasaki** loves using C++ and R, he has given talks on the
subject [before](https://heavywatal.github.io/slides/tokyor71/) and this
time was no different as he talked about incorporating and using C/C++
libraries with R. First, he introduced a number of great online
resources for developing `Rcpp` packages including stuff from his own
website as well as the free [“Rcpp for Everyone (English
version)”](https://teuder.github.io/rcpp4everyone_en/) written by fellow
Japanese R user [Masaki Tsuda](https://twitter.com/teuder).

<center>
<img src = "https://i.imgur.com/WvOGgHa.jpg" width = "550" height = "500"  />
<center/>
Next, he talked about a couple of basic steps needed to incorporate
C/C++ libraries as well as the advantages and disadvantages of the
various styles of doing so.

<center>
<img src = "https://i.imgur.com/AtAILYt.jpg" width = "550" height = "500"  />
<center/>
In Iwasaki-san’s concluding remarks he called on the community to share
their knowledge of handling external C++ libraries via social media or
through blog posts.

### Build an R compiler…with R! - [igjit](https://twitter.com/igjit)

-   [Slides](https://igjit.github.io/slides/2018/12/nrc/#/)

For this presentation `@igjit` told us about his attempt at creating an
R compiler written in R! You can see the fruits of his labor in the
`nrc` package that he created [here](https://github.com/igjit/nrc).
**Note**: currently it only works on Linux so you should use something
like Docker if you want to try it out on other OSs.

Here are some examples:

Simple addition:

<center>
<img src = "https://i.imgur.com/xlBhBA3.jpg" width = "550" height = "500" />
<center/>
You can even assign and use variables! (the function that got cut off is
`execute`):

<center>
<img src = "https://i.imgur.com/pZePhpc.jpg" width = "550" height = "500" />
<center/>
I unfortunately don’t have much experience with compilers so it was
tough for me to understand the technical details but it was another
pretty cool example of how you can use R for just about anything!

### Tennis Player Ratings with R! - [flaty13](https://twitter.com/flaty13)

-   [Slides](https://docs.google.com/presentation/d/1QSm7EDgNk7OeLWb266LZ57787v0tybirQ3Kr5A9cmHA/edit#slide=id.p)
-   [Code](https://github.com/flaty4218/20181117_TennisAnalysis)

In the second use of R in sports analysis we had `@flaty13` take a look
at tennis player ELO ratings. After a brief introduction relating to
tennis, ELO ratings, and his views on the difficulty of rating/ranking
tennis players, he used a data set from Kaggle and the `PlayerRatings`
package to conjure up some visualizations on tennis player rankings over
time.

<center>
<img src = "https://i.imgur.com/zU0oUGD.jpg" width = "650" height = "600"  />
<center/>
As a matter of course, he also looked at **Kei Nishikori**’s performance
and highlighted his rapid rise in the rankings during 2014 where he
became the first Asian to reach a [Grand Slam tournament
final](https://en.wikipedia.org/wiki/2014_US_Open_%E2%80%93_Men%27s_Singles)!

<center>
<img src = "https://i.imgur.com/RyE4xhk.jpg" width = "650" height = "600"  />
<center/>
Overall, it was nice to see how sports analytics have grown these past
few years in Japan as besides this tennis presentation and the rugby
presentation earlier there have been presentations relating to soccer
and baseball analytics at past TokyoR meetups.

Conclusion
==========

Following both the main talks and the LTs, sushi and drinks were served
at the after-party as R users from all over Japan shared their stories
of success and struggle alike!

The main organizer, [Atsushi Hayakawa](https://twitter.com/gepuro)
mentioned that he eventually wants **JapanR** to grow even bigger in the
coming years and to have every participant give a LT! Whether as a joke
or if that is actually feasible it would be cool if we set the *Guiness
World Record for Most Presentations at an R Conference*!

As you saw the quality of presentations at JapanR was very high.
Unfortunately, most of the content was only in Japanese which I thought
was a shame. That’s why I thought of doing this to share the knowledge
of **Japanese R Users** to those around the world! This is my first time
writing up one of these and I hope to contribute more and improve in the
years to come!

If you’re ever in Japan, come join us for some R&R … and R!
