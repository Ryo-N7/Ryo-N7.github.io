---
layout: post
title: "J.League Soccer 2022 Mid-Season Review!"
fb-img: https://imgur.com/WJ8mCoH.png
share-img: https://imgur.com/WJ8mCoH.png
tags: [japan, jleague, soccer, football, ggplot2, tidyverse]
---

-   [Introduction](#introduction)
-   [League table](#league-table)
-   [Team Reviews](#team-reviews)
    -   [Cerezo Osaka](#cerezo-osaka)
    -   [Shimizu S-Pulse](#shimizu-s-pulse)
    -   [Vissel Kobe](#vissel-kobe)
    -   [Kawasaki Frontale](#kawasaki-frontale)
    -   [Kashiwa Reysol](#kashiwa-reysol)
    -   [Kashima Antlers](#kashima-antlers)
    -   [Yokohama F. Marinos](#yokohama-f-marinos)
    -   [Nagoya Grampus](#nagoya-grampus)
    -   [Shonan Bellmare](#shonan-bellmare)
    -   [FC Tokyo](#fc-tokyo)
    -   [Gamba Osaka](#gamba-osaka)
    -   [Consadole Sapporo](#consadole-sapporo)
    -   [Urawa Reds](#urawa-reds)
    -   [Kyoto Sanga](#kyoto-sanga)
    -   [Sagan Tosu](#sagan-tosu)
    -   [Avispa Fukuoka](#avispa-fukuoka)
    -   [Sanfrecce Hiroshima](#sanfrecce-hiroshima)
    -   [Jubilo Iwata](#jubilo-iwata)
-   [Data Visualizations](#data-visualizations)
    -   [Squad Age Profiles](#squad-age-profiles)
    -   [Time Interval](#time-interval)
    -   [Scoring Situations](#scoring-situations)
    -   [Team Shot Quantity](#team-shot-quantity)
    -   [Team Shot Quality](#team-shot-quality)
    -   [5 Match Rolling Averages:](#match-rolling-averages)
        -   [Goals vs. Goals Against](#goals-vs.-goals-against)
        -   [xG vs. xGA](#xg-vs.-xga)
        -   [xG vs. Goals](#xg-vs.-goals)
        -   [xGA vs. Goals Against](#xga-vs.-goals-against)
    -   [xG Difference](#xg-difference)
-   [Conclusion](#conclusion)

# Introduction

A new year, a new season of the J.League! This is yet another condensed
season due to the 2022 World Cup in Qatar happening in late November \~
December, just about overlapping with the time the J.League usually
finishes so fans and players alike get yet another busy schedule. We are
now in the 30th season of the J.League and although COVID related
measures are still largely in place, things are slowly getting back to
normal with bigger crowds and hopefully soon, fans will start being
allowed to cheer again if the trials in the next few months are
successful. This season has seen **Jubilo Iwata** and **Kyoto Sanga**
join J1, their first time back to the premier competition level in 3
years and 12 years respectively. As has become tradition in the last few
years, this is the mid-season review of the J.League where I look at how
teams are doing using both **data** and **watching the games** (or the
eye-test or whatever other term you want to use).

For these blog posts that I create I would ideally use data from
WyScout, InStat, etc. to take advantage of their detailed stats
(expected goals, progressive passes, etc.) especially to look at
player-level data and match that up with my own notes from watching the
games and of course the tagged/organized video footage that these
platforms provide (especially as DAZN only keeps matches up online for
about a month until they are archived forever into the abyss…).
Unfortunately, all of that costs *$$$*. I do all of this as a hobby and
I can’t justify the expense (it’s not the $ but more importantly the
**time** to make full use of purchasing an account). So, I am only using
data from free websites which do not have as much detail. Thankfully, I
have been able to find a bit more on a player and team level from a
variety of new sources. Once again, a big *arigato* to websites like
[Transfermarkt](https://www.transfermarkt.com/),
[Sporteria](https://sporteria.jp/),
[Football-Lab](https://www.football-lab.jp/),
[FBref](https://fbref.com/en/), and more! As always, you can always
check **where** I got the **data** from my taking a look at the bottom
corners of any viz.

Since last year I’ve been heavily relying on the
[TACTICALista](https://app.tacticalista.com/#/) app to create tactics
diagrams/animations. You’ll see a lot of them in the team summary
sections and I urge you to check it out, it’s really great. For those of
you familiar with [my previous
work](https://ryo-n7.github.io/2018-06-29-visualize-worldcup/), I
would’ve liked to remain on brand and create soccer-related
diagrams/animations with {ggplot2} and {gganimate} but… that would’ve
taken a loooong time so I have been using a program that’s actually
built for this kind of thing instead.

I’ll be very happy if any J.League bloggers (as long as there’s no pay
wall or anything) want to use any of the viz I’ve made in this blog post
with proper credit along with a link to their work (as I’d love to read
more English J.League content). Some of the viz can be created for J2
and J3 teams as well so please don’t hesitate to reach out if you want
me to do so!

Before I start just a few notes:

-   To keep up to date with all of what’s happening in J1, I made a
    giant Twitter thread of lots of cool informed people to follow on
    **Twitter** for English language/international J.League content.
    [You can find it
    here!!!](https://twitter.com/R_by_Ryo/status/1493180532603383815)
-   While I have become a FC Tokyo fan since returning to Japan a few
    years back, this review is meant to be as **objective** as possible
    and I do try my best to be impartial.
-   I can’t watch **every** match for **every team** but I do try to
    watch around **80%** of all J1 games in a given season. Of those
    games I do watch I’m almost always taking detailed notes on them to
    review later, re-watching them, etc.
-   All of the shots and xG related stuff you see in the viz are
    **non-penalty** stats. Exceptions are stuff like the time interval
    and scoring situations plots.
-   My views come from watching **only J1 league matches** as most cup
    games clash with my work schedule and I can’t be bothered to
    subscribe to yet another streaming service. The things I talk about
    here are primarily based on the **J1 league** with occasional
    references to cup competitions.
-   Again, I am doing this all on my **own free time**. This latest one
    is probably my biggest yet but it’s honestly becoming a huge time
    sink (as much as I do enjoy doing this), so I may need to cut down
    on content for future releases. This has been a labor of love but
    there are limits and I need to start making some more compromises on
    top of the ones I’ve been making already.

Let’s get started!

# League table

There’s a clear top 3 then a huge jumble of good-but-inconsistent teams
that, if they can improve a few things, can actually challenge for the
top! **Sanfrecce Hiroshima** and **Kashiwa Reysol** look the most likely
to either challenge for the final ACL spot or even **Sagan Tosu** if
they can figure out how to score more and convert their draws into wins.
In the relegation battle are some unexpected guests in **Urawa Reds**
and **Vissel Kobe** along with relegation candidate regulars in
**Shimizu S-Pulse** and **Shonan Bellmare**. Some other poor teams (in
my opinion) like **Consadole Sapporo** and **Jubilo Iwata** may count
themselves lucky that they are managing to keep themselves above water…
for now!

<details>
<summary>
<b>Click to show R code!</b>
</summary>
<pre>

```r
# library(dplyr)
# library(knitr)
# library(kableExtra)

jleague_table_2022_mid_cleaned <- read.csv(
  file = "https://raw.githubusercontent.com/Ryo-N7/soccer_ggplots/master/data/jleague_2022_mid/jleague_table_2022_mid_cleaned.csv")

jleague_kable_table <- jleague_table_2022_mid_cleaned %>% 
  knitr::kable(format = "html", 
               caption = "J.League 2022 - League Table (After Matchday 16)") %>% 
  kable_styling(full_width = FALSE,
                bootstrap_options = c("condensed", "responsive")) %>% 
  add_header_above(c(" ", "Result" = 5, "Goals" = 3,
                     "Expected Goals" = 3)) %>% 
  column_spec(1:2, bold = TRUE) %>% 
  row_spec(1, bold = TRUE, color = "white", background = "green") %>% 
  row_spec(2:3, bold = TRUE, color = "grey", background = "lightgreen") %>% 
  row_spec(4:15, bold = TRUE, color = "grey", background = "white") %>% 
  row_spec(16, bold = TRUE, color = "white", background = "orange") %>% 
  row_spec(17:18, color = "white", background = "red") %>% 
  add_footnote(label = "Data: FBref.com & Sporteria | Gamba vs. Sanfrecce postponed due to COVID outbreak | All xG values do not include penalties",
               notation = "none")
```
</pre>
</details>
<table class="table table-condensed table-responsive" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>
J.League 2022 - League Table (After Matchday 16)
</caption>
<thead>
<tr>
<th style="empty-cells: hide;border-bottom:hidden;" colspan="1">
</th>
<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="5">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

Result

</div>

</th>
<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="3">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

Goals

</div>

</th>
<th style="border-bottom:hidden;padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="3">

<div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">

Expected Goals

</div>

</th>
</tr>
<tr>
<th style="text-align:left;">
Team
</th>
<th style="text-align:right;">
Matches
</th>
<th style="text-align:right;">
W
</th>
<th style="text-align:right;">
D
</th>
<th style="text-align:right;">
L
</th>
<th style="text-align:right;">
Pts
</th>
<th style="text-align:right;">
GF
</th>
<th style="text-align:right;">
GA
</th>
<th style="text-align:right;">
GD
</th>
<th style="text-align:right;">
xG
</th>
<th style="text-align:right;">
xGA
</th>
<th style="text-align:right;">
xGDiff
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: white !important;background-color: green !important;">
Yokohama Marinos
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white !important;background-color: green !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: green !important;">
9
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: green !important;">
4
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: green !important;">
3
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: green !important;">
31
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: green !important;">
30
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: green !important;">
17
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: green !important;">
13
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: green !important;">
24.81
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: green !important;">
17.63
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: green !important;">
7.18
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
Kashima Antlers
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
9
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
3
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
4
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
30
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
27
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
21
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
6
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
21.32
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
18.03
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
3.29
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
Kawasaki Frontale
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
9
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
3
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
4
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
30
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
20
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
17
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
3
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
16.39
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
17.22
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: lightgreen !important;">
-0.83
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
Kashiwa Reysol
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
8
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
3
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
5
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
27
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
22
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
14
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
8
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
20.98
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
15.67
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
5.31
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
Cerezo Osaka
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
7
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
5
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
4
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
26
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
23
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
7
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
19.94
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
19.82
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
0.12
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
FC Tokyo
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
7
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
4
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
5
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
25
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
18
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
14
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
4
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
15.94
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
18.75
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
-2.81
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
Sanfrecce Hiroshima
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
15
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
6
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
6
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
3
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
24
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
19
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
13
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
6
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
20.69
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
14.22
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
6.47
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
Sagan Tosu
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
5
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
9
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
2
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
24
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
21
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
5
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
16.60
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
15.79
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
0.81
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
Kyoto Sanga
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
5
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
5
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
6
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
20
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
18
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
-2
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
15.51
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
23.54
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
-8.03
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
Nagoya Grampus
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
5
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
5
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
6
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
20
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
14
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
-2
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
19.38
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
15.75
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
3.63
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
Consadole Sapporo
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
4
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
8
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
4
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
20
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
15
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
26
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
-11
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
20.56
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
23.15
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
-2.59
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
Avispa Fukuoka
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
4
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
7
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
5
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
19
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
11
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
10
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
1
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
17.10
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
15.82
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
1.28
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
Gamba Osaka
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
15
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
4
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
5
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
6
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
17
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
17
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
20
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
-3
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
16.18
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
21.48
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
-5.30
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
Urawa Reds
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
2
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
9
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
5
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
15
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
15
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
-1
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
19.51
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
14.77
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
4.74
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
Jubilo Iwata
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: grey !important;background-color: white !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
3
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
6
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
7
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
15
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
18
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
25
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
-7
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
16.00
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
24.05
</td>
<td style="text-align:right;font-weight: bold;color: grey !important;background-color: white !important;">
-8.05
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;font-weight: bold;color: white !important;background-color: orange !important;">
Shimizu S-Pulse
</td>
<td style="text-align:right;font-weight: bold;font-weight: bold;color: white !important;background-color: orange !important;">
16
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: orange !important;">
2
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: orange !important;">
7
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: orange !important;">
7
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: orange !important;">
13
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: orange !important;">
15
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: orange !important;">
24
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: orange !important;">
-9
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: orange !important;">
18.88
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: orange !important;">
20.30
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: orange !important;">
-1.42
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;color: white !important;background-color: red !important;">
Shonan Bellmare
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: red !important;">
16
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
3
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
4
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
9
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
13
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
13
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
23
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
-10
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
15.90
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
18.31
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
-2.41
</td>
</tr>
<tr>
<td style="text-align:left;font-weight: bold;color: white !important;background-color: red !important;">
Vissel Kobe
</td>
<td style="text-align:right;font-weight: bold;color: white !important;background-color: red !important;">
16
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
2
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
5
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
9
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
11
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
14
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
22
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
-8
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
19.90
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
21.29
</td>
<td style="text-align:right;color: white !important;background-color: red !important;">
-1.39
</td>
</tr>
</tbody>
<tfoot>
<tr>
<td style="padding: 0; border:0;" colspan="100%">
<sup></sup> Data: FBref.com & Sporteria \| Gamba vs. Sanfrecce postponed
due to COVID outbreak \| All xG values do not include penalties
</td>
</tr>
</tfoot>
</table>

# Team Reviews

I’ve gone for an approach to integrate everything (both the data viz and
the tactics stuff) for **every team** into its own section. Therefore,
if you want an explainer to the data viz you’ll need to jump down to the
`Data Visualizations` section to learn more. Hopefully the specific
context I provide when presenting each viz for a particular team I’m
talking about can give you the right idea though.

## Cerezo Osaka

Cerezo in **Akio Kogiku’s** first full season in charge (he replaced
**Levir Culpi** in summer 2021) are up in 5th spot, but with a mediocre
record of 7 wins, 5 draws, and 4 losses. With the loss of key players in
winger **Tatsuhiro Sakamoto** and defender **Ayumu Seko** (both gone to
seek adventure in Europe for Oostende and Grasshoppers respectively),
the Osaka side had quite a busy transfer window as they also sought to
start refreshing and lowering the average age of their squad. With the
likes of **Tiago Pagnussat**, **Yoshito Okubo**, **Naoyuki Fujita**,
**Toshiyuki Takagi**, and **Riki Matsuda** (all close or over 30)
leaving they brought in the likes of **Sho Funaki**, **Seiya Maikuma**,
**Tokuma Suzuki** (who impressed me at relegated Vortis last season),
and **Jean Patric**. Other more experienced players include **Ryosuke
Yamanaka**, the return of **Bruno Mendes**, and **Hikaru Nakahara**.
Another notable slightly late arrival has been the return of fan
favorite **Matej Jonjic** in defense giving **Ryuya Nishio** a talented
and more experienced partner to rely on.

![CZO squad age
profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_CerezoOsaka_2022_mid_EN.png)

Most of their season has seen very inconsistent results with Cerezo not
able to string two consecutive wins until late May. Besides a 0-3
reverse against Kashima Antlers they’ve been able to be in touching
distance of most of their opponents throughout a match, although some of
their performances in these games may not actually reflect these close
results. It certainly hasn’t been all sunshine and sakuras at the
`Yodokou Sakura Stadium` with star player **Takashi Inui** banned for 6
games due to frustration over Kogiku’s management of the team after
being substituted off in a game against Kashiwa Reysol in April.

![CZO
xGDifference](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/CerezoOsaka_2022_mid_xgdiff_logo.png)

**How do Cerezo Osaka play?**

Cerezo generally shape up in a 4-4-2 or a 4-2-3-1 with **Hiroshi
Kiyotake** playing behind any of their target man type strikers. In
defense they keep a solid 4-4 mid-block shifting across from
side-to-side in unison and trying to keep gaps between players to a
minimum. The strikers are also expected to have a high work-rate off the
ball as they are tasked with being Cerezo’s first line of defense. An
important aspect of their defending is to prevent passes back inside
after the opponent has passed the ball wide in the build-up to prevent
opponent Center Midfielders from facing forward and make switches across
the field to threaten Cerezo’s weak side.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/CerezoOsaka/CZO-defend-midblock.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/CerezoOsaka/CZO-defense-holes.png)

Cerezo will try to build the ball out from the back, sometimes with
**Riku Matsuda** shifting inside to form a back 3 and **Ryosuke
Yamanaka** pushing up high on the left. This is done to manipulate
opposition wide midfielders into pressing deeper into Cerezo’s half
while also creating space for Cerezo’s own wide midfielders further up
the pitch. Cerezo can also use **Kim J.H.’s** passing ability to access
players that aren’t covered by an opponent’s initial press or just
simply whack the ball up to the strikers.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/CerezoOsaka/CZO-buildup-KimJH.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/CerezoOsaka/CZO-buildup-up-back-through.png)

Cerezo have gathered a gang of big strikers in **Mutsuki Kato**, **Bruno
Mendes**, **Hiroto Yamada**, and **Adam Taggart** that are all equally
good in the air, can settle the ball with their backs to goal, and also
make runs in-behind defense lines after having laid the ball off to a
supporting player. The supporting players are usually the wide
midfielders that tuck in, trying to anticipate where loose balls might
fall or open spaces to receive a lay-off. As strong as the strikers are
it is a crucial aspect of Cerezo’s game plan that they are always
supported by the likes of **Kiyotake** and **Inui**, who can then in
turn play through balls behind the defense or dribble up field
themselves.

In the final 3rd, **Riki Harakawa** has been very good as the passer to
spread the ball from side-to-side probing defenses while also being
Cerezo’s primary set piece taker. Besides the magic provided by
**Kiyotake** and **Inui**, **Ryosuke Yamanaka** has also been a threat
with his great crossing ability, especially long range early crosses
coming from deep. See examples against
[Kobe](https://www.youtube.com/watch?v=TAAevTRRHj8) and
[S-Pulse](https://www.youtube.com/watch?v=X8aLjkWfCW0) as he has
completely taken over the Left Back spot from veteran **Yusuke
Maruhashi**. The wide midfielders frequently pinching inside to support
the strikers also give space to the fullbacks to bomb forward and launch
these formidable crosses.

With winning ways finally coming in recently, especially a
morale-boosting 3-1 win over local rivals Gamba, could Cerezo make a
push for the final ACL place (3rd)? A lot will rest on the continued
good form of **Kiyotake** along with the return of injury-wracked
**Taggart**, who scored his 1st (and only 2nd in his entire time in
Osaka!) goal of the season against rivals Gamba ~~and a hopefully more
clear-headed Takashi Inui~~ (~~I still have no idea what exactly is
going to happen with Inui considering he has finished serving his ban
but has apparently refused to train~~). NOTE: **Inui** and Cerezo Osaka
have decided to part ways in early June.

## Shimizu S-Pulse

Before I go into detail, I think the best way to describe how S-Pulse’s
season has gone is that manager **Hiroaki Hiraoka** has been **fired**!
S-Pulse have now gone nearly 4 seasons of hiring a new manager,
struggling in a relegation battle, firing that manager, and finally the
new manager or caretaker just about leading them to safety (S-Pulse were
also lucky there was no relegation play-off in 2020 due to COVID as
well), then rinse-and-repeat. It’s not as though S-Pulse are a club with
few resources either, while they may not have the strength of the
absolute top teams in J1, they have been able to splash some cash (well,
relatively speaking) on various players in transfer fees and wages all
throughout the past couple of years. It’s quite a damning indictment of
their top-level administration that they keep swapping and changing
players and managers, then starting all over again once they’ve fired
them. I’m not sure what S-Pulse’s vision or identity is, even more so
because they haven’t actually had any real success on the pitch in the
past 20 years with only **Kenta Hasegawa**’s tenure coming anywhere
close to consistent success (and he still didn’t win a single trophy!).

It’s rather frustrating for a neutral because in the past 2 years
especially, they are clearly some good players in the squad that when
things click they play quite well… but those performances haven’t quite
turned into good results, confidence wanes, then the manager is fired,
…return to the start of my previous paragraph. I wrote quite extensively
about S-Pulse in [last year’s
review](https://ryo-n7.github.io/2021-12-20-jleague-2021-endseason-review/),
mainly noting their inability to finish enough chances besides **Thiago
Santana**, getting hemmed into their own defensive 3rd/box, etc. This
season, unfortunately, while some things have changed, a whole lot of
other things have not.

![SPulse
xGD](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/ShimizuSPulse_2022_mid_xgdiff_logo.png)

**How do Shimizu S-Pulse play?**

I talked in length last year on S-Pulses’ problems getting hemmed into
their own defensive 3rd, and as an attempt at a solution this season,
S-Pulse have been a fair bit more pro-active in defending from the front
and trying to keep the general field of play further away from their own
goal.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShimizuSPulse/SPulse-track-back.png)

But what’s been a bigger game changer is their improvement in building
the ball out from the back. While it’s still not perfect, they are able
to progress much better compared to last season and they don’t have to
fall into the negative loop of chucking the ball away and getting pushed
further and further back toward their own box nearly as often. Playing a
large part of this is **Reon Yamahara**, a 23 year old Left Back who has
the passing and dribbling skills to help S-Pulse evade the opposition
press. Alongside **Eiichiro Katayama** and **Teruki Hara**, S-Pulse have
full backs that are good with the ball at their feet but to get the most
out of them they need to be able to receive higher up the pitch far more
consistently as well.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShimizuSPulse/SPulse-buildup-Yamahara-dribble.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShimizuSPulse/SPulse-buildup-Frontale-evade.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShimizuSPulse/SPulse-buildup-Frontale-evade-2.png)

This is on top of their already excellent attacking ability in
transition, spearheaded by **Yuito Suzuki** (another player I’ve written
on extensively in the past). He is fantastic at finding gaps between the
lines, turning with the ball and carrying it up field. The off-season
purchases of **Ryohei Shirasaki**, **Yuta Kamiya**, and **Katsuhiro
Nakayama** have helped S-Pulse double-down on this style of play.
**Shirasaki** has been a great help assisting **Suzuki** in finding
space or appearing in gaps between the lines himself while
**Nakayama’s** speed has been an asset on the counter.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShimizuSPulse/SPUlse-Yuito-Suzuki-space.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShimizuSPulse/SPulse-buildup-Suzuki-space.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShimizuSPulse/SPulse-Yuito-Suzuki-space-2.png)

However, it hasn’t all been perfect as S-Pulse still do give the ball
away cheaply at times and their blocks of 4 can be dragged apart by
smart movements from opposition as their defense is man-oriented rather
than space-oriented. For example, Center Midfielders have been dragged
away from vital central areas (like in the FC Tokyo game), forced to
cover space behind the Full Backs or the gaps between the
Fullbacks-Center Backs as quick switches of play force Center Backs to
come out wide (vs. Urawa, Cerezo, Tosu, etc.). S-Pulse’s fortunes really
hinge upon their press working and the differences in performance and
results depending on this aspect has been quite stark.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShimizuSPulse/SPulse-block-gaps.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShimizuSPulse/Frontale-transition-attack.png)

Even worse is their inability to defend crosses, despite the likes of
**Valdo**, **Yoshinori Suzuki** (no relation to Yuito), **Yugo
Tatsuta**, and **Shuiichi Gonda** in their back line. The Shizuoka-based
side have conceded 6 from crossing situations and a further 4 from
set-pieces (totaling to around 41% of all of their goals conceded so far
this season).

![SPulse
situations](../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_ShimizuSPulse.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShimizuSPulse/SPulse-CBs-gaps.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShimizuSPulse/SPulse-defense-dragged.gif)

S-Pulse are fortunate that there are quite a few mediocre teams around
them, including the surprisingly poor results from Urawa and Kobe, so
they are still more than capable of turning things around, even with
just a few bounces here or there going their way for once (unlike last
season). Much depends on **Yoshiyuki Shinoda** (2nd time as a caretaker
in the past 3 years!) and how he rallies this set of players. Looking at
their stats, “simply/obviously” they’ll need to decrease the quantity of
opponent shots while also increasing the quality of their own shots at
the opposite end (easier said than done!).

**NOTE**: In the middle of writing this, S-Pulse have announced their
new manager: **Ze Ricardo** from Vasco Da Gama. Apparently he is someone
the S-Pulse hierarchy have been chasing for a few years so it’ll be
interesting to see how he gets on!

![SPulse squad age
profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_ShimizuSPulse_2022_mid_EN.png)

## Vissel Kobe

It has been a disastrous season for Vissel Kobe, with **Atsuhiro Miura**
becoming the first managerial casualty of the season in late March, as
they currently sit at the **bottom** of the league table despite their
best ever league finish last season (3rd)! Their first win of the season
only came in mid-May against Sagan Tosu. There are quite a mix of
reasons for these poor performances but a few main ones stand out. First
a **lack of plan B** even more so now that a big part of Plan A, **Sergi
Samper**, the guy who is pretty much the protagonist of their build-up
play, is out for the season. Also the **lack of squad depth**. Compared
to Marinos who invested significantly into their squad, Kobe mostly
replaced their outgoings. There are still clear lack of backups at Full
Back, square-pegs-in-round-holes (**Takahiro Ogihara** and **Koya
Yuruki** filling unfamiliar roles in a midfield diamond). While
**Yoshinori Muto** and **Yuya Osako** have struck a good partnership up
front since their arrival last summer and largely continue to do so,
this season their other signings such as **Bojan**, **Lincoln**,
**Takahiro Ogihara**, **Shion Inoue**, and **Tomoaki Makino** have
flattered to deceive. Other crucial players such as **Ryuho Kikuchi**
and **Ryo Hatsuse** have been off form, with the former only making a
return from injury in March while the latter has lost his place in the
starting XI.

![squad-age-profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_VisselKobe_2022_mid_EN.png)

**How do Vissel Kobe play?**

With **Sergi Samper**, they had someone who could set the tempo for the
team and be the initiator of attacking moves. Last season manager
**Atsuhiro Miura** finally was able to unlock how to get the best out of
**Andres Iniesta** by turning the midfield into a diamond, with
**Samper** at the base and **Iniesta** at the tip.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/VisselKobe/Kobe-Samper-buildup.gif)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/VisselKobe/Kobe-Samper-buildup-2.gif)

**Samper’s** passing range also allowed Kobe to use their full backs
aggressively and stretch defense as they are usually the only source of
width on the Kobe team. Most of the players would congest the middle,
trying to play quick combinations with each other and get into the box
or find one of the full backs in open space to cross it back into the
box.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/VisselKobe/Kobe-Samper-long-diagonal.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/VisselKobe/Kobe-attack-positioning-before.png)

Following **Samper’s** injury and managerial changes, the new manager
**Miguel Lotina** has shifted Kobe into a 4-4-1-1/4-2-3-1 with
**Iniesta** playing behind the striker. Defense-wise its a
straight-forward 4-4-2 and the high-press was done away with a slightly
more passive approach in a mid-block.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/VisselKobe/Kobe-4-4-block-good.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/VisselKobe/Kobe-4-4-block-gap.png)

However, without **Samper**, ideas in how to build the ball up from the
back have been sparse. **Hotaru Yamaguchi** and **Yuta Goke** have
always played more of a supportive role, making good runs into the final
3rd/box or creating space for others to shine rather than being
play-makers themselves.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/VisselKobe/Kobe-buildup-no-Samper.png)

While in other parts of the field there just aren’t players to set the
right tempo at the right times.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/VisselKobe/Kobe-buildup-speed.png)

Despite the challenges that cloud Kobe, **Iniesta** can still fashion
chances out of nothing.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/VisselKobe/Kobe-Iniesta-magic.png)

The club used the Asian Champions League (ACL) group stages as a chance
to reset and **Miguel Lotina** sought to use the trip to Thailand as a
mini pre-season of sorts. Some signs of life with a return to basics
under their new manager as seen in this [video
analysis](https://twitter.com/QuanTue/status/1527583963631394817) on
their game against Kawasaki Frontale from [Quan
Tue](https://twitter.com/QuanTue). Unfortunately, a romping 4-0 victory
over Sagan Tosu on their return to Japanese soil proved to be a false
dawn as despite a spirited performance against Kawasaki Frontale, they
were outdone by a last minute goal. Things only got worse as after their
disastrous loss against relegation rivals Shonan Bellmare, Shonan
themselves then pulled off a surprise victory over Frontale keeping the
distance between the two bottom side at 2 points. Going into the 2nd
half of the season, the `Rakuten Rovers` are 4 points and a few goal
difference away from **safety**.

![xGD](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/VisselKobe_2022_mid_xgdiff_logo.png)

## Kawasaki Frontale

…Yet another Asian Champions League disappointment, somehow even worse
than last year’s by dropping out in the group stages this time around!
In the league, they’ve been grinding out results despite some
mediocre-at-best performances, mostly on the attacking side of things
where they only seem to be able to manage to score 1\~2 goals at the
best of times (compared to regularly scoring 3-or-more in previous
seasons). However, a lot of those ‘grindy’ wins were off the back of
very good finishing streaks that didn’t quite match up to their
underlying performances. As can be seen below, Frontale have been
consistently scoring above their xG but in the past few games, they are
finally regressing to the point where their goal scoring is more in line
with the quality of shots they are creating.

![Frontale
xG-Goals](../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/KawasakiFrontale_2022_mid_rollingxGGoals_logo.png)

Much has been made of their blow out losses against Shonan, Cerezo, and
Marinos but their defense has been relatively stable otherwise this
season. To me, what’s been their real problem this season has been their
**attack** as their metrics have taken a considerable nose-dive compared
to past seasons! Last season they were still taking a bit over **14
shots** per 90 minutes and also the average quality of their shots
hovered around **0.115** xG/shot (see their position in the ‘green’ top
right corner in last year’s plot on the left). However this season their
shot quantity (**\~12 shots** per 90 minutes) **and** shot quality
(**0.085** xG / shot) have dropped significantly (while the scales along
the axes are different between the plots, see how in general they are
positioned much lower along both x/y axes).

![quadrant
2021](../assets/2021-12-20-jleague-2021-endseason-review_files/quadrant/J-League_2021_end_team_shot_quant_qual_plot.png)

![shot quantity
quality](../assets/2022-06-15-jleague-2022-midseason-review_files/quadrant/J-League_2022_mid_team_shot_quant_qual_plot.png)

They are also just about squeaking by due to proficiency on **set
pieces** (a notable recent example being their last minute win over
Kobe), with 7 goals scored from these situations which amounts to a
whopping **35%** of their total goals scored.

![Frontale goal situation
plot](../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_KawasakiFrontale.png)

**How do Kawasaki Frontale play?**

With the departures of the likes of **Ao Tanaka**, **Reo Hatate**, and
**Hidemasa Morita** in the past few seasons Frontale’s midfield has had
to go through an evolution. While **Kento Tachibanada** emerged as
**Morita’s** clear successor while **Yasuto Wakisaka** has continued to
excel (especially as a pass receiver), a big question marked remained on
who would become the 3rd man in the midfield 3 after **Hatate’s**
departure to Celtic. In came the Thai superstar, **Chanathip
Songkrasin**. His game at Consadole Sapporo was to drop deep to pick up
the ball and carry or pass it into the final 3rd or box and was given a
lot of freedom by **Mischa Petrovic** as to how he did that. While his
first appearance for Frontale was in the Super Cup, where he was oddly
playing out on the wing, in league play he has been playing as one of
the box-to-box midfielders.

However in the first league game of the season against FC Tokyo, with
both **Chanathip** and **Ryota Oshima** on the field, they were both
trying to drop too much to support Frontale’s defense in the build-up.
This created large distances between the midfield and forward lines
where and while **Leandro Damiao** was good at holding the ball up, he
still needed more support from the midfield.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KawasakiFrontale/Frontale-Chanathip-integrate-1.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KawasakiFrontale/Frontale-Chanathip-integrate-2.png)

In later games with **Kento Tachibanada** back in the engine room,
Frontale’s midfield has looked a lot more balanced like last season.
**Chanathip** has been busy getting involved in Frontale’s signature
quick passing combinations to escape opponent’s pressing.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KawasakiFrontale/Frontale-Tachibanada-defense.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KawasakiFrontale/Frontale-pass-combos-1.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KawasakiFrontale/Frontale-pass-combos-2.png)

On their day, Frontale can still look very good but it’s been **far less
of a consistent feature** this season with a noticeable lack of
chemistry between the attack and midfield at times being a very real
concern. Unfortunately, due to injury since early April **Chanathip**
hasn’t really seen much league action, so only time will tell how he
continues to integrate fully into Frontale’s midfield. The main
benefactor of **Chanathip** and **Oshima’s** injury as well as **Tatsuki
Seko** seemingly not impressing manager **Tohru Oniki** enough, has been
**Daiya Tono** who has been able to assert himself as a starting member
of the squad. He has the added bonus of being able to play behind the
striker too when Frontale want to switch to a double-pivot by throwing
in **Joao Schmidt** next to **Tachibanada**.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KawasakiFrontale/Frontale-transition-attack.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KawasakiFrontale/Frontale-pass-grain.gif)

While unlike the attack, the defense has held mainly firm so far this
season (including **Jung S.R.’s** good performances in between the
sticks) but it’s really defending from the front, Frontale’s famous
pressing, that just doesn’t seem to have the same kind of killer edge as
it had in previous seasons. This was quite noticeable in games against
**Shimizu S-Pulse**, **Yokohama F. Marinos**, and **FC Tokyo**.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KawasakiFrontale/Frontale-press-evaded.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KawasakiFrontale/Frontale-press-evaded-2.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KawasakiFrontale/Frontale-press-evaded-3.png)

On the other side of the ball, teams have made Frontale suffer in the
build-up phase by matching up against Frontale’s defensive midfielder
(**Tachibanada**) and the two Center Backs. With these concerns in mind,
the other midfielders also try to drop to help out but this makes the
problem worse by restricting the space available for the CBs to perform
any sort of evasive maneuvers against the press by dribbling out. With
**Shintaro Kurumaya** being the only left footed CB Frontale have, it’s
been difficult for **Shogo Taniguchi** on the left side paired with
**Kazuya Yamamura** to find good passing angles forward. This only
highlights the importance of **Shintaro Kurumaya**, who only came back
from injury in early May, as his ability to carry the ball up field from
the back and his good passing has been a lifeline for the Frontale
defense line.

Out on the right, **Miki Yamane** looks **tired** (this was already a
problem last season… but obviously now its gotten worse especially as
he’s made numerous appearances for the national team too). At Left Back,
**Asahi Sasaki** has shown some promise at various points but is clearly
not ready to be starting week-in week-out at the J1 level but again,
there’s no one to replace him as the usual starter **Kyohei Noborizato**
has been fighting off various injuries all season.

A major concern is in attack as **Leandro Damiao**… seems to be slowing
down? The Brazilian’s shot numbers have decreased considerably from
averaging around over 3 shots per 90 the past few seasons but this year
his shot production has dropped into the low 2 shots per 90 level. Is he
not getting into good positions or are teammates unable to get the ball
to him? **A little bit of both**? Without better data and a closer
inspection of **Damiao** on video I can’t make any conclusions but
there’s clearly **something** going on here that warrants further
investigation. It’s also worth noting that **Damiao’s** back-ups are an
ever-aging **Yu Kobayashi** (who also seems to be playing out on the
Right Wing more frequently these days) as well as **Kei Chinen** who has
mainly played a bit part role throughout his career. Clearly a new young
or at least younger striker is going to be necessary soon, even if
**Damiao** returns to form. Possibly **Taisei Miyashiro**, but his loan
at Sagan Tosu this season has not gone nearly as well as his time at
Tokushima Vortis last season.

Looking at the squad age profile below, it’s very telling how little
Frontale are using their squad. A good chunk of the players taking up a
majority of the minutes are way into their 30s, while recent signings in
their ‘peak’ years have either been injured or not played as much for
various reasons. **Tatsuki Seko**, who impressed for Yokohama FC last
season has barely had a look in while depth signings (that I thought
were quite smart signings at the beginning of last year) like **Kazuki
Kozuka** and **Koki Tsukagawa** are either injured, not trusted, or
thrown in as emergency defenders.

![Frontale squad age
profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_KawasakiFrontale_2022_mid_EN.png)

The silky smooth quick exchanges of passes in the final 3rd and around
the box, the coordinated and intense pressing just hasn’t been seen as
much this season compared to the past. They are still in the title race
as the teams around them continue to trip themselves over as well. It is
concerning that the cracks seen last season weren’t solved at all and
now have grown bigger and bigger as a result. Frontale are holding on to
their top 3 stop by the skin of their teeth this season, as they are
just about getting good results despite quite a few poor performances
throughout the first half of the season. Frontale fans will have to hope
that this over performance (in both attack and defense) doesn’t catch up
to them and that their actual performances improve to match their
results soon.

(Sorry that the designs are completely different but I think you can get
the idea… you want more of your games to be below the diagonal line)
Last season:

![Frontale 2021
xGD](../assets/2021-12-20-jleague-2021-endseason-review_files/xGDiff/KawasakiFrontale_2021_end_xgdiff_logo.png)

This season:

![Frontale 2022
xGD](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/KawasakiFrontale_2022_mid_xgdiff_logo.png)

## Kashiwa Reysol

Kashiwa Reysol have surprised pretty much everybody, including me, over
some good results at the start of the season. Their 2021 season was
extremely poor in my opinion and it did feel like **Cristiano** (who has
since dropped down to J2 team, V-Varen Nagasaki) broke them out of jail
more than a few times at crucial turning points in games. With
**Cristiano’s** departure and the post-Olunga/post-Esaka transfers not
working out well at all, it really did seem like to me that Reysol’s
days in J1 were numbered. However, manager **Nelsinho** has finally
found a formula to Reysol’s woes by sticking to a back 3 / back 5,
whereas last season he kept swapping between a back 3 and a back 4 in
what seemed like between every game.

While **red cards** for opponents in some of their early games certainly
helped, they still had to press their advantage and were usually well
worth the 3 points they collected at the end of these games. After a
trial-by-fire rookie season in professional football, **Mao Hosoya** has
used last year’s experience to really break through and become the focal
point in attack for Reysol with the departure of long time talisman
**Cristiano** which has also earned him national team call-ups. Also
crucial has been the stellar form of **Matheus Savio**, who in 2020
suffered a very bad injury and looked quite far from his best on his
return last season. **Tomoya Koyamatsu** who impressed so many last
season for Tosu has continued his good form for his new side, mainly
supporting the striker or in the midfield engine room. Another thing to
note has been **Nelsinho’s** use of youth players with **Kaito Mori**,
**Yugo Masukake**, **Masato Sasaki**, and **Hidetaka Maie** getting
minutes or at least a place on the bench.

![Reysol squad age
profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_KashiwaReysol_2022_mid_EN.png)

**How do Kashiwa Reysol play?**

After vacillating between a back 4 and back 3\~5 last year, **Nelsinho**
has fully stuck to a 3-5-2 or 3-4-2-1 system this season. A strong
coordinated press has been the identity of this team with one of the
strikers leading the opponent defenders toward the sides where the
Reysol midfield and the ball-near wing back jump out with intensity to
trap opponents against the sideline. The other will usually sit deeper
by closely marking the ball-near center midfielder to prevent them from
receiving the ball in the center.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-press.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-press-3.png)

Alongside creating high turnovers, Reysol are very quick and vertical in
transition. Both **Matheus Savio** and **Mao Hosoya** have been the
driving force in attack with their line-breaking dribbles and runs into
space.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-Savio-carry-Hosoya-run.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-fast-counter-Savio-carry.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-B2B-runs.png)

However, teams have been able to evade Reysol’s press in certain games.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-press-nullify.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-press-nullify-2.png)

Opponents can use Reysol’s forward momentum against them, making them
run, stretching the distances between their players, and exploiting the
gaps that appear.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-gaps-midfield-evade-press.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-gaps-midfield-evade-press-2.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-Shiihashi-lured-away.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-DF-pulled-apart.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-CB-lured-forward.png)

**Nelsinho** therefore has also put a lot of effort into getting Reysol
to also be able to build out from the back (**Taiyo Koga** being
instrumental in this, being comfortable with both feet) for when their
pressing strategy to attack doesn’t work, with mixed results.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-buildup-success.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-buildup-fail.png)

**Hosoya** is frequently called upon to be the escape route, his
strength against opponent Center Backs providing a platform for lay-offs
to midfielders and then to gain territory up the field.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-buildup-Hosoya-layoff-switch.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-Hosoya-receive-layoff.png)

However, **Hosoya** can also become isolated when opponent Center Backs
can dominate him physically, which can push Reysol back into their own
3rd. As this continues to happen, it can become even harder for
teammates to support **Hosoya** to receive lay-offs or pick up loose
balls which creates a negative cycle of Reysol being progressively
unable to escape their own half.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashiwaReysol/Reysol-pinned-back-def3rd.png)

The return of **Douglas** can’t come soon enough as **Hosoya** has had
to play significant amount of minutes without much rest (not helped by
the fact his good form has resulted in call ups to the national team,
adding to the minutes played). The other striker options just don’t give
the same `oomph` to their attack, especially consistently throughout the
90 minutes. As shown in the tactics section above, in recent games it’s
been fairly easy for the opposition to simply shut down **Hosoya** and
prevent Reysol from making any headway into the opposition half. There
are still concerns over their inability to break down defenses when
their tried-and-true tactic of long balls and quick counters are
nullified by the opposition, but they are well clear of any relegation
battle. With improvements to their build-up capabilities, a challenge
that **Nelsinho** clearly wants to overcome to provide some alternative
to their now predictable method of attack, Reysol may not just keep
their upper-mid table place but even attempt to break into the top 3.

![Reysol
xGD](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/KashiwaReysol_2022_mid_xgdiff_logo.png)

## Kashima Antlers

Kashima Antlers are going through another re-build upon the foundations
built by **Naoki Soma** after he took over from **Antonio Zago’s**
disastrous start to the 2021 season. New manager **Rene Weiler** was
another who arrived in Japan late due to COVID entry restrictions but he
has been quickly putting his own stamp on the team, going for a very
attack-minded 4-4-2. Antlers have had quite a run of good results of
varying levels of performances, with lots of close 1 goal margin games
in the early part of the season… A big loss to Marinos in April was a
stark wake up call that things were still very much work-in-progress.
Alongside their early season loss to Kawasaki Frontale, these results
show this Antlers side still don’t quite have what it takes to go
toe-to-toe with the on-paper “top” sides in the league. But, will this
actually matter though in the long run if they can keep up their good
results by beating up the rest of the league?

![Antlers
xGD](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/KashimaAntlers_2022_mid_xgdiff_logo.png)

The main concern for Kashima is how light they are at **Center Back**.
With various injuries, suspensions, and the poor form of **Kim M.T.**,
**Kento Misao** has been converted to a Center Back! This then has had a
knock-on effect of a lack of Center Midfielders, a problem made a
reality upon **Diego Pituca’s** suspension which left **Yuta Higuchi**
as the only recognizable Center Midfielder (the likes of **Ryotaro
Nakamura** either injured themselves or not trusted yet). **Rene
Weiler’s** solution was to double-down: using **Higuchi** as a single
pivot in a diamond shape, with a supporting cast of the likes of **Ryuji
Izumi** and **Juan Alano** playing slightly more deeper and centrally
than usual. Continued attempts to use **Kim M.T.** in central midfield
(!) since his return from injury has been puzzling to me… and it hasn’t
quite worked out but the Swiss manager seems insistent on continuing
this project.

![Antlers
xG-xGA](../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/KashimaAntlers_2022_mid_rollingxGGA_logo.png)

**How do Kashima Antlers play?**

Antlers play a very intense physical game. Kashima players further back,
such as **Kento Misao** from Center Back play a lot of long balls into
the two strikers, **Yuma Suzuki** and **Ayase Ueda**. Midfield runners
then rush up to support and gather loose balls or receive lay-offs. When
playing the ball long they usually try to aim toward one side so as to
be able to congest play into a small area to create overloads. The
attack is very free form with **Yuma Suzuki** noticeably drifting over
to the Left Wing quite often. This also allows the full back on the
opposite side to be free in lots of space for a possible switch/diagonal
across to the weaker side to push even further into the opponent half.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashimaAntlers/Antlers-Left-Wide-Attack.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashimaAntlers/Kashima-long-ball-Suzuki-drag.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashimaAntlers/Antlers-compress-space-counterpress.png)

Once in the final 3rd, they try to get as many bodies into the box as
possible for crosses from the likes of Full Backs like **Koki Anzai**
and **Keigo Tsunemoto** pushing up in support.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashimaAntlers/Antlers-switch-multiple-runners.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashimaAntlers/Antlers-switch-multiple-runners-2.png)

There is considerable risk in negative transitions (from attack to
defense) by playing this way, as Kashima usually only keep **Higuchi**
as the sole screen for the back line. Manager **Rene Weiler** mitigates
this by employing a very intense counter-press to win the ball back,
which is another reason why Kashima try to congest the wide areas of the
pitch. When the press is broken through, Antlers rush back to form a
low-mid block but they aren’t quite so effective at defending in their
own box. Against teams good in possession Antlers face the risk of
having their strikers isolated from the rest of the team. Further
compounding their problems is that they aren’t that great in
building-out from the back to slowly advance up the pitch and get
support to their strikers in that way (see their games vs. Frontale &
Marinos).

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashimaAntlers/Antlers-buildup-fail-counter.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashimaAntlers/Antlers-tilt-field-fail.png)

Therefore, Kashima’s strategy really hinges on keeping up their
intensity, in winning duels all over the pitch whether it is in midfield
or the Center Backs knocking balls back forward, to keep the field of
play in the opposition half as much as possible.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashimaAntlers/Antlers-press-success.png)

Despite some defensive lapses, **Ikuma Sekigawa** is still having a
decent season although its quite clear he misses a proper Center Back
partner like **Koki Machida** from last season. One of my favorite
aspects of his play is his great one-touch passing from interceptions,
which allow Antlers so much opportunity due to the great speed in
transition that **Sekigawa’s** anticipation and forethought allow
Antlers to catch the opponent completely unready in mid-transition.
Goalkeeper **Kwon S.T.** has also rescued Antlers from more than a few
of their defensive lapses as a very calming veteran presence for the
defense. The Korean took over from **Yuya Oki** late last season as the
youngster’s passing and handling became rather erratic.

Antlers this season haven’t been far from controversy, with **Yuma
Suzuki’s** antics in the Gamba Osaka and FC Tokyo games as well as
**Diego Pituca’s** show of frustration that earned him a lengthy
suspension. Another big question mark this season has been, where is
**Ryotaro Araki**? The winner of the `J.League Rookie of the Year` award
last season has barely seen the pitch in 2022. There was promising signs
of co-existence with **Suzuki** in the Gamba game as they rotate with
each other out on the Left but it seems **Suzuki** has completely taken
over **Araki’s** role as the creator and partner to **Ayase Ueda**. In
May there was news about a hernia operation but as usual with a lot of
Japanese teams, there’s been radio silence for quite some time before
that so one can only assume the hernia or some other injury had been
ruling him out since mid-April.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashimaAntlers/Antlers-Araki-Left-Suzuki-Left.png)

On a more positive note has been the continued rise of **Ayase Ueda**
who, with 10 goals to his name already, has taken over as the league’s
top goal scorer from Peter Utaka in recent games. The static diagrams I
make don’t really do justice to his wonderful movement and exquisite
finishing skill so I’ll leave you to look at his highlight videos on
youtube.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KashimaAntlers/Antlers-Ueda-movement.png)

With rumors swilling around **Ueda’s** potential European transfer,
Antlers fans would hope that fit again **Everaldo** can create a similar
kind of chemistry with **Suzuki** in the coming months as he comes back
to full fitness after a injury-plagued 2021 season. At the other end of
the pitch, if **Weiler** can figure out the defense then with Antlers
only a point behind Marinos going into this international break, the sky
is the limit. In the near future a new Center Back should be a priority
in the market or the likes of **Bueno** or **Naoki Hayashi** start to
gain the trust of the manager, as they are only one or two injuries to
the back line to cause a serious crisis. This may also let **Misao**
back into midfield next to **Higuchi** or **Pituca**. In general this
squad is very top-heavy so sooner or later Antlers will be needing
reinforcements especially if they keep the results up to return to the
ACL next season.

![Antlers squad age
profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_KashimaAntlers_2022_mid_EN.png)

## Yokohama F Marinos

**Kevin Muscat’s** Marinos side is another team that have defied my
expectations. I was honestly **very skeptical** over Marinos after he
took over from Ange Postecoglou as the team really didn’t look up that
great (yes, I say this despite them finishing in 2nd last season). Along
with the departures of key players like **Daizen Maeda** and **Thiago
Martins** (the latter mere weeks before the start of the season), I
didn’t have them challenging for the title at all nor did I believe they
would finish in the ACL places, although I did think they would still be
‘in competition’ for that last ACL spot.

However, watching Marinos this season I have been very impressed. What’s
been a clear intention from **Muscat** has been heavy rotation using as
much of the squad as possible to maintain their **intensity** in every
match. This doesn’t always work out due to chemistry issues from new
combinations of players like in the games against Kashiwa, Sanfrecce,
and Consadole but its something very necessary with the ACL campaign
congesting the already busy J1 schedule. Players both young and old such
as **Ryotaro Tsunoda**, **Yuta Koike**, **Kaina Yoshio**, **Riku
Yamane**, and **Yuki Saneto** have all seen some varying levels of
action on the pitch so far this season, filling in for injuries,
suspensions, or just to give the best players a break.

![Marinos squad age
profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_YokohamaMarinos_2022_mid_EN.png)

**How do Yokohama F. Marinos play?**

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/YokohamaMarinos/Marinos-buildup-principles.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/YokohamaMarinos/Marinos-buildup-GK.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/YokohamaMarinos/Marinos-buildup-fail.png)

Probably the thing you’ll notice most often about Marinos’ build-up is
how narrow the fullbacks can be positioned, being involved more
centrally in midfield and providing the Center Backs access to the
wingers spread out further ahead on the sidelines.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/YokohamaMarinos/Marinos-buildup-1-vertical-halfspace.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/YokohamaMarinos/Marinos-buildup-2-vertical-wide.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/YokohamaMarinos/Marinos-underlap-space-wide.png)

Although of course, they can still sit wide near the sideline as well.
Marinos like to create passing triangles or even diamonds to force
opponents to become disorganized as they quickly pass between them. The
#10, **Marcos Junior**, is excellent at either finding pockets of space
or helping another teammates out by dragging an opponent away.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/YokohamaMarinos/Marinos-diamonds.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/YokohamaMarinos/Marinos-Kida-drag-space.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/YokohamaMarinos/Marinos-Marcos-drag-space.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/YokohamaMarinos/Marinos-Marcos-drag-space-2.png)

A common theme you can see above is how many Marinos attacks end with
crosses or cut-backs into the box. So it’s no surprise that 40% or 12 of
their total goals have come from crossing situations!

![Marinos
situation](../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_YokohamaMarinos.png)

With **Eduardo** having trouble settling in (as the emergency Thiago
Martins replacement) and **Shinnosuke Hatanaka** having various problems
of his own, **Ryotaro Tsunoda** has stepped up to take his chances in
the Center Back role. While it certainly helps that he is left footed,
he has **often** looked reassured at the back on top of his build-up
capabilities. After a rather disappointing time back at Sendai, **Takuma
Nishimura** has found new life again at Marinos. It has helped that he’s
been played far more centrally than he was under **Makoto Teguramori**
as he’s been a perfect squad player filling in either behind the striker
or leading the line himself when **Marcos Junior** or **Anderson Lopes**
has needed a break. One of my favorite players on this team has been
**Tomoki Iwata**, a jack-of-all-trades who can fill in at Center Back,
Center Midfield, and Right Back. **Nishimura** has been excellent
finding pockets of space to receive passes, acting as an escape route
for Marinos as they try to build up from the back. He has contributed in
the opponent half as well, as he is tied 2nd in the team alongside
**Teruhito Nakagawa** on 4 goals scored. **Anderson Lopes** has been
terrific so far but then he got himself banned over spitting in the
Avispa Fukuoka game… Fortunately **Leo Ceara** (who admittedly has not
hit the heights of last season) and **Nishimura** are around to fill in
(again, squad depth!). The Yokohama-based side need to make sure
horrific defensive collapses like against Urawa don’t happen again as
their 1-point lead at the top could have been far more heading into this
June international break. Of the current “top 3”, I think they are the
most polished team based on my experience watching them and the data.
It’ll be interesting to see if their results can continue to match their
performances in the 2nd half of the season.

![Marinos
xGD](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/YokohamaFMarinos_2022_mid_xgdiff_logo.png)

## Nagoya Grampus

**Kenta Hasegawa’s** new job after his FC Tokyo tenure went up in flames
has not gone according to plan. I remarked in last season’s review that
star striker, the guy that literally solved pretty much all of their
goal scoring issues, **Jakub Swierczok**, tested positive for some
illegal substance and has been banned since late 2021 while **Naoki
Maeda**, another important attacking piece, left for FC Utrecht. So it
wasn’t a very positive start before he even rolled up to Nagoya. Their
off-season transfers were somewhat sensible, adding dangerous Sagan Tosu
pair **Keiya Sento** and **Noriyoshi Sakai** and replacing outgoing
**Takuji Yonemoto** with the equally veteran **Leo Silva** being the
highlights.

**Hasegawa** didn’t change too much of the 4-2-3-1 formula deployed by
**Massimo Ficcadenti** to start the season but turgid displays forced
him to change tracks as he moved to a back 3 system by late April. Early
on in his tenure, **Hasegawa** already remarked upon the lack of squad
options to choose from which has been made worse by the formation change
as the squad really wasn’t constructed around a 3-5-2, especially in
center midfield where **Kazuki Nagasawa’s** injury means even fewer
opportunity for rotation for the essential midfield trio of **Sho
Inagaki**, **Leo Silva**, and **Keiya Sento**.

![Grampus squad age
profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_NagoyaGrampus_2022_mid_EN.png)

**How do Nagoya Grampus play?**

For the past few years, Nagoya have successfully played a variant of
4-4-2/4-2-3-1 under **Massimo Ficcadenti** and new manager **Kenta
Hasegawa** started the season largely following this tried-and-tested
formula. But as noted in the previous section, some kind of change had
to be made due to poor form. With the lack of a true threat up
top/centrally as well as the additional defensive demands placed on
**Mateus** when he’s playing out wide, the move to a 3-5-2 was created
in part to push the Brazilian maestro more centrally with the freedom to
drift around and get him on the ball closer to goal. Meanwhile the the
wide areas became the remit of the new wingbacks, such as **Yutaka
Yoshida**, **Ryoya Morishita**, and the converted **Yuki Soma** bombing
up and down the pitch to support both the defense and attack.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/NagoyaGrampus/Grampus-Kakitani-drop.png)

Another new feature as a result of this change in shape was a more
aggressive press with **Yoichiro Kakitani** and **Mateus** leading from
the front, sheperding teams over to the sidelines where **Sento**, if
not the rest of Nagoya’s midfield pushing up in support, along with the
ball-near wing back try to trap them against the sideline.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/NagoyaGrampus/Grampus-high-press.png)

This also has Nagoya playing a much higher line than in previous
seasons, but here **Haruya Fujii** has excelled in covering large
amounts of space especially as **Mitch Langerak** isn’t exactly the
sweeper keeper type.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/NagoyaGrampus/Grampus-Fujii-cover-1.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/NagoyaGrampus/Grampus-Fujii-cover-2.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/NagoyaGrampus/Grampus-pressing-highline.png)

The midfielders, mainly **Leo Silva**, **Sho Inagaki**, and **Keiya
Sento** have slowly developed good chemistry as the engine room trio.
They have slowly developed a balance of when/who drops and who pushes up
to support the attack.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/NagoyaGrampus/Grampus-midfield-movement.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/NagoyaGrampus/Grampus-midfield-support.png)

Their recent results have picked up going into the June international
break, and while on one hand I don’t think the performances were
anything particularly noteworthy, you can commend them for showing some
‘character’ squeaking out wins a man down vs. Fukuoka and in injury time
vs. S-Pulse. I still remain skeptical of this team without further
reinforcements, getting more help for **Mateus** in attack (transfers or
**Noriyoshi Sakai** finding some semblance of form) and also padding out
the squad with more J1 level players (so not the likes of **Takuya
Uchida**). Their defense in the new back 3 or 5 shape looks quite solid,
with the performances of **Fujii** in particular standing out as the
most central defender in the back line. It does look like Nagoya are
finding their footing in this new formation and performances are
improving somewhat. An interesting summer awaits and we’ll see if Nagoya
can dip into the transfer market to bolster their squad as with the
grueling summer fixtures on the horizon, this thin squad is a few key
injuries from real trouble.

![Grampus
xGD](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/NagoyaGrampus_2022_mid_xgdiff_logo.png)

## Shonan Bellmare

Another year, another season of struggle for Shonan Bellmare. After
escaping relegation by the skin of their teeth last year, the
Hiratsuka-based side were surprisingly able to hold on to their highly
coveted young stars such as **Taiga Hata**, **Satoshi Tanaka**, and
**Shuto Machino** while **Kosei Tani’s** medium-long term loan from
Gamba Osaka was extended yet again. Their incoming transfers in the
off-season were intriguing with the return of **Ryota Nagaki** and the
acquisition of veteran **Takuji Yonemoto** from Nagoya Grampus (which to
my disappointment has led to 19 year old **Taiyo Hiraoka** not getting a
whole lot of minutes this season…). Yet, they didn’t really address
their main problem from last year which was finding a reliable source of
goals, with only versatile Reysol attacker **Yusuke Segawa** coming into
the team. So, it really shouldn’t surprise anybody that Shonan have yet
again struggled for goals as despite their energetic press creating
opportunities, they have struggled to then convert those opportunities
into good quality chances. Even when they create some chances they just
don’t seem to be able to finish (again, a recurring theme from last
year) or in their anxiety to score they rush shots or squander good
opportunities from good positions.

![Shonan
xG-Goals](../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/ShonanBellmare_2022_mid_rollingxGGoals_logo.png)

**How do Shonan Bellmare play?**

The thing you’ll notice immediately when you watch Shonan is their
highly aggressive press. There are many examples from last year’s review
that I created so I’ll refer you to those, like the one below:

![Vegalta-Shonan-11.20.21](../assets/2021-12-20-jleague-2021-endseason-review_files/diagrams/SB/SB-VS-Hiraoka-intercept.png)

Good teams, like Marinos below, can still work their way around them
though. Swinging the ball side-to-side, forcing Shonan’s lines to shift
back-and-forth until a large gap appears on the opposite side for a
switch ball into space. Also note that their midfield 3 can’t cover the
entire width of the field easily so a lot of work is put on their
shoulders to be able to shift over in time.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShonanBellmare/Bellmare-shift-across.png)

Bellmare themselves are capable of doing this too, with **Satoshi
Tanaka** integral to their build-up. Further up field, **Shuto Machino**
performs a lot of dropping movements to find space between the lines
while **Tarik Elyounoussi** is fantastic at quick combinations to
release players into space following a ball reception or take-on in a
congested area.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShonanBellmare/Bellmare-Machino-drop-Hata-run.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShonanBellmare/Bellmare-buildup-Hata-run.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShonanBellmare/Bellmare-longball-Tarik-support.png)

Shonan’s back line also chooses their moments carefully to push up field
in support of the attack, making late runs to surprise defenses caught
inattentive or to simply provide another option when Shonan are able to
settle the ball in the final 3rd.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShonanBellmare/Bellmare-Hata-counter.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ShonanBellmare/Bellmare-layers-attack.png)

**Satoshi Tanaka** and **Taiga Hata** are good young players with plenty
of upside, both of whom have been called up to the youth national setups
in the past few years. Worryingly, **Tanaka** hasn’t really been at his
best this season while **Hata** has once again battled injury problems
as he missed around a month and a half with a MCL issue. I don’t have
too much to add from what I wrote on them last year so please read
[those
sections](https://ryo-n7.github.io/2021-12-20-jleague-2021-endseason-review/)
if you’re particularly interested in them.

With the relatively lack of resources available at Shonan its
understandable that they are usually in the relegation battle but the
past two years have shown they can perform well, its just the results
that haven’t followed. There’s not much hope for significant incoming
transfers so one will have to bank on the goal scoring touch coming from
somewhere within the squad whether its Wellington or more likely **Shuto
Machino**, who has already topped his previous goal record (4 in 2021)
with 6 goals halfway through the season.

![squad age
profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_ShonanBellmare_2022_mid_EN.png)

## FC Tokyo

Mixi’s takeover from long-time sponsors Tokyo Gas was finally completed
in late 2021 and a new era for FC Tokyo began. From J2 side Albirex
Niigata came a new Spanish manager, **Albert Puig**, who also has had
experience leading Barcelona’s academy setup. It’s been a rough
transition period for FC Tokyo to conform to a completely different
style of play compared to the previous years under **Kenta Hasegawa**.
Despite a series of good results to start off the season (although it
should be noted how close these games actually were), performances on
the attacking side of things wavered as both shots and goals dried up
when FC Tokyo’s attempts at build-up were continuously thwarted.

When zooming out away from individual matches where things looked rocky,
FC Tokyo do have one of the meanest defenses in the league, conceding
only 14 goals (tied 3rd best) but it should be noted that they have
conceded chances worth 18.75 non-penalty expected goals against (xGA).
The one saving grace throughout some troubled times during April and May
were the last ditch defending from the likes of new Center Back signing
**Yasuki Kimoto** and veteran **Masato Morishige** as well as the
fantastic saves of new goalkeeper, **Jakub Slowik**.

![shot against quantity
quality](../assets/2022-06-15-jleague-2022-midseason-review_files/quadrant/J-League_2022_mid_team_shot_against_quant_qual_plot.png)

A clear issue as seen below has been the quantity of shots taken, and
when diving deeper into the individual shot numbers, things are
concerning especially for striker **Diego Oliveira**. The Brazilian’s
shot production has gradually decreased all throughout his time at FC
Tokyo, which makes sense given that Tokyo acquired him right around in
his ‘peak’ years and he is now well over 30 years old.

**Data according to FBref after MD 16**

-   2018: `2.84` shots per 90 minutes (age 27-28)
-   2019: `2.67` shots per 90 (age 28-29)
-   2020: `1.90` shots per 90 (age 29-30)
-   2021: `1.85` shots per 90 (age 30-31)
-   2022: `1.26` shots per 90 (age 31-32) - after around 14 90s played

It hasn’t all been down to him of course, at times he has looked
increasingly isolated up front as balls are booted up to him from
harried defenders looking to launch the ball away under pressure without
midfielders like **Shuto Abe** or **Kuryu Matsuki** in a good position
to pick up loose balls or receive the Brazilian’s lay-offs. This has had
a doubly negative effect of FC Tokyo then being hemmed deeper and deeper
into their own half, causing Tokyo defenders to be under more pressure
and the negative cycle continues as they have to boot it away again.
Also we shouldn’t discount all of **Diego’s on-ball and off-ball work**
that he does outside of shooting and scoring as his ability to combine
with other players around him, especially with Brazilian teammates
**Adailton** and **Leandro** (the `'O Tridente'`) as well as his
defensive work rate (mainly looking after the opponent’s central
midfielder in the opponent’s build up).

However, if your main striker isn’t taking shots then **somebody** has
to pick up the slack and FC Tokyo only has one in Left Winger
**Adailton** with 3.49 shots per 90 and there is a huge chasm between
**Adailton** and the rest of the team. The next few players, who have
also played a significant amount of minutes (when using per 90 stats you
always need to use a ‘minimum minutes played’ threshold or you’re
considering people who’ve played 9 minutes and taken 2 shots and wow
he’s got 22.5 shots per 90, which is nonsense), are **Kensuke Nagai** on
1.16 shots per 90 (from 9.5 90s played) and **Shuto Abe** at 1.03 shots
per 90 (from 15.5 90s played). Ideally, FC Tokyo will want both **Kuryu
Matsuki**, **Shuto Abe**, and at least the other winger to start getting
more shots in addition to creating chances in the final 3rd.

**Most** good-to-great teams (be they in the J.League or elsewhere) will
consistently have at least 2\~4 players with over 2 or even 3 shots per
90. Check out [Yokohama F.
Marinos](https://fbref.com/en/squads/3ded797c/Yokohama-F-Marinos-Stats)
or [Kashima
Antlers](https://fbref.com/en/squads/dd694b37/Kashima-Antlers-Stats) on
FBref’s shooting section or even look further afield to the top teams in
Europe for comparison. Of course, this isn’t even considering the actual
quality of shots **Diego** or any other FC Tokyo player is taking, and
while I do have team-level xG data, I unfortunately don’t have
individual level data for comparison. So below I’ll just show you where
FC Tokyo falls when considering team level shot quality and team level
shot quantity. The best teams are obviously taking lots of shots that
are also of good quality.

![shot quantity
quality](../assets/2022-06-15-jleague-2022-midseason-review_files/quadrant/J-League_2022_mid_team_shot_quant_qual_plot.png)

**How do FC Tokyo play?**

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-Press-Aoki-cover.gif)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/Marinos-buildup-fail.png)

On the ball, FC Tokyo have challenged themselves under manager **Albert
Puig** to try and build the ball up from the back as much as possible.
There have been a lot of struggles but during this transition period
it’s to be expected.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-buildup-success-Matsuki-Adailton.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-buildup-attack-1.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-buildup-fail-backline.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-buildup-fail-sideline.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-buildup-fail-sideline-2.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-buildup-pressed-fail.png)

I was concerned with **Jakub Slowik’s** signing, as good-if-not-great of
a shot stopper he is, I didn’t really understand why FC Tokyo would get
him alongside hiring **Albert Puig**. His shot stopping has been
excellent as ever, saving Tokyo more than a few points and his kicking
has teetered between bad-to-OK. There definitely have been times where
his excellent saves have only occurred as a because of his poor passing
in the first place (with the rest of the defense also partly to blame
too by putting him in uncomfortable situations). I’m not going to make
more of a fuss because he’s largely been great and at this point the
manager just has to deal with the hands (or gloves in this case) that
he’s been dealt with. There are definitely ways to mitigate this issue
and it’ll be interesting to see how much **Slowik** can improve and/or
how FC Tokyo’s defenders try to make it as easy as possible for Slowik
to contribute to the build-up (it’s a team game after all!).

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-Slowik-kicking.png)

FC Tokyo’s box-to-box midfielders are crucial to the new style of play.
**Shuto Abe** and **Kuryu Matsuki** have been excellent so far but as
mentioned above, FC Tokyo will need more from them in terms of output in
the final 3rd to support and relieve the goal scoring burden on **Diego
Oliveira**.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-B2B-midfielders.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-Adailton-deep-Abe-runners.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-longball-transition.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-buildup-attack-2-layoff-Diego.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-Matsuki-Abe-runs.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-buildup-layoff-Abe-run.png)

Although, it is a worry that there aren’t a whole lot of backups in
their position to relieve them. **Keigo Higashi** doesn’t really have
the aggression or mobility and in fact he’s been played as the single
pivot instead recently where he’s looked surprisingly good.

![squad-age-profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_FCTokyo_2022_mid_EN.png)

**Matsuki** in particular has struck up a great partnership with
**Adailton** on the Left. For a guy that was only playing at the high
school level a mere half a year ago, it’s been surprising how good
**Matsuki** has fit into the professional setting. While in the
beginning he accumulated quite a lot of fouls as his timing was off (he
was suspended for getting 5 yellows quite early into the season), he’s
gradually gotten up to speed on the defensive side of things as well.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-high-press-success.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-Matsuki-Adailton-counter.png)

At worst, they can use **Yasuki Kimoto** and **Masato Morishige’s**
excellent long passing range to try and get their fast wingers behind
the opponent’s high line.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-Kimoto-longball.png)

**Ryoma Watanabe** had an injury-ravaged 2021 season but he’s looked to
make his mark in the new era. He’s played at Right Back, midfield, and
on the wing as he bring a lot of positional fluidity to FC Tokyo,
floating around to confuse opponent markers and contributing to easing
Tokyo’s build-up troubles.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-buildup-fluid-Ryoma.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-Ryoma-between-lines.gif)

Some signs of improvement in FC Tokyo’s build-up were seen in the wins
against S-Pulse and Antlers leading up to the international break. While
scoring goals is still a concern, being able to consistently deliver the
ball into the final 3rd and box to shoot should drastically improve FC
Tokyo’s fortunes in front of goal. With longtime Left Back **Ryoya
Ogawa** leaving for Europe (Vitoria Guimaraes), there will have to be a
bit more shuffling around at the back with **Yuto Nagatomo** most likely
moving over to the left and **Hotaka Nakamura** becoming a more
permanent fixture in the line-up. It took **Hotaka Nakamura** quite a
while to break into the team this year but in recent games he’s looked
quite good so he has already stepped up to the plate.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-buildup-success-Aoki-Hotaka.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/FCTokyo/FCT-press-success-high-across.png)

