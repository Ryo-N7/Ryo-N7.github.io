---
layout: post
title: "The JapanR Conference 2018 Round-Up!"
fb-img: https://i.imgur.com/YZXPElx.png
share-img: https://i.imgur.com/YZXPElx.png
tags: [japan, japanr, community, tokyor]
---

This past weekend was the **9th JapanR Conference** hosted at [LINE
Corporation](https://linecorp.com/en/) in Tokyo, Japan\!

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
Wickham](https://twitter.com/hadleywickham) visited Japan\!

  - Want to learn more about **TokyoR** and when the next meeting is?
    Check this [link](https://tokyor.connpass.com/)\! (Next meeting is
    January 19th, 2019)
  - Want to learn more about **JapanR**? Check this
    [link](http://japanr.net/)\!

This time around I took the time to take notes on the presentations and
write up a little round-up blog post about it. As much as I would like
to write about every single presentation there were a number of topics
where I really wouldn’t have been able to explain well even if the
presentation were done in English\! You can watch most of the
presentations on the [JapanR YouTube
channel](https://www.youtube.com/channel/UCXKQBlJczU7YTyVu_wW7yHA).
Although the talks are in **Japanese** maybe you’ll still find something
useful in their slides… or you can read on as I give a summary on around
9 (out of 22) presentations that I found interesting\!

**NOTE**: Some people presented using their Twitter/online name only,
it’s just a cultural thing I’ve found here relating to privacy.

**NOTE 2**: There are still several presentations/slides that haven’t
been uploaded yet but I will put more screenshots in as they become
available so please check back in the coming
days\!

# The Presentations

### Creating your own RMarkdown template\! - [Kazuhiro Maeda](https://twitter.com/kazutan)

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
R Markdown document and clicks on a plot image, et Voila\! It pops up
very nicely\!

Since I wasn’t able to translate the template creation process well
enough (live-translating technical stuff is hard\!), I will leave some
good links to creating your own R Markdown template in English below:

  - [Document
    Templates](https://bookdown.org/yihui/rmarkdown/document-templates.html)
    chapter from Yihui Xie’s **R Markdown: The Definitive Guide**
  - A [list](http://jianghao.wang/post/2017-12-08-rmarkdown-templates/)
    of R Markdown template packages from Jianghao Wang
  - An example: the R markdown templates used by [Monash University
    Department of Econometrics and Business
    Statistics](https://github.com/robjhyndman/MonashEBSTemplates)
  - A short [tutorial](http://ismayc.github.io/ecots2k16/template_pkg/)
    by Chester
Ismay

### Easy and modern data analysis with **“R AnalyticFlow”**\! - [Ryota Suzuki](https://www.ef-prime.com/index_en.html)

**Ryota Suzuki**, CEO of
[ef-prime](https://www.ef-prime.com/index_en.html) and author of the
[pvclust](http://stat.sys.i.kyoto-u.ac.jp/prog/pvclust/) package, gave a
talk on [R AnalyticFlow](https://r.analyticflow.com/en/) which is a free
software that his company built that utilizes the R environment for
statistical computing in a GUI format. **R AnalyticFlow** was created in
Java and is compatible with Windows, Mac, and Linux OSs as well as being
available in English, Japanese, Chinese, and many more
languages.

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
you know your way around Java and want to help, let him
know\!

### I have completely understood Shiny\! - [Med\_KU](https://twitter.com/Med_KU)

In what was a very lively and fun presentation, `@Med_KU` took us
through a very comprehensive tour of Shiny apps. First he talked about
how to create a Shiny app via R Studio, working with the app.R and ui.R
files, and publishing through R Studio Connect. Afterwards, he went
through many examples with `plotly` and `googleVis` showing all the
interactive/reactive capabilities that Shiny apps are known for.
Personally, I’m more of a `ggiraph` fan myself (I use it at work for
flexdashboards and Shiny apps) but `@Med_KU`’s presentation has gotten
me interested in trying `googleVis` out as well\!

I recommend watching the
[recording](https://www.youtube.com/watch?v=sXXXsb1MNMk&feature=youtu.be&t=6928)
of the presentation as `@Med_KU` goes through a lot of different
examples\!

### DID Analysis with R\! - [Yuki Yagi](https://twitter.com/Yagi__Bei)

University student **Yuki Yagi** presented on DID (Difference in differences) analysis and how he utilized it in one of his research papers. For those unfamiliar, DID is a statistical technique that observes the differential effect of a treatment (training program, medication intake, etc.) on a treatment group vs. a control group. A quick overview of DID can be found [here](https://www.mailman.columbia.edu/research/population-health-methods/difference-difference-estimation). 

The main question that Yagi-san investigated in his research paper was: "What would be the impact on the number of patents produced when research subsidies were given to companies that were already highly skilled and had a track record of producing many patents."

<center> <img src="https://i.imgur.com/l3MQoUu.jpg" width="650" height="600" /> <center/>

DID is really easy to understand given the above diagram. On the left hand side is the measurement of the outcome variable, in this case the number of patents before the treatment, while on the right is the measurement of the number of patents after the treatment (research subsidies) were given to the treatment group (blue dot is the control and red dot is the treatment group). 

<center> <img src="https://i.imgur.com/555oM5Z.jpg" width="650" height="600" /> <center/>

Above is how the model looked like for the research question with the use of dummy variables, B (subsidy), C (post-treatment), and D (subsidy + post-treatment). 

### Rugby Analytics with R\! - [Koichi Kinoshita](https://twitter.com/K_Shoppi)

**Koichi Kinoshita**, a rugby performance analyst for the [HITO-Communications Sunwolves](https://sunwolves.or.jp/en/) and the Northland Rugby Union (in New Zealand), gave a presentation on how he applied his nascent R skills to his favorite sport. After giving a brief explanation about the state of sports analytics in rugby and his resolve to improve his data analytics skills in R, he showed us a number of plots from data he gathered from the Japanese national rugby league website. 

THroughout the presentation Kinoshita-san tried to answer several questions such as "*Is tackling percentage related to lost tries?*", "*Do a higher number of tackles help stop line-breaks?*", "*Can you stop line-breaks if you have a higher tackle success percentage?*" among others as he explained his results in thorough detail using plots as a visual aid. Ultimately, his data showed that those Japanese rugby teams with over i6% tackle success rate were able to limit line-breaks to 10 or less and were very likely to win matches while those teams with a tackle success rate of below 78% mostly wound up losing. 