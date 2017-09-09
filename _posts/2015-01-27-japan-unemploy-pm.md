---
title: "Visualizing Japan's Prime Ministers and unemployment data."
author: "RN7"
date: "September 8, 2017"
output: 
  html_document: 
    keep_md: yes
---

```{r setup, include = FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## Simple graphing with ggplot2. 

I was flipping through Hadley Wickham's *ggplot2* book the other day when I came across this:

```{r hadleys plot, echo = FALSE, warning = FALSE, message = FALSE}
library(dplyr)
library(ggplot2)

presidential <- presidential %>% filter(start > economics$date[1])

ggplot(economics) +
  geom_rect(
    aes(xmin = start, xmax = end, fill = party), 
    ymin = -Inf, ymax = Inf, alpha = 0.2,
    data = presidential
  ) +
  geom_vline(
    aes(xintercept = as.numeric(start)), 
    data = presidential,
    color = "grey50", alpha = 0.5
  ) +
  geom_text(
    aes(x = start, y = 2500, label = name), 
    data = presidential, 
    size = 3, nudge_x = 50
  ) +
  geom_line(aes(date, unemploy)) +
  scale_fill_manual(values = c("blue", "red"))
```

Which shows the unemployment data for the USA from 1967 to 2015 along with the Presidents in power during those periods (and their respective political parties). A very simple but poignant graph that (with added historical narrative) can tell us a lot about different stories about the US economy and the politics driving them! Motivated by this I set out to make a similar graph but with data from my birth country, Japan.

  For the unemployment data, I was able to download a dataset from the ["Federal Reserve Bank of St. Louis"] (https://fred.stlouisfed.org/series/LRHUTTTTJPM156S) website. It's a really fantastic source with loads of raw data from around the world that you can download (in Excel, .csv, .png, PowerPoint, and .pdf formats), I will definitely be coming back here for other articles! This dataset comprises of the harmonized monthly unemployment rate for ALL person for Japan. There was another dataset for Aged 15-64 however that one only went back to January of 1970. I wanted to go back to 1960 (or better 1945) for a better look at Japan's post-war economic history and recovery so I went with this one instead. For a more in-depth analysis I would hunt down some Japanese sources but for today we are just focusing on the simple **ggplot2** graph.

  For the dataset about the Prime Ministers of Japan I went to Wikipedia, a source that's pretty reliable and easy to use. Normally, I would web-scrape the information using **rvest** however, I did not know how to scrap multiple tables at once (as the Prime Ministers were divided into individual tables according to the reigning Emperor) so I created it manually. Thankfully this didn't take too long!

```{r create prime ministers data set}
prime_ministers <- data.frame(
  name = c("Tetsu Katayama", "Hitoshi Ashida", "Shigeru Yoshida", "Ichiro Hatoyama", "Tanzan Ishibashi",
           "Nobusuke Kishi", "Hayato Ikeda", "Eisaku Sato", "Kakuei Tanaka", "Takeo Miki",
           "Takeo Fukuda", "Masayoshi Ohira", "Zenko Suzuki", "Yasuhiro Nakasone", "Noboru Takeshita",
           "Sosuke Uno", "Toshiki Kaifu", "Kiichi Miyazawa", "Morihiro Hosokawa", "Tsutomu Hata",
           "Tomiichi Murayama", "Ryutaro Hashimoto", "Keizo Obuchi", "Yoshiro Mori", "Junichiro Koizumi",
           "Shinzo Abe (1)", "Yasuo Fukuda", "Taro Aso", "Yukio Hatoyama", "Naoto Kan",
           "Yoshihiko Noda", "Shinzo Abe (2)"),
  
  start = as.Date(c("1947-05-24", "1948-03-10", "1948-10-15", "1954-12-10", "1956-12-23",
                    "1957-02-25", "1960-07-19", "1964-11-09", "1972-07-07", "1974-12-09",
                    "1976-12-24", "1978-12-07", "1980-07-17", "1982-11-27", "1987-11-06",
                    "1989-06-03", "1989-08-10", "1991-11-05", "1993-08-09", "1994-04-28",
                    "1994-06-30", "1996-01-11", "1998-06-30", "2000-04-05", "2001-04-26",
                    "2006-09-26", "2007-09-26", "2008-09-24", "2009-09-16", "2010-06-08",
                    "2011-09-02", "2012-12-26")),
  
  end = as.Date(c("1948-03-10", "1948-10-15", "1954-12-10", "1956-12-23", "1957-02-25",
                  "1960-07-19", "1964-11-09", "1972-07-07", "1974-12-09", "1976-12-24",
                  "1978-12-07", "1980-07-17", "1982-11-27", "1987-11-06", "1989-06-03",
                  "1989-08-10", "1991-11-05", "1993-08-09", "1994-04-28", "1994-06-30",
                  "1996-01-11", "1998-06-30", "2000-04-05", "2001-04-26", "2006-09-26",
                  "2007-09-26", "2008-09-24", "2009-09-16", "2010-06-08", "2011-09-02",
                  "2012-12-26", "2017-01-01")),
  stringsAsFactors = FALSE
)
```

With that out of the way we can load the unemployment data set and set about tidying out the raw data.

```{r load data, warning=FALSE}
# load data ---------------------------------------------------------------
japan_unemploy <- read.csv("~/R materials/Misc.ProjectsTutorials/japan_pm/LRUNTTTTJPM156S.csv", 
                           header = TRUE, stringsAsFactors = FALSE)