On the topic of stepping up to the plate, it will be interesting to see
whether **Kashif Bangunagande** can break into the team and usurp
**Ogawa/Nagatomo’s** position at Left Back in the near future (for a
deeper dive into **Kashif**, I wrote about him in [last year’s
mid-season
review](https://ryo-n7.github.io/2021-07-26-jleague-2021-midseason-review/)).
**Puig** has built a good foundation so far, and despite the clear
struggles as the team gets more and more used to the way the new manager
wants to play, this will hopefully lead to improved performances in the
2nd Half of the season.

![FCT
xGD](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/FCT_2022_mid_xgdiff_logo.png)

## Gamba Osaka

**Tomohiro Katanosaka** came into the Gamba hot seat amidst much fanfare
after having led the unfancied Oita Trinita side to a Emperor’s Cup
final. Although in the league the Kyushu-based side were relegated to J2
in the process, one has to remember that he was able to bring them up
all the way from J3 and keep them in J1 for 3 seasons without a whole
lot of resources at his disposal. However, it hasn’t been smooth sailing
for Gamba as they sit in 13th, 4 points off the drop albeit with a game
in hand due to the game against Sanfrecce being cancelled due to a COVID
outbreak. It’s been quite a bumpy inconsistent ride, which has not been
helped by a horrendous injury malaise plaguing the squad along with
several separate COVID scares. Particular lowlights have been key player
**Takashi Usami** ruled out for the season with a ruptured achilles in
March while main goalkeeper **Masaaki Higashiguchi** will only be back
to full fitness in mid/late June.

![squad age
profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_GambaOsaka_2022_mid_EN.png)

As seen in the above graphic, these issues have forced **Katanosaka** to
use a variety of youth players to fill out the bench or even the
starting XI at times throughout the season. Nevertheless, this hasn’t
excused some rather poor performances as the players are only able to
sometimes fulfill the requirements needed for `Katano-soccer` to work.

**How do Gamba Osaka play?**

The slow but methodical build-up play that characterized
**Katanosaka’s** Oita Trinita side has not been seen. This has been a
problem for quite some time now at Gamba with players such as **Genta
Miura**, **Gen Shoji**, etc. while all very capable defenders, aren’t
very good at passing or carrying the ball up-field from the back. To try
and solve this **Katanosaka** has rotated just about every defender
Gamba have into the back 3 to varying degrees of success.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/GambaOsaka/Gamba-pass-backline-fail.png)

This has resulted in more and more midfielders trying to drop deep,
creating large gaps between the defense/midfield and the attackers so
that even when the likes of **Hiroto Yamami**, **Jiro Nakamura**,
**Kosuke Onose**, and **Yuya Fukuda** are able to get the ball in the
final 3rd (still usually out wide rather than in dangerous central
areas), they are outnumbered and lose the ball before reinforcements can
arrive.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/GambaOsaka/Gamba-buildup-early.png)

