---
layout: post
title: "My first R package building experience: Reflections from creating bulletchartr!"
fb-img: https://i.imgur.com/8FrfaRWm.png
share-img: https://i.imgur.com/8FrfaRWm.png
tags: [r-packages, data-viz, bulletchartr, r-bloggers]
---

I haven't been able to make a blog post in a while (my blog post on [cherry blossoms](https://ryo-n7.github.io/2018-04-02-sakura-surprise/) earlier this month was more of a big update)! Since my last [post](https://ryo-n7.github.io/2018-01-12-japan-postwar-economic-recovery/) I: moved back to Tokyo, went to the [RStudio Conference](https://www.rstudio.com/resources/videos/rstudioconf-2018-talks/) in San Diego, AND started my data analyst/viz internship at [ACDI/VOCA](http://www.acdivoca.org/)! As part of my internship, I was tasked with creating a package for visualizing KPIs with [bullet charts](https://www.perceptualedge.com/articles/misc/Bullet_Graph_Design_Spec.pIndicatorData). Working with my supervisor, [Amit Kohli](http://amitkohli.com/) we developed `bulletchartr`, based off of the ephemeral `ggplot2`, which allows one to create different versions of bullet charts with either a R data frame or Excel file input! You can read the intro article [here](http://www.acdivoca.org/2018/03/introducing-the-monitoring-and-evaluation-bullet-chart/) and/or check out the Git Hub repo [here](https://github.com/ACDIVOCATech/bulletchartr)! Here's a look at one of the bullet charts that you can make with `bullet_chart()`:

![](https://i.imgur.com/8FrfaRW.png)

Today I wanted to talk a bit about my R package building experience and showcase some of the things that really helped me out!

When I first proposed we turn our set of bullet chart functions into a full-blown package I noted that I had a lot of preparation to do. The first source of information I looked into was of course, Hadley Wickham's ["R Packages"](http://r-pkgs.had.co.nz/) book! After confirming with Amit that we will work on this exciting project, I proceeded to read most of it in the weekend that followed. From chapters on `documentation` to `compiled code` it gave me a good overview on what I needed to do and I frequently referred back to it throughout the package building process.

`Git` it done!
--------------

For most of my time working with R, I was mainly doing things by/for myself; Doing projects to showcase on my blog, doing analyses for my dissertation, etc. So this was also a great opportunity to collaborate on a R-related project for the first time. As I'm in Tokyo and Amit is in London, our communication was purely online as we bounced ideas off each other and let each other know of issues and possible ideas not just through Skype but also through commit messages and Git repo issues. A handy trick I learned was that you can close and reference `Issues` in the commit message!

![](https://i.imgur.com/K8RC5gI.jpg)

To see a full list of the keywords to close an issue check [this](https://help.github.com/articles/closing-issues-using-keywords/) help page!

Recently I saw [this](https://suzan.rbind.io/2018/03/reflections-4-months-of-github/) article which talked about using the `Git Bash` console for handling your version control. Although the RStudio Git Hub panel is quite good and gets the majority of things done (indeed, I still use it most of the time), sometimes, as I'll show below, may necessitate learning how to use Git through the console as well!

Originally, the repo for bulletchartr was on my account Ryo-N7, however, as an official work project it had to be moved to the ACDI/VOCATech account. To do this I first had to `transfer ownership` on Git Hub (via the "Settings" tab), then for my local copy I had to change the remote repository url using:

-   `git remote set-url origin https://github.com/Ryo-N7/ACDIVOCATech/bulletchartr.git`

Just for the sake of being thorough, here are the steps to check your repo, stage any changes, commit with a message, and then push to origin (make sure you have Git installed on your computer first)!

1.  Go to the where the local copy of your repo is and right-click to pop up the menu, then click "Git Bash Here" (this should automatically open Git Bash and have it pointed right at the folder you want without having to change directories!)
2.  `git status` to check whether your branch is up-to-date with origin/master, look at what files are unstaged, etc.
3.  `git add .` or `git add -A` to stage all changed files, if you only want to add a specific file you can type `git add file1 file2` . For more detailed explanation of `git add` variants look [here](https://stackoverflow.com/questions/572549/difference-between-git-add-a-and-git-add?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)
4.  `git commit -m "my git commit message here"`, pretty self explanatory, main thing is the `-m` to add a message! This isn't the best way to add a commit message/title as you can't make new lines and go into great detail.
5.  `git push` to update!

Bottom line is don't just use the RStudio Git Hub panel! Practice and master using the console to have better control over what you push, pull, commit, revert, etc.!

Building the functions
----------------------

A little bit more about actually building the package itself. After the first few days, the basic bare bones plots themselves were ready, however more work was needed to polish it up for a proper "alpha version" release. As `bulletchartr` is a visualization package, the code was divided mainly into two steps:

1.  Building the internal "calculation" function: To reduce the work that the user needs to do and to avoid repeating the calculations every time for each `bullet_chart_*()` function, we decided to have all the calculations be done by an internal function. The function transforms the various input values into percentages in relation to both the target and time of the year as well as creating the custom labels for the plot.

2.  Building the plotting functions: The bulk of the plotting code came from setting the aesthetics of the various `geom_col()`s as well as extensive usage of `theme()` to set up the textual information. Most of the time taken for this part was figuring out the layering order as well as figuring out how to best implement the intuitive defaults for options such as "legend", "small version" (so one could preview the bullet charts in the windowed RStudio `Plots` panel without having to open it up in a new window), and "fiscal calendar type". More features will be added in the next versions!

By transitioning from making this package simply for the people at ACDI/VOCA to the R community, it became apparent that I needed the function to allow custom inputs. Which leads us to the next section...

Working with tidyeval
---------------------

Working on bulletchartr was the first time I used tidyeval, I've been hearing about it for ages but usually skipped over reading articles about it as I really had no clue what was going on. My first real introduction to it was Hadley's [talk](https://www.rstudio.com/resources/videos/tidy-eval-programming-with-dplyr-tidyr-and-ggplot2/) on it at the RStudio Conference a few months ago.

To make it easier for people to use the functions we used tidyeval to allow users to import data sets/excel files with their own column names.

![](https://i.imgur.com/soyVQVJ.jpg)

Then in the function call we ask users to specify those column names to the corresponding bulletchartr column names through tidyeval.

![](https://i.imgur.com/3M4dNnt.jpg)

When a user enters their own variable names into the arguments, under-the-hood the `bullet_chart()` function uses `enquo()` to quote them and turned them into quosures. These quosures allow the function to capture user input as an expression. Then, when these are called to create the data frame (still within the function), we use the !! operator to "explode" them as variables without quotations. so that they'll be properly read and used by the function to turn them into the columns for our data set.

![](https://i.imgur.com/TgasoHu.jpg)

[Here](https://www.rstudio.com/resources/webinars/tidy-eval/) is a great vid from RStudio that really made me understand tidy eval after multiple failed attempts, especially if you didn't understand my explanation above (sorry, I'm almost to the point of being able to explain it in my own words)!

Rockin' roxygen!
----------------

What's the point of having a nice package if people have no idea how to use it? To make the documentation process easier to help both users and authors is the [roxygen2](https://cran.r-project.org/web/packages/roxygen2/vignettes/roxygen2.html) package! With this our documentation is in the same place as our functions so we won't forget to update them whenever we change bits of code! As an added bonus, we no longer need to manually change the man files. All we have to do is add new comments above our code with `#'` at the start of every line and then `roxygenize()`!

In addition to this, the add-in "`createOxygen`" from the [sinew](https://metrumresearchgroup.github.io/sinew/createoxygen-static.html) package allows you to automatically create a nice template or "skeleton" of the type of topics that should be in a help page. All you need to do is to run your function once to commit it to memory, highlight the function name, then click `createOxygen` from the *Addins* tab in RStudio to create a roxygen template that is ready-to-go!

With all this in mind, you now have a nice workflow for building packages:

1.  Build code/functions
2.  Run your functions once to commit it into memory (as in it shows up in your `Global Environment`)
3.  Highlight the function name and click on the `sinew::createOxygen` addin
4.  Update documentation
5.  `roxygen2::roxygenize()` 
6. `Install & Restart`: Build your package! [(Optional): `devtools::check()`]
7.  git commit & push!

Style your code with `lintr`!
-----------------------------

Writing code is not just a "science" but in some ways an "art" as well. Having clean, well-formatted, consistent code may seem like an arduous extra step but in the long-term it is a good habit to have. In terms of coding style, this becomes doubly important when you are collaborating as you'll need to decide with your fellow collaborators on what coding style to use and you'll have to learn to accommodate contrasting styles! As, above all, you want to be consistent throughout your package to make it both easier to read and maintainable not just for others, but for your future self! Even still, no one has time to comb line-by-line through their code but fear not, there are packages that can do it for you! One package that can help is the [lintr](https://github.com/jimhester/lintr) package by Jim Hester! By running for example:

``` r
# install.packages("lintr")
lint("R/bullet_chart_functions.r")
```

It will look at each line of the file specified and highlight any problems for you, like so:

![](https://i.imgur.com/c8070Y3.jpg)

Other great packages include [styler](https://github.com/r-lib/styler), which will automatically style your code (according to the tidyverse formatting rules) as well as the [Lintr Bot](http://www.masalmon.eu/2018/03/30/lintr-bot/) which will comment on Pull Requests for R Packages on the Git Hub repo if you have a `lintr` unit test in it!

Package etc.
------------

A few quick comments about other aspects of building a package:

-   A lot of the `devtools` functions automatically creates certain directories/files/etc. for you! Here are some that I used:

``` r
# create testing infrastructure: "tests/testthat.r", "tests/testthat/ folder"
devtools::uses_testthat()

# add files and lines in description for declaring package to be distributed under GPL v3 license:
devtools::use_gpl3_license()

# ease the process of saving package data in correct format:
devtools::use_data()
```

-   DESCRIPTION file: One example of something to be careful about here is to make sure you have the correct version of dependencies in the `IMPORT` section as well as having the correct `>=` or `>` signs.

-   Bugs: I ran into a lot of bugs in my code. Some that I made were things forgetting a comma to separate function arguments and mixing up when to use `=` or `==`. Others like not placing certain arguments inside or outside `aes()` as well as making sure I had the `geoms`, `themes`, etc. in the correct order! Though a lot of these are small silly mistakes, they can become increasingly frustrating as they begin to pile up, especially when you've been working on stuff for a few hours! When silly mistakes start popping up regularly, it might be time to take a bit of a breather, **relax**!

-   License: I ended up just choosing what `ggplot2` had as our code is mainly based on that...! Remember to read documentation of packages you're using as dependencies for your own package! Here's a good [website](https://choosealicense.com/) for comparing licenses.

Beyond the first release:
-------------------------

Just because you released your package doesn't mean you can just sit back and relax, the real work begins here! Immediately after our first mini-release, showcasing our bullet charts to the various project managers at ACDI/VOCA, we got feedback on several issues along with a few things we noticed we were lacking. One of those things was cutting down duplicate code in our plotting functions for when we incorporated the `small` and `legend` options. This was important because as we develop this package further, we don't want to be changing code in multiple places to keep everything consistent. As I've said many times throughout this blog post, we want to make things easier for ourselves and any collaborators in the future!

Another important thing to note when creating a package/set of visualization tools for a client (in this case the various project managers at ACDI/VOCA) is that you need to be flexible towards the concerns of the end users. What's important is not what you, personally, think is the best visualization strategy or presentation but to think from the perspective of those who will actually be using the product/package/service on a daily basis, post-release. An example of this is concerning having **legends** in the plot. From my perspective, I thought it would really clog up the visualization, so I opted to do away with them all together especially since the graphs were quite intuitive (and a legend would be redundant, again in my opinion). However, the end-users really wanted them so after a quick discussion we added them in as an option, `legend = TRUE/FALSE`!

Currently I am trying to fix a few things up but you should still be able to download via `devtools::install_github("ACDIVOCATech/bulletchartr")` and try it out! I should have finished this article a few weeks ago (when we actually released the alpha version along with the ACDI/VOCA blog article) buuuttt.... life happens! While its important to take heed of this [article](https://medium.com/indeed-data-science/marketing-for-data-science-a-7-step-go-to-market-plan-for-your-next-data-product-60c034c34d55) concerning timing your PR/marketing with your product releases, I say - well, better late than never!

Next version will allow full customization of the bullet\_chart variables courtesy of `tidyeval`, as in you don't have to only use proxy variables such as "last year" or "last week" and you could maybe make your own `bullet_chart` graph with "daily" as your time unit! The alpha version is quite limited in what it can intake and output at the moment but improving that is the main goal for the next version!

Hopefully this recollection of random tips, tricks, and my thoughts of my package building experience can be helpful to would-be novice package developers in the future. This was a great experience for me and I hope to create more `R` packages in the future!