library(tibble)
glimpse(japan_unemploy)   # glimpse() is similar to using str() but tidier
```

  We can see here that the dates are in character format and that the column names are in all caps. We can convert the dates using the `as.Date()` function included in base R and change the column names to lower case using the `str_lower()` function from the **stringr** package:

```{r set date format, warning=FALSE}
library(stringr)

japan_unemploy$DATE <- as.Date(japan_unemploy$DATE, format = "%Y-%m-%d")

colnames(japan_unemploy) <- japan_unemploy %>% 
  colnames() %>% 
  str_to_lower()

glimpse(japan_unemploy)
```

Now, we need to change the column name for the unemployment data to something more reasonable:

```{r rename column, warning=FALSE}
japan_unemploy <- japan_unemploy %>% rename(unemployed = lrunttttjpm156s)

glimpse(japan_unemploy)

glimpse(prime_ministers)
```

Fantastic! Now we have two tidied data sets that we can use for our graph.

Let's start plotting!

  Here we use **ggrepel** package to prevent the labels from overlapping. `geom_vline()` and `geom_hline()` are used to create custom vertical and horizontal lines on the starting and ending dates of each Prime Minister's term and for the mean unemployment rate respectively.

```{r first plot, warning=FALSE}
library(ggrepel)  # to help with overlapping labels
library(scales)   # to help format scales and labels

japan_unemploy %>% 
  ggplot() +
  geom_line(
    aes(date, unemployed/100)
    ) +
  geom_vline(
    data = prime_ministers, 
    aes(xintercept = as.numeric(start)),
    color = "red", alpha = 0.5
    ) +
  geom_text_repel(
    data = prime_ministers %>% filter(start > japan_unemploy$date[1]),
    aes(x = start, y = 0.015, label = name)
    ) +
  scale_y_continuous(
    labels = percent_format()
    ) +
  geom_hline(
    yintercept = mean(japan_unemploy$unemployed/100), color = "blue", alpha = 0.5
    ) +
  labs(
    x = "Year", y = "Unemployment Rate (%)"
    ) +
  theme_bw()

```

  Looking at this graph, even with using `geom_text_repel()` there are too many Prime Ministers for it to look nice. This speaks for the highly turbulent "revolving door" of politics in Japan, especially in times of economic downturns such as in the 1990s and early 2000s (although many were caught in unrelated scandals or other kerfluffles too...). 

  To unclutter our graph, let's only show Prime Ministers whose term exceeded 2 years (730 days to be exact). 

```{r PM_term calculate}
(prime_ministers$end - prime_ministers$start) %>% head(8)   # only show results from first 8 rows
```

  By subtracting the starting dates from end dates we can calculate the length of each Prime Minister's term in days. The PM that lasted **64** days as shown is [Tanzan Ishibashi] <https://en.wikipedia.org/wiki/Tanzan_Ishibashi>, who unfortunately was incapacitated by stroke. Others such as  [Sosuke Uno] <https://en.wikipedia.org/wiki/S%C5%8Dsuke_Uno> (**68** days) resigned in more acrimonious terms (allegations of an extramarital affair with a **geisha** leading to a terrible performance in the subsequent election! Details can be read in *Secrets, Sex, and Spectacle: The Rules of Scandal in Japan and the United States* by Mark West if you're **really** curious).

Now we just have to use mutate() to add this data into a new column:
```{r PM_term add}
prime_ministers <- prime_ministers %>% mutate(pm_term = (end - start))
```

Now let's try plotting again:

```{r plot again}
# vertical line for each decade interval as scale_x_date() was being uncooperative...
grid_year <- as.Date(c("1960-01-01",
                       "1970-01-01", 
                       "1980-01-01", 
                       "1990-01-01", 
                       "2000-01-01", 
                       "2010-01-01"))

# second try!

japan_unemploy %>% 
  ggplot() +
  geom_line(
    aes(date, unemployed/100)) +
  geom_vline(
    data = prime_ministers, 
    aes(xintercept = as.numeric(start)),
    color = "blue", alpha = 0.5) +
  geom_vline(
    xintercept = as.numeric(grid_year), color = "#636363") +
  geom_text_repel(
    data = prime_ministers %>% filter(start > japan_unemploy$date[1], pm_term > 730),
    aes(x = start, y = 0.06, label = name), nudge_x = 10
  ) +
  scale_y_continuous(
    labels = percent_format(), 
    limits = c(0.0, 0.07),
    expand = c(0, 0)) +
  geom_hline(
    yintercept = median(japan_unemploy$unemployed/100), color = "red") +
  labs(
    x = "Year", y = "Unemployment Rate (%)") +
  theme_bw()

```

Much better!