As the season has gone by and more work done on the training ground,
Gamba have achieved a bit more cohesion in what they want to do, but
again the execution has been a bit lacking with the occasional times
where it **clicks**.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/GambaOsaka/Gamba-buildup-shape.png)

In previous years, Gamba had **Usami** and **Patric** pretty much able
to bring attacks to completion (either a shot or earn a corner) by their
own individual quality alone but **Usami** is out for the year, while
**Patric** and fellow Brazilian striker **Leandro Pereira** have not
been effective.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/GambaOsaka/Gamba-Usami-spread.png)

Both Brazilian strikers are used to settle long balls but have no one to
play to, forced to make isolated runs down the channels, and asked to
hold up the ball under a lot of pressure with support taking too long to
help. For a good chunk of the season, even when Gamba are able to get
from the defensive 3rd to the middle 3rd, there hasn’t been a clear
consistent method to get from the final 3rd and into the box (if they
can even get to the final 3rd in the first place). Many times they can’t
even get out of their own defensive 3rd because of the aforementioned
poor ball-playing abilities of all of their Center Backs.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/GambaOsaka/Gamba-buildup-lack-support-2nd-phase.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/GambaOsaka/Gamba-break-press-then-what.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/GambaOsaka/Gamba-buildup-half-spaces.png)

For all the problems outlined above, a thing to note has been that
**Katanosaka’s** in-game management has usually been quite good, with
quick adjustments to fix problems such as against Urawa (switching to a
5-4-1 from 4-3-3), Reysol (3-4-2-1 from 4-4-2). If you’re being overly
harsh, you could turn around and say that the original plans against
these teams have been off the mark as well.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/GambaOsaka/Gamba-Katanosaka-change-1.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/GambaOsaka/Gamba-Katanosaka-change-2.png)

With **Usami’s** very likely season-ending injury, Gamba needed somebody
or somebodies to stand up to fill his creative boots. Surprisingly, it
was not any of the other veteran players but the Osaka-based side have
come to rely on some fantastic performances of young stars like **Jiro
Nakamura** and **Hiroto Yamami** (the latter has also been designated as
one of Gamba’s primary set piece takers already due to his deadly
accurate right foot). As great as they have been, they are still very
young and inexperienced so they aren’t always going to be consistent.
Banking a lot on these young guys to be able to perform week-in week-out
is a tough ask and just about scraping results from superb bits of
individual play (like screamers from one of the few good recent Gamba
signings, **Dawhan** or heroic goalkeeping performances from the likes
of **Jun Ichimori** and **Kei Ishikawa**) is not very sustainable.

This is why one can begin to question Gamba’s signings (again, with a
few exceptions like **Dawhan**), as multiple attempts to move away from
the dependency on **Patric/Usami** have largely failed. The likes of
**Wellington Silva**, **Tiago Alves**, **Leandro Pereira**, **Hideki
Ishige**, **Ju Se-jong**, among others have all come with certain
expectations and they haven’t met them at all. This is on top of the
fact that main squad members of past few seasons don’t look nearly as
effective without **Usami** such as **Kosuke Onose**, **Yuya Fukuda**,
**Yuki Yamamoto**, **Shu Kurata**, and more. **Usami’s** absence has
really had an impact on this team as they can’t rely on his very good
floor-raising ability to drag teammates up a few levels. As an aside, if
you want to learn more about the the concepts of ‘floor-raisers’ and
‘ceiling-raisers’ as they apply to soccer, I urge you to check out [Om
Arvind](https://twitter.com/OmVAsports)’s blog post: [How Basketball Can
Help Us Understand Football: Introducing ‘Floor Raising’ & ‘Ceiling
Raising’](https://tacticalrant.substack.com/p/basketball-football-floor-ceiling-raising).

On a more positive note, the energetic and aggressive midfield pairing
of **Mitsuki Saito** and **Dawhan** has been quite good but mainly in
transition-heavy games while **Kohei Okuno** has filled in at times as
he’s more useful in possession. With this squad, the investment in the
past few seasons, Gamba clearly should be doing better… but given
**Katanosaka’s** profile, the amount of trust he seems to have from the
club hierarchy, and the clear misfortune regarding injuries and COVID
outbreaks, there’s still time for him to turn things around and turn
some of the **glimpses of quality** we’ve seen into a sustainable set of
good performances.

![Gamba
xGD](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/GambaOsaka_2022_mid_xgdiff_logo.png)

## Consadole Sapporo

Consadole Sapporo started their season off in… intriguing fashion as
they drew the first 6 (six!) games of the season before finally getting
walloped 0-5 against Sagan Tosu on matchday 7. Since then the usual
theme of Sapporo **yo-yo-ing** between Wins-Draws-Losses took hold and
they sit 11th in the standings. From watching their games and from [the
data](https://twitter.com/ARDataAnalysis/status/1535215205281505280), it
does feel like they have been bailed out of more potential losing games
due to some superb saves from **Takanori Sugeno**.

![Sapporo
xGD](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/ConsadoleSapporo_2022_mid_xgdiff_logo.png)

Unfortunately for Sapporo, **Sugeno** came off injured after matchday 13
and they have missed both his big saves as well as his involvement in
their build-up. With or without him though, their defense has leaked
like a sieve and they seem to concede goals from all sorts of
situations. They “lead” the league in goals conceded with a whopping 26.

![Sapporo
situation](../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_ConsadoleSapporo.png)

They also give up a league worst (by quite a margin) quality of shots
conceded that is somewhat counterbalanced by a OK-to-decent (if slightly
profligate) attack.

![Sapporo quadrant xG
xGA](../assets/2022-06-15-jleague-2022-midseason-review_files/quadrant/J-League_2022_mid_team_xG_xGA_plot.png)

**How do Consadole Sapporo play?**

The defense is based on **man-marking all over the pitch**, completely
ignoring concerns of wide open spaces left between players or lines.
While Sapporo at their best don’t have to worry about those gaps because
they can dispossess the opponent or win duels before that becomes an
issue, but as you might imagine this is also why they can be so easy to
create chances against. It’s a lot of running and pressing but they do
look like headless chickens at times. On the ball, one of the central
midfielders drops to turn the back 3 into a back 4. The outer Center
Backs, usually **Akito Fukumori** and **Shunta Tanaka** pretty much
operate as Full Backs while **Daiki Suga** and **Lucas Fernandes** take
up high and wide positions.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/ConsadoleSapporo/ConsadoleSapporo-buildup.png)

Since **Anderson Lopes** left early last year, there has been a clear
lack of focal point up top for Sapporo to settle long balls or get on
the end of one of **Lucas’** crosses. **Milan Tucic** has looked very
underwhelming to the point where it has usually been **Gabriel Xavier**
playing as a striker with **Yoshiaki Komai** and **Takuro Kaneko** in
close support. **Xavier** has usually been forced out of central areas
and drifts wide to receive the ball only making the problem worse. In
the off-season they brought back **Shinzo Koroki** but at age 35, his
best days are behind him and he’s also only appeared in 5 league games
due to injury. A bright spot has appeared this season with young **Taika
Nakashima** providing a spark as a late substitute in many games with
his strength, running, and heading ability. He has also scored more than
a few goals in the league cup so that’s added fuel to the flame over
calls for his inclusion into the starting lineup. It remains to be seen
if **Nakashima** can indeed nail down the striker role as consistently
performing from kickoff is very different from flashes of brilliance
against tired legs.

Despite finishing 4th in **Mihailo Petrovic’s** first season at the helm
back in 2018, results have been consistently **mediocre** with
consecutive midtable finishes and only a runner up finish in the 2019
League Cup were they anywhere near any sort of silverware. Sapporo don’t
have a whole lot of resources and **Petrovic** has been dipping into the
good pool of youth academy and university graduates throughout his
tenure but the problem has been a real lack of progress on any front,
tactically or in results. Even if their young players become good, then
they are either going to get taken by other J.League teams (for not a
whole lot, **Chanathip’s** transfer to Frontale being an exception) or
going straight to Europe. The big money they got for **Chanathip** is
presumably not going to be splashed out on big signings but rather to
keep things running and improve stuff behind-the-scenes, which is
reasonable. But in terms of the near-to-mid term future, where does
**Mischa** go from here? It just feels like Sapporo keep taking a few
steps forward but even more steps back every season and wind up in
midtable mediocrity… or this season, it could easily be worse.

![Sapporo squad age
profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_ConsadoleSapporo_2022_mid_EN.png)

## Urawa Reds

It has been a rocky start to the 2nd season of **Ricardo Rodriguez’s
Reds Revolution** as the club hovers just above the relegation zone. A
wild mix of disallowed goals (some deserved, some questionable), chances
being missed by themselves or scored by the opposition at crucial
branching points in games, and idiotic red cards especially when Urawa
were in the ascendancy (Gamba, Kobe, etc.), have seen the Reds
completely throwing away their momentum from their Emperor’s Cup win
late last year. This hasn’t been helped by injury issues (star striker
**Kasper Junker** having an especially slow start as his injury malaise
from last year followed him into this season) and a COVID scare right
after the morale-boosting pre-season Super Cup win over league and ACL
rivals Kawasaki Frontale.

Even with the injuries to **Tomoya Inukai** (out for the season) and
**Hiroki Sakai** (out for a few months), the defense hasn’t been the
problem at all with the Reds only conceding 16 goals, tied 5th best in
the league but more contextually is **significantly less than their
fellow relegation strugglers** around them. Even still, the problem
becomes when you can’t kill games off, even if Urawa manage to take the
lead, you keep giving opponents **hope** and they can very well manage
to nick a goal off of you no matter how good your defense normally is.
Of course, that doesn’t excuse **Ricardo Rodriguez** who just can’t seem
to figure out how to give the platform for his attackers to score goals
and unfortunately even in the few times they do, they aren’t able to
take their chances.

![UR
xG-Goals](../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/UrawaReds_2022_mid_rollingxGGoals_logo.png)

At the other end of the pitch, things have been pretty solid as they not
only allow very few shots, they are usually of very low quality as well.

![shot against quantity
quality](../assets/2022-06-15-jleague-2022-midseason-review_files/quadrant/J-League_2022_mid_team_shot_against_quant_qual_plot.png)

All of this has culminated in a side that suppresses opponent’s attacks,
creates few but good quality chances of their own… that they just can’t
finish.

![UR
xGD](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/UrawaReds_2022_mid_xgdiff_logo.png)

**How do Urawa Reds play?**

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/UrawaReds/Urawa-buildup-back3.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/UrawaReds/Urawa-buildup-Scholz-carry.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/UrawaReds/Urawa-buildup-movement-lure.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/UrawaReds/Urawa-Sekine-lure-upfield-switch.png)

Their build-up, excellent as it usually is can still be stifled too.
However, using **Shusaku Nishikawa’s** long range passing ability, Urawa
do have some forms of escape especially with long aerials toward
**Takahiro Akimoto** who is good at settling the ball using his
strength.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/UrawaReds/Urawa-buildup-trapped.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/UrawaReds/Urawa-pressed-go-long.png)

Like last year, **Ataru Esaka** and **Yoshio Koizumi** have been
excellent at finding gaps, turning, and playing a pass.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/UrawaReds/Urawa-buildup-movement-gaps.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/UrawaReds/Urawa-buildup-movement-gaps-2.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/UrawaReds/Urawa-buildup-movement-gaps-3.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/UrawaReds/Urawa-buildup-movement-gaps-4.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/UrawaReds/Urawa-buildup-movement-gaps-5.png)

On the other hand, a clear problem has been getting from the middle 3rd
to the final 3rd/penalty box…

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/UrawaReds/Urawa-no-runs-2nd-phase.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/UrawaReds/Urawa-no-runs-2nd-phase-2.png)

If this team can start scoring goals they will rocket up the table
because they really do have all the hallmarks of a good side with a
solid defense and a bag full of build-up routines that can evade almost
any press. Even with considerable investment on players and trust placed
in **Ricardo Rodriguez** as part of Urawa’s **3 Year Plan**, poor
results have derailed their season as they sit 14th, and a whole 15
points away from the last ACL spot (double of their current tally). So
although another top table finish is already off the cards, the Reds are
still with a shout in all cup competitions including the coveted Asian
Champions League trophy. Out of all the other struggling clubs around
them in the bottom half (especially fellow ACL team, Vissel Kobe), they
are the ones I believe have the best chance of climbing back into the
top half of the table.

![UR squad age
profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_UrawaReds_2022_mid_EN.png)

NOTE: **Bryan Linssen** has been signed, maybe he’s the one to solve
their goal scoring issues? After **Alex Schalk** and **David Moberg**,
maybe 3rd time is the charm??

## Kyoto Sanga

**Cho Kwi-jae** has revitalized a Kyoto Sanga side that had been stuck
in J2 for over a decade by immediately installing his playing style to
push Kyoto to an automatic promotion spot in his first season in charge
of the club in 2021. Kyoto is all about high intensity, pressing and
harrying opponents from the front while also launching quick counter
attacks when they are able to regain the ball in their own defensive 3rd
as well. On the other hand, they don’t seem quite so adept at breaking
down defenses so they do get stuck when opponents simply retreat and not
play into their hands. Their defending deeper in their own half of the
field has also been a concern as they have forced Naoto Kamifukumoto to
make a lot of saves. A mix of the veteran goalkeeper working miracles
and opponent’s poor finishing has Kyoto in the worrying position of
consistently conceding goals far less than the quality of chances they
give away opponents, something that could change with drastic
consequences. Overall they have conceded 17 non-penalty goals from 23.54
non-penalty xGA (around the middle of the pack in the former category
but 2nd worst in the league in the latter!).

![Kyoto
xGA-GoalsAgainst](../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/KyotoSanga_2022_mid_rollingxGAGoalsAgainst_logo.png)

Sanga’s main threat has been the eternal Nigerian, **Peter Utaka**. His
very presence has terrorized J2 and J1 defenses in the past as he has
the skill to complete attacks all by himself at times. At the **age of
38**, the big question in pre-season was whether he could still do his
thing against J1 defenses. With 8 goals and playing nearly every league
minute at the halfway point of the 2022 season, we can emphatically say
that he can. On the other hand, Kyoto’s clear reliance on him for any
attacking output has its limits as despite a decent start to the season
(including a surprise victory over Urawa Reds on opening day), Sanga
went win-less for nearly a month until their fortunate win against
Kawasaki Frontale right before the June international break.

![Kyoto
xGD](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/KyotoSanga_2022_mid_xgdiff_logo.png)

**How do Kyoto Sanga play?**

**NOTE**: All of the images come from one match because while I have
watched quite a bit of Kyoto this season (including going to a match at
their **wonderful** stadium), it’s simply a lot of work to do any of
this in my (limited) free time. In any case, their game against Urawa
was quite representative of what they want to do.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KyotoSanga/Sanga-high-press.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KyotoSanga/Sanga-high-press-long-diagonal.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KyotoSanga/Sanga-high-press-Utaka.png)

Sota Kawasaki, especially, has been very good in transitions.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KyotoSanga/Sanga-Kawasaki-transition.png)

Kyoto can also play out from the back, with the two box-to-box
midfielders working with the wingers to find space between the lines.
Although they don’t mind playing it more direct as well.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KyotoSanga/Sanga-between-lines.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/KyotoSanga/Sanga-long-ball.png)

Kyoto sit comfortably in 9th place right now, but points-wise the table
is quite tight and any more wobbles in form like in May can knock them
down into the relegation battle again. While the starting XI is decent
with aforementioned players like **Peter Utaka**, **Sota Kawasaki**,
**Shogo Asada**, being the standout, quite a lot of their squad options
are clearly J2 quality and don’t really seem to be able to make an
impact off the bench other than to reinvigorate Sanga’s press deep in
the 2nd Half of games. **Cho Kwi-jae** has a clearly defined system but
a lot still rests on the continued fitness and form of **Peter Utaka**,
his goals and assists will ultimately decide Kyoto’s fate in the 2nd
half of the season.

![Kyoto squad age
profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_KyotoSanga_2022_mid_EN.png)

## Sagan Tosu

Sagan Tosu are another team that I discounted heavily in my pre-season
predictions. While I still thought they wouldn’t get relegated, I
imagined them to probably be skirting around 13th-15th but then I got
really worried after defensive stalwart **Eduardo** was pried away by
Marinos mere weeks before the season started. While I did consider the
retention of Tosu’s ‘system’ that was fairly successful in 2021, albeit
this season with vastly different players of questionable (or so I
thought at that time) quality, I didn’t know how much of that was based
on **Kim Myung-hwi’s** work or the coaches. With the benefit of
hindsight now it seems that a lot of the mechanisms of the system was
crystallized by the coaches and the new manager **Kenta Kawai** came in
to add his own tweaks to it while trying best to integrate a whole new
set of players to it. Instead of the more “established” J1 names like
**Naoyuki Fujita**, **Yuki Kakita**, **Taisei Miyashiro**, **Hwang
Seok-Ho**, it has been relatively unknowns/unheralded players (**Yuto
Horigome**, **Akito Fukuta**) or young players (**Fuchi Honda**,
**Taichi Kikuchi**) that have taken the place of outgoing transfers.

![Tosu squad age
profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_SaganTosu_2022_mid_EN.png)

The performances and results have been relatively stable, which is a far
cry from what other people, including myself, were expecting. They were
actually undefeated until matchday 8 and also are the team with the
lowest number of losses in this half of the season (just 2!), however
they are “only” 8th due to 9 draws. This is partly by design due to
their conservative possession used as a defensive tactic as they
carefully try to build-up the ball from the back.

![Tosu xG
xGA](../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/SaganTosu_2022_mid_rollingxGGA_logo.png)

**How do Sagan Tosu play?**

The most notable tweak this season has been a consistent use of a
double-pivot as last season Tosu had a lot of trouble defending in
negative transitions (from attack-to-defense) using only a single pivot
of **Daiki Matsuoka** or **Keiya Sento**. This season has seen **Kei
Koizumi** (who at the closing stages of the last season took over the
single pivot position) sit next to **Akito Fukuta**. The shifting of the
back 3 into a back 4 on the left side that was a key aspect of their
play last season continues today but with different players.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SaganTosu/Tosu-position-fluidity.png)

While \_\_Park I.G.’\_\_s involvement isn’t shown in the below scenes,
he provides a lot of support the the Center Backs and provides that +1
in the build-up that can make playing through easier or even attract
more opponents high up (consequently leaving space to exploit behind for
Tosu attackers).

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SaganTosu/Tosu-buildup-rotations-movement.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SaganTosu/Tosu-buildup-rotations-movement-2.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SaganTosu/Tosu-buildup-rotations-movement-3.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SaganTosu/Tosu-buildup-rotations-movement-4.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SaganTosu/S-Pulse-defense-dragged.gif)

As good as they look in the examples above, they still do mess up and
give up chances especially compared to last season as they just don’t
have the quality of individuals in the back line and midfield having had
to go from **Eduardo** to **Masaya Tashiro** or **Akito Fukuta** instead
of **Daiki Matsuoka** or **Keiya Sento**, etc.

When teams try to play it long to nullify Tosu’s press or they are
simply able to evade it, it becomes all the more important for the back
3 to be able to shut down attacks before their opponent can push up to
support their strikers. Worse comes to worst, they do still have **Park
I.G.** who can sweep up across a big area.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SaganTosu/Tosu-defend-back3.png)

While Tosu have been consistently solid in defense, its still a concern
that they haven’t pressed their advantages when it comes to attack
especially when they are able to steal that ball high up the pitch due
to their well coordinated press. Tosu haven’t been able to get the best
out of **Yuki Kakita** (only 3 goals this season) and **Taisei
Miyashiro**, both of whom impressed at a poor Tokushima Vortis side last
season. A rotating cast of strikers have been tried, none of whom has
fully nailed down a spot until recently where **Yuji Ono** has been
picked for his pressing acumen and link-up abilities rather than his
hunger for goal. It seems the direction manager **Kawai** wants to take
is to let the goals be spread around the entire team.

![Tosu goals -
xG](../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/SaganTosu_2022_mid_rollingxGGoals_logo.png)

![Tosu
xGD](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/SaganTosu_2022_mid_xgdiff_logo.png)

## Avispa Fukuoka

It’s been pretty much the same for Avispa Fukuoka, although some results
haven’t fallen their way this year compared to last season but Avispa
plays along the very fine margins in football so it should be expected.
Looking at their xG difference chart in games where they’ve had a
positive xGD (even if by not a whole lot) results haven’t followed as
much this time around (note the 6 draws and 1 loss despite their
positive xGD in those games).

![Avispa
xGD](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/AvispaFukuoka_2022_mid_xgdiff_logo.png)

The Kyushu-based side still use a small tight knit squad, manager
Shigetoshi Hasebe’s only major changes was the incoming transfer of
Brazilian striker **Lukian** from newly promoted Jubilo Iwata and
**Tatsuya Tanaka** from Urawa Reds. Unfortunately it hasn’t worked out
for **Lukian** as he only scored his first goals against FC Tokyo in
early May after a drought of 10 matches. As a result, Avispa have
continued to rely on **Yuya Yamagishi** up top while the likes of
**Jordy Croux** continues to ably supply the attackers or take shots
himself by cutting in on his wicked left foot.

![Avispa squad age
profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_AvispaFukuoka_2022_mid_EN.png)

**How do Avispa Fukuoka play?**

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/AvispaFukuoka/Avispa-attack.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/AvispaFukuoka/Avispa-defense-block.png)

Even with a move to a slightly more pressing style to change things up,
the lack of goal scoring threat is still painfully clear with the game
against 10 men Nagoya in late May proving to be an egregious example.
One wonders how much manager **Shigetoshi Hasebe** might want to
sacrifice their defensive solidity to squeeze just a little more juice
out of an attack that, when their defense is breached by skill or luck,
don’t seem able to provide any sort of riposte.

![Avispa xG
xGA](../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/AvispaFukuoka_2022_mid_rollingxGGA_logo.png)

## Sanfrecce Hiroshima

It was a rough start of the season for a Sanfrecce Hiroshima that were
trying to rid themselves of the **Hiroshi Jofuku** era that started in
the 2018 season. With the entry restrictions for COVID in place at the
start of 2022, once again foreign managers and players coming into the
J.League had their arrival delayed. Although **Michael Skibbe** had
participated in pre-season “remotely”, without his actual presence there
on the sidelines until days before matchday 3 in early March the team
struggled as they posted a `0W 3D 2L` record in the first 5 games of the
2022 season. However, fortunes turned around as **Skibbe’s** revolution
started to take hold as they have only lost a single game (to Kashiwa
Reysol in matchday 11) since matchday 5 as Sanfrecce rocketed up the
table from the relegation zone and into the crowded top half of the
table. Their attacking output has improved tremendously compared to last
season and they are top or close to the top in a variety of attacking
stats like 20.69 total non-penalty xG (4th in the league), 1.38
non-penalty xG per 90 (2nd), and 229 total non-penalty shots (3rd).

![Sanfrecce Goals -
xG](../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/SanfrecceHiroshima_2022_mid_rollingxGGoals_logo.png)

This hasn’t come at a cost of poor defending as **Skibbe** has kept the
strong back 3 of **Hayato Araki**, **Sho Sasaki**, and **Yuki Nogami**
largely intact as a unit with **Tsukasa Shiotani** replacing **Nogami**
in the last few matchdays before the June international break. With
their aggressive high press, they try to win the ball back as high up
the pitch and away from their own goal as much as possible. This along
with the steady back line backed up by **Keisuke Osako** (who has
wrestled away the starting birth from veteran **Takuto Hayashi**) in
goal have kept down the volume of shots against extremely well as they
lead the league with 9.67 shots against per 90. On the other hand, when
Sanfrecce’s high press is evaded, teams have a lot of space to run at
against the Hiroshima back line to create dangerous chances.

![shot against quantity
quality](../assets/2022-06-15-jleague-2022-midseason-review_files/quadrant/J-League_2022_mid_team_shot_against_quant_qual_plot.png)

**How do Sanfrecce Hiroshima play?**

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SanfrecceHiroshima/Sanfrecce-press.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SanfrecceHiroshima/Sanfrecce-press-evade-gaps-2.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SanfrecceHiroshima/Sanfrecce-press-evade-gaps-4.png)

On the ball, Sanfrecce do try to work it out from the back, with clever
movements by the likes of **Tsukasa Morishima** and **Makoto Mitsuta**
to drop into space.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SanfrecceHiroshima/Sanfrecce-buildup-drop-mid.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SanfrecceHiroshima/Sanfrecce-Morishima-drop-create.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SanfrecceHiroshima/Sanfrecce-Morishima-drop-layoff.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SanfrecceHiroshima/Sanfrecce-Morishima-Mitsuta-pockets.png)

There still have been problems as whens things aren’t working out from
the back 3, their wing backs try to come deeper to help, which only
makes the problem worse at times.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SanfrecceHiroshima/Sanfrecce-buildup-squeezed.png)

Both are also threats on the counter as well, supported by the likes of
**Tomoya Fujii** rocketing up the right wing in support.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SanfrecceHiroshima/Sanfrecce-quick-counter.png)

The outer Center Backs also get involved to create overloads on the
wings as well, either carrying the ball up field themselves or timing
late runs into the final 3rd.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SanfrecceHiroshima/Sanfrecce-Nogami-support.png)

What **Michael Skibbe** has provided the team is a very clear plan of
attack and its a major reason why Sanfrecce are able to consistently get
a lot of shots (of varying quality).

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SanfrecceHiroshima/Sanfrecce-attack-plan.png)

With hardly any incoming transfers to shake things up what is still
largely a Jofuku-era squad, **Michael Skibbe** has done quite a good job
on a shoe string budget, improving and evolving existing players
(**Tomoya Fujii**, **Tsukasa Morishima**) and also bringing back players
out on loan (**Gakuto Notsuda**). **Yoshifumi Kashiwa** is rolling back
the years with some great performances and has nailed down that LWB spot
ahead of younger teammates. I was pretty skeptical of **Nassim Ben
Khalifa** but he’s honestly turned out all right so far. From his time
working with Skibbe in Switzerland, he clearly understands what is
required of him and while he’s only hit the net once so far, he’s been
contributing both on and off the ball across the pitch.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/SanfrecceHiroshima/Sanfrecce-BenKhalifa-2ST.png)

Still, some **more** investment is clearly needed with a clear drop off
in quality between their starting XI and the bench. A return from injury
of **Shun Ayukawa** and **Ezequiel** should add a bit more depth to
their squad as the very busy and physically taxing summer schedule comes
around to start the 2nd half of the season.

![Sanfrecce squad age
profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_SanfrecceHiroshima_2022_mid_EN.png)

## Jubilo Iwata

Manager **Masakazu Suzuki** had to step down due to health concerns so
**Akira Ito**, who had led fellow J2 team Ventforet Kofu in 2021,
stepped up to lead a Jubilo side who returned to J1 for the first time
since the 2019 season. As if that wasn’t enough they had lost their star
20 goal striker, **Lukian**, to Avispa Fukuoka in the winter transfer
window. The loss of such a focal point in attack was only exacerbated by
the fact that his replacement was none other than goal-shy **Kenyu
Sugimoto**.

As such it has not been an easy return to J1 for the Shizuoka-based side
as they have struggled in most games so far, their performances
consistently mediocre. Yet, more than a few results have gone their way
and the existence of even worse teams this season have meant they are
just about keep themselves above the relegation zone by a 2 point margin
in 15th place.

![iwata
xGD](../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/JubiloIwata_2022_mid_xgdiff_logo.png)

The stats all give a grim view of a very mediocre team that not only
take the fewest shots (although to be fair, they are of relatively good
quality) but in turn concede the most per 90 minutes as well.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/quadrant/J-League_2022_mid_shooting_plot.png)

A whopping 11 goals or 44% of all of their goals conceded have come from
crosses.

![iwata
situation](../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_JubiloIwata.png)

**How do Jubilo Iwata play?**

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/JubiloIwata/Jubilo-wing-overload.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/JubiloIwata/Jubilo-Sugimoto-long-ball.png)

A lot of emphasis is placed on players occupying all 5 lanes relative to
the positioning of their teammates. Jubilo can take it slow but their
build-up play has been susceptible to being intercepted in dangerous
positions. Manager **Ito** seems persistent on preserving this style
despite a more counter-attacking setup seemingly suiting the players
better such as **Yuto Suzuki** and **Fabian Gonzalez**.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/JubiloIwata/Jubilo-midfield-wingbacks-positioning.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/JubiloIwata/Jubilo-long-counter.png)

![](../assets/2022-06-15-jleague-2022-midseason-review_files/diagrams/JubiloIwata/Jubilo-long-counter-2.png)

**Yuto Suzuki** (not to be confused with Yuito at regional rivals
S-Pulse) has been a revelation even at the J1 level but it should be
concerning that not only does he lead the team in goal scoring but also
in assists despite being a Right Wing back. Both **Yuki Otsu** and
**Fabian Gonzalez** have appeared as super subs with both players on 3
goals at this point in the season. It took a bit of time but **Rikiya
Uehara**, who was curiously on loan at J1 side Vegalta Sendai last
season while Iwata themselves were in J2, has pushed his way into the
starting line up as he has started all but one game from matchday 9.
Japan and J.League legend **Yasuhito Endo** still contributes with his
great range of passing and set pieces, Iwata will need all of his
experience to be able to keep themselves afloat in J1. All in all,
Jubilo Iwata will have to sharpen up considerably at both ends of the
pitch as their results might dip to levels more in line with their bad
performances in the 2nd half of the season.

![iwata
squad-age-profile](../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_JubiloIwata_2022_mid_EN.png)

![xG-xGA](../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/JubiloIwata_2022_mid_rollingxGGA_logo.png)

# Data Visualizations

## Squad Age Profiles

I’ve changed the calculation of a squad’s median age up a bit by simply
taking into account only players that have played 50% of more of total
possible league minutes. This is so when looking at the ‘average’ age of
a team, we’re doing a better job of considering players who are
**regulars** in the team. I am not sure how other people might do it but
from playing around with the raw data it looks OK, most teams have
around 9\~12 players that meet this threshold so I do think I’m
capturing the right selection of players in any given team.

Anyway, here’s the list of the U-23 players in the league with the most
minutes played so far this season (filtered for those that have played
more than 50% of total possible league minutes). You might want to keep
an eye on these guys in the short-to-mid term.

<details>
<summary>
<b>Click to show R code!</b>
</summary>
<pre>

```r
# library(dplyr)
# library(knitr)
# library(kableExtra)

jleague_age_utility_df <- read.csv(
  file = "https://raw.githubusercontent.com/Ryo-N7/soccer_ggplots/master/data/jleague_2022_mid/jleague_age_utility_df_2022_mid.csv")

u23_players_tab <- jleague_age_utility_df %>% 
  filter(age <= 23, min_perc >= 0.5) %>% 
  arrange(desc(min_perc)) %>% 
  select(contains('name'), age, -fname, minutes, min_perc) %>% 
  mutate(min_perc = min_perc * 100) %>% 
  tidyr::unite('Name', first_name, last_name, sep = ' ') %>% 
  rename(Team = team_name, Age = age, Minutes = minutes,
         `% of Total Minutes Played` = min_perc) %>% 
  knitr::kable()
```
</pre>
</details>
<table>
<thead>
<tr>
<th style="text-align:left;">
Name
</th>
<th style="text-align:left;">
Team
</th>
<th style="text-align:right;">
Age
</th>
<th style="text-align:right;">
Minutes
</th>
<th style="text-align:right;">
% of Total Minutes Played
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Taiyo Koga
</td>
<td style="text-align:left;">
Kashiwa Reysol
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
1440
</td>
<td style="text-align:right;">
100.0
</td>
</tr>
<tr>
<td style="text-align:left;">
Tomoya Fujii
</td>
<td style="text-align:left;">
Sanfrecce Hiroshima
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
1310
</td>
<td style="text-align:right;">
97.0
</td>
</tr>
<tr>
<td style="text-align:left;">
Yuito Suzuki
</td>
<td style="text-align:left;">
Shimizu S-Pulse
</td>
<td style="text-align:right;">
20
</td>
<td style="text-align:right;">
1328
</td>
<td style="text-align:right;">
92.2
</td>
</tr>
<tr>
<td style="text-align:left;">
Keigo Tsunemoto
</td>
<td style="text-align:left;">
Kashima Antlers
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
1301
</td>
<td style="text-align:right;">
90.3
</td>
</tr>
<tr>
<td style="text-align:left;">
Ayase Ueda
</td>
<td style="text-align:left;">
Kashima Antlers
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
1284
</td>
<td style="text-align:right;">
89.2
</td>
</tr>
<tr>
<td style="text-align:left;">
Mao Hosoya
</td>
<td style="text-align:left;">
Kashiwa Reysol
</td>
<td style="text-align:right;">
20
</td>
<td style="text-align:right;">
1278
</td>
<td style="text-align:right;">
88.7
</td>
</tr>
<tr>
<td style="text-align:left;">
Shogo Asada
</td>
<td style="text-align:left;">
Kyoto Sanga
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
1262
</td>
<td style="text-align:right;">
87.6
</td>
</tr>
<tr>
<td style="text-align:left;">
Ryuya Nishio
</td>
<td style="text-align:left;">
Cerezo Osaka
</td>
<td style="text-align:right;">
21
</td>
<td style="text-align:right;">
1260
</td>
<td style="text-align:right;">
87.5
</td>
</tr>
<tr>
<td style="text-align:left;">
Kosei Tani
</td>
<td style="text-align:left;">
Shonan Bellmare
</td>
<td style="text-align:right;">
21
</td>
<td style="text-align:right;">
1260
</td>
<td style="text-align:right;">
87.5
</td>
</tr>
<tr>
<td style="text-align:left;">
Yuki Kobayashi
</td>
<td style="text-align:left;">
Vissel Kobe
</td>
<td style="text-align:right;">
21
</td>
<td style="text-align:right;">
1216
</td>
<td style="text-align:right;">
84.4
</td>
</tr>
<tr>
<td style="text-align:left;">
Haruya Fujii
</td>
<td style="text-align:left;">
Nagoya Grampus
</td>
<td style="text-align:right;">
21
</td>
<td style="text-align:right;">
1212
</td>
<td style="text-align:right;">
84.2
</td>
</tr>
<tr>
<td style="text-align:left;">
Yuto Iwasaki
</td>
<td style="text-align:left;">
Sagan Tosu
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
1208
</td>
<td style="text-align:right;">
83.9
</td>
</tr>
<tr>
<td style="text-align:left;">
Kuryu Matsuki
</td>
<td style="text-align:left;">
FC Tokyo
</td>
<td style="text-align:right;">
19
</td>
<td style="text-align:right;">
1191
</td>
<td style="text-align:right;">
82.7
</td>
</tr>
<tr>
<td style="text-align:left;">
Reon Yamahara
</td>
<td style="text-align:left;">
Shimizu S-Pulse
</td>
<td style="text-align:right;">
22
</td>
<td style="text-align:right;">
1182
</td>
<td style="text-align:right;">
82.1
</td>
</tr>
<tr>
<td style="text-align:left;">
Daiki Suga
</td>
<td style="text-align:left;">
Consadole Sapporo
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
1136
</td>
<td style="text-align:right;">
78.9
</td>
</tr>
<tr>
<td style="text-align:left;">
Ikuma Sekigawa
</td>
<td style="text-align:left;">
Kashima Antlers
</td>
<td style="text-align:right;">
21
</td>
<td style="text-align:right;">
1123
</td>
<td style="text-align:right;">
78.0
</td>
</tr>
<tr>
<td style="text-align:left;">
Asahi Sasaki
</td>
<td style="text-align:left;">
Kawasaki Frontale
</td>
<td style="text-align:right;">
22
</td>
<td style="text-align:right;">
1122
</td>
<td style="text-align:right;">
77.9
</td>
</tr>
<tr>
<td style="text-align:left;">
Makoto Mitsuta
</td>
<td style="text-align:left;">
Sanfrecce Hiroshima
</td>
<td style="text-align:right;">
22
</td>
<td style="text-align:right;">
1023
</td>
<td style="text-align:right;">
75.8
</td>
</tr>
<tr>
<td style="text-align:left;">
Daiki Sugioka
</td>
<td style="text-align:left;">
Shonan Bellmare
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
1024
</td>
<td style="text-align:right;">
71.1
</td>
</tr>
<tr>
<td style="text-align:left;">
Hirokazu Ishihara
</td>
<td style="text-align:left;">
Shonan Bellmare
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
1010
</td>
<td style="text-align:right;">
70.1
</td>
</tr>
<tr>
<td style="text-align:left;">
Teruki Hara
</td>
<td style="text-align:left;">
Shimizu S-Pulse
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
980
</td>
<td style="text-align:right;">
68.1
</td>
</tr>
<tr>
<td style="text-align:left;">
Keisuke Osako
</td>
<td style="text-align:left;">
Sanfrecce Hiroshima
</td>
<td style="text-align:right;">
22
</td>
<td style="text-align:right;">
900
</td>
<td style="text-align:right;">
66.7
</td>
</tr>
<tr>
<td style="text-align:left;">
Hisashi Appiah
</td>
<td style="text-align:left;">
Kyoto Sanga
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
944
</td>
<td style="text-align:right;">
65.6
</td>
</tr>
<tr>
<td style="text-align:left;">
Sota Kawasaki
</td>
<td style="text-align:left;">
Kyoto Sanga
</td>
<td style="text-align:right;">
20
</td>
<td style="text-align:right;">
907
</td>
<td style="text-align:right;">
63.0
</td>
</tr>
<tr>
<td style="text-align:left;">
Atsuki Ito
</td>
<td style="text-align:left;">
Urawa Reds
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
884
</td>
<td style="text-align:right;">
61.4
</td>
</tr>
<tr>
<td style="text-align:left;">
Hiroto Yamami
</td>
<td style="text-align:left;">
Gamba Osaka
</td>
<td style="text-align:right;">
22
</td>
<td style="text-align:right;">
824
</td>
<td style="text-align:right;">
61.0
</td>
</tr>
<tr>
<td style="text-align:left;">
Taiga Hata
</td>
<td style="text-align:left;">
Shonan Bellmare
</td>
<td style="text-align:right;">
20
</td>
<td style="text-align:right;">
857
</td>
<td style="text-align:right;">
59.5
</td>
</tr>
<tr>
<td style="text-align:left;">
Yugo Tatsuta
</td>
<td style="text-align:left;">
Shimizu S-Pulse
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
814
</td>
<td style="text-align:right;">
56.5
</td>
</tr>
<tr>
<td style="text-align:left;">
Shuto Machino
</td>
<td style="text-align:left;">
Shonan Bellmare
</td>
<td style="text-align:right;">
22
</td>
<td style="text-align:right;">
792
</td>
<td style="text-align:right;">
55.0
</td>
</tr>
<tr>
<td style="text-align:left;">
Daiya Tono
</td>
<td style="text-align:left;">
Kawasaki Frontale
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
769
</td>
<td style="text-align:right;">
53.4
</td>
</tr>
<tr>
<td style="text-align:left;">
Satoshi Tanaka
</td>
<td style="text-align:left;">
Shonan Bellmare
</td>
<td style="text-align:right;">
19
</td>
<td style="text-align:right;">
764
</td>
<td style="text-align:right;">
53.1
</td>
</tr>
<tr>
<td style="text-align:left;">
Taichi Kikuchi
</td>
<td style="text-align:left;">
Sagan Tosu
</td>
<td style="text-align:right;">
23
</td>
<td style="text-align:right;">
738
</td>
<td style="text-align:right;">
51.2
</td>
</tr>
</tbody>
</table>

Here are the image links for each team:

\|<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_KawasakiFrontale_2022_mid_EN.png">Kawasaki
Frontale</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_GambaOsaka_2022_mid_EN.png">Gamba
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_NagoyaGrampus_2022_mid_EN.png">Nagoya
Grampus</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_CerezoOsaka_2022_mid_EN.png">Cerezo
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_KashimaAntlers_2022_mid_EN.png">Kashima
Antlers</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_FCTokyo_2022_mid_EN.png">FC
Tokyo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_KashiwaReysol_2022_mid_EN.png">Kashiwa
Reysol</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_SanfrecceHiroshima_2022_mid_EN.png">Sanfrecce
Hiroshima</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_YokohamaFMarinos_2022_mid_EN.png">Yokohama
F. Marinos</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_UrawaReds_2022_mid_EN.png">Urawa
Reds</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_JubiloIwata_2022_mid_EN.png">Jubilo
Iwata</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_ConsadoleSapporo_2022_mid_EN.png">Consadole
Sapporo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_SaganTosu_2022_mid_EN.png">Sagan
Tosu</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_VisselKobe_2022_mid_EN.png">Vissel
Kobe</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_ShimizuSPulse_2022_mid_EN.png">Shimizu
S-Pulse</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_AvispaFukuoka_2022_mid_EN.png">Avispa
Fukuoka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_ShonanBellmare_2022_mid_EN.png">Shonan
Bellmare</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/squad_age_profile/SquadAge_KyotoSanga_2022_mid_EN.png">Kyoto
Sanga</a>

## Time Interval

Ideally I would use a 15 minute interval so I could get rid of that one
weird section straddling both halves (40-50th minute) but this was the
easiest data set I could get. What’s noticeable from this data set is
that the **good** teams generally know how to close out a game and don’t
concede many goals in the last 10\~20 minutes.

Here are the image links for each team:

\|<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_KawasakiFrontale.png">Kawasaki
Frontale</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_GambaOsaka.png">Gamba
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_NagoyaGrampus.png">Nagoya
Grampus</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_CerezoOsaka.png">Cerezo
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_KashimaAntlers.png">Kashima
Antlers</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_FCTokyo.png">FC
Tokyo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_KashiwaReysol.png">Kashiwa
Reysol</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_SanfrecceHiroshima.png">Sanfrecce
Hiroshima</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_YokohamaMarinos.png">Yokohama
F. Marinos</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_UrawaReds.png">Urawa
Reds</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_JubiloIwata.png">Jubilo
Iwata</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_ConsadoleSapporo.png">Consadole
Sapporo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_SaganTosu.png">Sagan
Tosu</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_VisselKobe.png">Vissel
Kobe</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_ShimizuSPulse.png">Shimizu
S-Pulse</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_AvispaFukuoka.png">Avispa
Fukuoka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_ShonanBellmare.png">Shonan
Bellmare</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/interval/interval_goaltimes_KyotoSanga.png">Kyoto
Sanga</a>

## Scoring Situations

Ideally, I would have data that concerns all shots or xG accumulated
from different match situations as that would mean a much larger sample
of data to power any insights (as goals are only the end result and may
not give us information about a team’s actual performance).

Here are the image links for each team:

\|<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_KawasakiFrontale.png">Kawasaki
Frontale</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_GambaOsaka.png">Gamba
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_NagoyaGrampus.png">Nagoya
Grampus</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_CerezoOsaka.png">Cerezo
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_KashimaAntlers.png">Kashima
Antlers</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_FCTokyo.png">FC
Tokyo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_KashiwaReysol.png">Kashiwa
Reysol</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_SanfrecceHiroshima.png">Sanfrecce
Hiroshima</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_YokohamaMarinos.png">Yokohama
F. Marinos</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_UrawaReds.png">Urawa
Reds</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_JubiloIwata.png">Jubilo
Iwata</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_ConsadoleSapporo.png">Consadole
Sapporo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_SaganTosu.png">Sagan
Tosu</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_VisselKobe.png">Vissel
Kobe</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_ShimizuSPulse.png">Shimizu
S-Pulse</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_AvispaFukuoka.png">Avispa
Fukuoka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_ShonanBellmare.png">Shonan
Bellmare</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/situation/goal_situation_plot_2022_mid_KyotoSanga.png">Kyoto
Sanga</a>

## Team Shot Quantity

In the previous few sections we got to know a lot about the goals that
J.League teams scored. However, in a sport like soccer/football goals
are hard to come by, they might not really accurately represent a team’s
actual ability or performance (even if ultimately, it’s the end result
that matters). To take things one step further I was able to gather data
from Sporteria on shot quantity to dive a bit more into team
performances. I’ve reversed the order of some of the stats in these next
few plots so that in all cases the **top right** is **best** and
**bottom left** is the **worst** teams when looking at their respective
stats.

![](../assets/2022-06-15-jleague-2022-midseason-review_files/quadrant/J-League_2022_mid_shooting_plot.png)

## Team Shot Quality

So, what exactly is **expected goals** (xG)? Expected goals is a
statistic where a model assigns a probability (between 0 and 1) that a
shot taken will result in a goal based on a variety of variables and is
used for evaluating the quality of chances and predicting players’ and
teams’ future performances. A xG model only looks at the variables up to
the point that the player touches the ball for a shot. Post-shot xG
models covers the information about where in the frame of the goal the
shot went (“post” as in all the information after the player touches the
ball for the shot) but I won’t cover that here.

For some quick primers on xG check the links below:

-   [Expected Goals in Context
    (StatsPerform)](https://www.statsperform.com/resource/expected-goals-in-context/)
-   [What is xG?
    (TifoFootball)](https://www.youtube.com/watch?v=zSaeaFcm1SY)

The following two sections use xG data from Football-Lab. I’m not privy
to all of what goes into their model but the [explanation page on their
website (in Japanese)](https://www.football-lab.jp/pages/expected_goal/)
tells us about some of the information they used:

-   Distance from goal?
-   Angle from goal line?
-   Aerial duel?
-   Body part used?
-   Number of touches? (one touch, more than two touches, set plays,
    etc.)
-   Play situation? (Corner kick, direct/indirect free kick, open play,
    etc.)

So, the usual variables that you might recognize from other xG models
are being considered. Combining shot quantity and shot quality numbers
gives you a much better idea about a team’s performance on either side
of the ball.

![xG-xGA](../assets/2022-06-15-jleague-2022-midseason-review_files/quadrant/J-League_2022_mid_team_xG_xGA_plot.png)

![shot quantity
quality](../assets/2022-06-15-jleague-2022-midseason-review_files/quadrant/J-League_2022_mid_team_shot_quant_qual_plot.png)

![shot against quantity
quality](../assets/2022-06-15-jleague-2022-midseason-review_files/quadrant/J-League_2022_mid_team_shot_against_quant_qual_plot.png)

## 5 Match Rolling Averages:

Here are the image links for each team:

### Goals vs. Goals Against

\|<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/KawasakiFrontale_2022_mid_rollingGGA_logo.png">Kawasaki
Frontale</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/GambaOsaka_2022_mid_rollingGGA_logo.png">Gamba
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/NagoyaGrampus_2022_mid_rollingGGA_logo.png">Nagoya
Grampus</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/CerezoOsaka_2022_mid_rollingGGA_logo.png">Cerezo
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/KashimaAntlers_2022_mid_rollingGGA_logo.png">Kashima
Antlers</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/FCTokyo_2022_mid_rollingGGA_logo.png">FC
Tokyo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/KashiwaReysol_2022_mid_rollingGGA_logo.png">Kashiwa
Reysol</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/SanfrecceHiroshima_2022_mid_rollingGGA_logo.png">Sanfrecce
Hiroshima</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/YokohamaMarinos_2022_mid_rollingGGA_logo.png">Yokohama
F. Marinos</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/UrawaReds_2022_mid_rollingGGA_logo.png">Urawa
Reds</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/JubiloIwata_2022_mid_rollingGGA_logo.png">Jubilo
Iwata</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/ConsadoleSapporo_2022_mid_rollingGGA_logo.png">Consadole
Sapporo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/SaganTosu_2022_mid_rollingGGA_logo.png">Sagan
Tosu</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/VisselKobe_2022_mid_rollingGGA_logo.png">Vissel
Kobe</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/ShimizuSPulse_2022_mid_rollingGGA_logo.png">Shimizu
S-Pulse</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/AvispaFukuoka_2022_mid_rollingGGA_logo.png">Avispa
Fukuoka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/ShonanBellmare_2022_mid_rollingGGA_logo.png">Shonan
Bellmare</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/goals/KyotoSanga_2022_mid_rollingGGA_logo.png">Kyoto
Sanga</a>

### xG vs. xGA

\|<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/KawasakiFrontale_2022_mid_rollingxGGA_logo.png">Kawasaki
Frontale</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/GambaOsaka_2022_mid_rollingxGGA_logo.png">Gamba
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/NagoyaGrampus_2022_mid_rollingxGGA_logo.png">Nagoya
Grampus</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/CerezoOsaka_2022_mid_rollingxGGA_logo.png">Cerezo
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/KashimaAntlers_2022_mid_rollingxGGA_logo.png">Kashima
Antlers</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/FCTokyo_2022_mid_rollingxGGA_logo.png">FC
Tokyo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/KashiwaReysol_2022_mid_rollingxGGA_logo.png">Kashiwa
Reysol</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/SanfrecceHiroshima_2022_mid_rollingxGGA_logo.png">Sanfrecce
Hiroshima</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/YokohamaMarinos_2022_mid_rollingxGGA_logo.png">Yokohama
F. Marinos</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/AvispaFukuoka_2022_mid_rollingxGGA_logo.png">Urawa
Reds</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/JubiloIwata_2022_mid_rollingxGGA_logo.png">Jubilo
Iwata</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/ConsadoleSapporo_2022_mid_rollingxGGA_logo.png">Consadole
Sapporo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/SaganTosu_2022_mid_rollingxGGA_logo.png">Sagan
Tosu</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/VisselKobe_2022_mid_rollingxGGA_logo.png">Vissel
Kobe</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/ShimizuSPulse_2022_mid_rollingxGGA_logo.png">Shimizu
S-Pulse</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/AvispaFukuoka_2022_mid_rollingxGGA_logo.png">Avispa
Fukuoka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/ShonanBellmare_2022_mid_rollingxGGA_logo.png">Shonan
Bellmare</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG/KyotoSanga_2022_mid_rollingxGGA_logo.png">Kyoto
Sanga</a>

### xG vs. Goals

\|<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/KawasakiFrontale_2022_mid_rollingxGGoals_logo.png">Kawasaki
Frontale</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/GambaOsaka_2022_mid_rollingxGGoals_logo.png">Gamba
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/NagoyaGrampus_2022_mid_rollingxGGoals_logo.png">Nagoya
Grampus</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/CerezoOsaka_2022_mid_rollingxGGoals_logo.png">Cerezo
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/KashimaAntlers_2022_mid_rollingxGGoals_logo.png">Kashima
Antlers</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/FCTokyo_2022_mid_rollingxGGoals_logo.png">FC
Tokyo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/KashiwaReysol_2022_mid_rollingxGGoals_logo.png">Kashiwa
Reysol</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/SanfrecceHiroshima_2022_mid_rollingxGGoals_logo.png">Sanfrecce
Hiroshima</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/YokohamaMarinos_2022_mid_rollingxGGoals_logo.png">Yokohama
F. Marinos</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/UrawaReds_2022_mid_rollingxGGoals_logo.png">Urawa
Reds</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/JubiloIwata_2022_mid_rollingxGGoals_logo.png">Jubilo
Iwata</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/ConsadoleSapporo_2022_mid_rollingxGGoals_logo.png">Consadole
Sapporo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/SaganTosu_2022_mid_rollingxGGoals_logo.png">Sagan
Tosu</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/VisselKobe_2022_mid_rollingxGGoals_logo.png">Vissel
Kobe</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/ShimizuSPulse_2022_mid_rollingxGGoals_logo.png">Shimizu
S-Pulse</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/AvispaFukuoka_2022_mid_rollingxGGoals_logo.png">Avispa
Fukuoka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/ShonanBellmare_2022_mid_rollingxGGoals_logo.png">Shonan
Bellmare</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xG-Goals/KyotoSanGoals_2022_mid_rollingxGGoals_logo.png">Kyoto
Sanga</a>

### xGA vs. Goals Against

\|<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/KawasakiFrontale_2022_mid_rollingxGAGoalsAgainst_logo.png">Kawasaki
Frontale</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/GambaOsaka_2022_mid_rollingxGAGoalsAgainst_logo.png">Gamba
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/NagoyaGrampus_2022_mid_rollingxGAGoalsAgainst_logo.png">Nagoya
Grampus</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/CerezoOsaka_2022_mid_rollingxGAGoalsAgainst_logo.png">Cerezo
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/KashimaAntlers_2022_mid_rollingxGAGoalsAgainst_logo.png">Kashima
Antlers</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/FCTokyo_2022_mid_rollingxGAGoalsAgainst_logo.png">FC
Tokyo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/KashiwaReysol_2022_mid_rollingxGAGoalsAgainst_logo.png">Kashiwa
Reysol</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/SanfrecceHiroshima_2022_mid_rollingxGAGoalsAgainst_logo.png">Sanfrecce
Hiroshima</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/YokohamaMarinos_2022_mid_rollingxGAGoalsAgainst_logo.png">Yokohama
F. Marinos</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/AvispaFukuoka_2022_mid_rollingxGAGoalsAgainst_logo.png">Urawa
Reds</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/JubiloIwata_2022_mid_rollingxGAGoalsAgainst_logo.png">Jubilo
Iwata</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/ConsadoleSapporo_2022_mid_rollingxGAGoalsAgainst_logo.png">Consadole
Sapporo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/SaganTosu_2022_mid_rollingxGAGoalsAgainst_logo.png">Sagan
Tosu</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/VisselKobe_2022_mid_rollingxGAGoalsAgainst_logo.png">Vissel
Kobe</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/ShimizuSPulse_2022_mid_rollingxGAGoalsAgainst_logo.png">Shimizu
S-Pulse</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/AvispaFukuoka_2022_mid_rollingxGAGoalsAgainst_logo.png">Avispa
Fukuoka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/ShonanBellmare_2022_mid_rollingxGAGoalsAgainst_logo.png">Shonan
Bellmare</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/rolling_average/xGA-GoalsAgainst/KyotoSanga_2022_mid_rollingxGAGoalsAgainst_logo.png">Kyoto
Sanga</a>

## xG Difference

xG Difference is pretty much the same thing as Goal Difference except
that we use xG and xGA rather than goals and goals against. This lets us
see very quickly which teams generally outperformed their opponents in
terms of quality of chances created to quality of chances conceded based
on a xG model. This time around I also included the team’s results
inside the bubble points. So it’s easier to see whether a team that had
a positive xGD in a specific match couldn’t manage to win the game or
vice-versa.

\|<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/KawasakiFrontale_2022_mid_xgdiff_logo.png">Kawasaki
Frontale</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/GambaOsaka_2022_mid_xgdiff_logo.png">Gamba
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/NagoyaGrampus_2022_mid_xgdiff_logo.png">Nagoya
Grampus</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/CerezoOsaka_2022_mid_xgdiff_logo.png">Cerezo
Osaka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/KashimaAntlers_2022_mid_xgdiff_logo.png">Kashima
Antlers</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/FCTokyo_2022_mid_xgdiff_logo.png">FC
Tokyo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/KashiwaReysol_2022_mid_xgdiff_logo.png">Kashiwa
Reysol</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/SanfrecceHiroshima_2022_mid_xgdiff_logo.png">Sanfrecce
Hiroshima</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/YokohamaMarinos_2022_mid_xgdiff_logo.png">Yokohama
F. Marinos</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/AvispaFukuoka_2022_mid_xgdiff_logo.png">Urawa
Reds</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/JubiloIwata_2022_mid_xgdiff_logo.png">Jubilo
Iwata</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/ConsadoleSapporo_2022_mid_xgdiff_logo.png">Consadole
Sapporo</a> \| \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/SaganTosu_2022_mid_xgdiff_logo.png">Sagan
Tosu</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/VisselKobe_2022_mid_xgdiff_logo.png">Vissel
Kobe</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/ShimizuSPulse_2022_mid_xgdiff_logo.png">Shimizu
S-Pulse</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/AvispaFukuoka_2022_mid_xgdiff_logo.png">Avispa
Fukuoka</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/ShonanBellmare_2022_mid_xgdiff_logo.png">Shonan
Bellmare</a> \|
<a href="../assets/2022-06-15-jleague-2022-midseason-review_files/xGDiff/KyotoSanga_2022_mid_xgdiff_logo.png">Kyoto
Sanga</a>

# Conclusion

It’s been quite a season so far, and unlike recent previous seasons
**Kawasaki Frontale** isn’t dominating at the top of the table. The gap
between all teams feels quite smaller than they have in the last few
years with anybody capable of getting a few consecutive good/bad results
to rocket/plummet up/down the table! The top of the table is quite tight
with what was supposed to be the ‘top 3’ teams all taking stumbles in
late May bringing the likes of **Kashiwa Reysol** and **Cerezo Osaka**
on the cusp of breaking into the Asian Champions League places, if not
getting involved in the title race themselves.

At the bottom sit **Vissel Kobe** who have got their only 2 wins of the
season in the past month but hope that they can turn their season
around. As mentioned if Urawa can find their goal scoring boots they’ll
be able to jump back up the table as well. This might spell trouble for
other bottom clubs who are slightly buoyed in the standings due to the
under-performance of these ‘on-paper’ stronger clubs. With a lot of
fixtures in the hot and humid Japanese summer to come, buckle up for
some more table turbulence!

As for myself, in early April I went to Kyoto and watched **Kyoto
Sanga** play against **Sagan Tosu** at the lovely `Sanga Stadium`. Below
are some pictures:

<img src="../assets/2022-06-15-jleague-2022-midseason-review_files/IMG-5040.JPG" style="display: block; margin: auto;" width = "750" />

This weekend I will be going to Saitama to watch **Urawa Reds** take on
**Nagoya Grampus**, hopefully as things start opening up more I’ll be
able to visit more and more stadiums (with full crowd atmospheres) in
the coming months!

See you all in November for the season end review!

<center>
<script type='text/javascript' src='https://storage.ko-fi.com/cdn/widget/Widget_2.js'></script>
<script type='text/javascript'>kofiwidget2.init('Buy Me A Coffee!', '#29abe0', 'O4O342A2A');kofiwidget2.draw();</script>
<center/>
