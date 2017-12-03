---
layout: post
title: "Where to live in Japan: XKCD-themed climate plots and maps!"
fb-img: https://ryo-n7.github.io/assets/2017-11-22-japan-xkcd-weather-index_files/xkcd-graph-1.png
share-img: https://ryo-n7.github.io/assets/2017-11-22-japan-xkcd-weather-index_files/xkcd-graph-1.png 
tags: [xkcd, riem, weather, climate, maps, japan, ggplot2]
---

In the past week or so, XKCD graphs of "The most comfortable place to live in ___" have been popping up on the \#rstats community on Twitter. Jumping onto this trend (though slightly late), I will do one for Japan, the country where I was born! Some great examples that I've seen so far include [Ma&euml;lle Salmon's](http://www.masalmon.eu/2017/11/16/wheretoliveus/) blog post for cities in the USA (which started this trend), as well as ones for [Spain](https://twitter.com/claudiaguirao/status/931615734521909248), [Germany](https://franziloew.github.io/xkcd_weather_cities_de/weatherdata.html), [Netherlands](http://rmhogervorst.nl/cleancode/blog/2017/11/20/xkcd-the-netherlands-weather.html), and even for all of [Europe](https://twitter.com/matamix/status/932192147062784000)! The original XKCD comic can be seen [here](https://xkcd.com/1916/).

Let's get started!

``` r
library(riem)

riem_stations(network = "JP__ASOS")
```

    ## # A tibble: 136 x 4
    ##       id             name      lon      lat
    ##    <chr>            <chr>    <dbl>    <dbl>
    ##  1  RORA AGUNI ISLAND     127.2403 26.59277
    ##  2  RJOE AKENO (JASDF)    136.6722 34.53333
    ##  3  RJSK AKITA AIRPORT    140.2167 39.61667
    ##  4  RJKA AMAMI AIRPORT    129.7125 28.43083
    ##  5  RJSA AOMORI AIRPORT   140.6886 40.73333
    ##  6  RJEC ASAHIKAWA AIRPOR 142.4475 43.67083
    ##  7  RJCA ASAHIKAWA (JASDF 142.3650 43.79444
    ##  8  RJFA ASHIYA (JASDF)   130.6517 33.88139
    ##  9  RJTA ATSUGI NAS (JMSD 139.4500 35.45472
    ## 10  RJAO CHICHIJIMA ISLAN 142.1900 27.09167
    ## # ... with 126 more rows

Using Ma&euml;lle Salmon's `riem` package we can look up weather data from all over the world collected at airport weather stations. We can see that there are 136 different stations (and airports) in Japan's network! From the `ID` we can also see that the airports are coded in the **ICAO** standard rather than the **IATA** standard, this will come into play later!

For which exact cities to choose, I took a note from Ma&euml;lle's article where she searched for the cities with the busiest airports. This makes sense as the weather data we will gather and the airport data will then have a similar column (the ICAO code) on which we can join on!

My source was from the **Ministry of Land, Infrastructure, Transport and Tourism (MLIT)** statistics on Japan's busiest airports (in terms of total passenger traffic), which has been copied onto everybody's favorite "knowledge bank", Wikipedia ([link](https://en.wikipedia.org/wiki/List_of_the_busiest_airports_in_Japan))! The most recent list is from 2015 and although I could look up more recent figures I don't think two years would make such a big difference (... and I'm lazy).

I load up my favorite web scraping package, `rvest` and gather the list of airports! (For a step-by-step intro to web-scraping using R, check out my other blog post [here](https://ryo-n7.github.io/2017-09-18-global-peace-index/)!)

``` r
library(rvest)
library(dplyr)

url <- "https://en.wikipedia.org/wiki/List_of_the_busiest_airports_in_Japan"

# css selector: "table.wikitable:nth-child(10)"

japan_airports <- url %>% 
  read_html() %>% 
  html_node("table.wikitable:nth-child(10)") %>% 
  html_table()

glimpse(japan_airports)
```

    ## Observations: 51
    ## Variables: 8
    ## $ Rank           <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, ...
    ## $ Airport        <chr> "Haneda Airport", "Narita International Airport...
    ## $ `City\nserved` <chr> "Tokyo", "Tokyo", "Osaka", "Fukuoka", "Sapporo"...
    ## $ Region         <chr> "Kanto", "Kanto", "Kansai", "Kyushu", "Hokkaido...
    ## $ `IATA/ICAO`    <chr> "HND/RJTT", "NRT/RJAA", "KIX/RJBB", "FUK/RJFF",...
    ## $ Passengers     <chr> "75,254,942", "34,751,221", "23,136,223", "20,9...
    ## $ Aircraft       <chr> "438,542", "233,500", "163,506", "172,964", "14...
    ## $ Cargo          <chr> "1,173,752", "2,122,318", "745,606", "262,481",...

In the table, the airport codes in both IATA and ICAO format are in a single column separated by a slash. We can use the `separate()` function from the `tidyr` package to separate the airport code column into the respective IATA and ICAO codes. The regex for a literal slash is `"\\/"`, remember that you need to escape twice!

Let's also rename `City\nserved` into a simpler `City`.

Then, let's **save** our handy dataset so we do not have to re-run web scraping every time!

``` r
# Separate IATA and ICAO codes:
library(tidyr) # use separate() function!

japan_airports <- japan_airports %>% 
  separate(`IATA/ICAO`, c("IATA", "ICAO"), "\\/")

japan_airports <- japan_airports %>% rename(City = `City\nserved`)

write.csv(japan_airports, "~/R_materials/japan_weather_xkcd/japan_airports.csv")
```

So, if we start a new session we can use `read.csv()` to load our data set without have to go through the web scraping code!

``` r
japan_airports <- read.csv("~/R_materials/japan_weather_xkcd/japan_airports.csv", 
         stringsAsFactors = FALSE)

# We only need a small subset of the variables for this particular blog post!
jp_airport_codes <- japan_airports %>% select(Airport, City, ICAO)

glimpse(jp_airport_codes)
```

    ## Observations: 51
    ## Variables: 3
    ## $ Airport <chr> "Haneda Airport", "Narita International Airport", "Kan...
    ## $ City    <chr> "Tokyo", "Tokyo", "Osaka", "Fukuoka", "Sapporo", "Naha...
    ## $ ICAO    <chr> "RJTT", "RJAA", "RJBB", "RJFF", "RJCC", "ROAH", "RJOO"...

Weather data
------------

For the weather data I considered quite a few sources before just settling with the `riem` package for convenience.

* The first place I looked was the Japan Meteorological Agency's website in both English and Japanese. If you go [here](http://www.data.jma.go.jp/obd/stats/koku/kikohyo/kikohyomain_e.html) you can find the the climatological tables for all Japanese airports in English. You can download the entire data set as a .zip file (click on "File" on the top header) or you can click on each airport (with its corresponding ICAO location indicator) to grab its report.
* You can also find in English, [here](http://www.data.jma.go.jp/obd/stats/data/en/smp/index.html), the tables of monthly climate statistics with drop-down menus for each station and for different variables such as "monthly mean air temperature", "monthly vapor pressure", etc.
* Probably the most useful tables for a quick glance is [here](http://www.data.jma.go.jp/obd/stats/data/en/normal/normal.html), which shows tables for monthly and annual climate normals for the major observatories in Japan from 1981-2010.
* For Japanese people there is a built-in API on the website ([here!](http://www.data.jma.go.jp/gmd/risk/obsdl/index.php)) that lets you choose from a multitude of different options and download your own customized dataset as a CSV file.

Just putting this out there for anybody who wants to look at Japan's meteorological data in the future!

Now to grab the weather data from the weather stations using the `riem` package, we use code from Ma&euml;lle Salmon's original post where we use `map_df()` to basically to apply `riem_measures()` on each airport code (as a vector input) with the output being a nice data frame! I've been slowly trying to incorporate more purrr into my data analysis tool set, so it's great that I get another chance to see it in action here!

``` r
library(purrr)
library(riem)

summer_weather <- map_df(jp_airport_codes$ICAO, riem_measures,
                                date_start = "2017-06-01",
                                date_end = "2017-08-31")

winter_weather <- map_df(jp_airport_codes$ICAO, riem_measures,
                                date_start = "2016-12-01",
                                date_end = "2017-02-28")

# As before we save these as .csv files:
write.csv(summer_weather, "~/R_materials/japan_weather_xkcd/summer_weather.csv")
write.csv(winter_weather, "~/R_materials/japan_weather_xkcd/winter_weather.csv")

# Load them back in after opening a new session instead of waiting to download from RIEM package again:
summer_weather <- read.csv("summer_weather.csv", stringsAsFactors = FALSE)
winter_weather <- read.csv("winter_weather.csv", stringsAsFactors = FALSE)
```

The result is two gigantic datasets of around 105,000 observations each along with 25 variables ranging from dew point temperature, wind speed in knots, relative humidity, and many more!

Further data munging
--------------------

Recalculate the temperatures into **Celcius** using the `convert_temperature()` function in the `weathermetrics` package!

A quick reminder that the formula is: $$\large\frac{(Fahrenheit - 32)\cdot5}{9} = Celsius$$

``` r
library(weathermetrics)

summer_weather <- summer_weather %>% 
                    mutate(tmpc = convert_temperature(tmpf,
                                                      old_metric = "f", 
                                                      new_metric = "c"),
                           dwpc = convert_temperature(dwpf,
                                                      old_metric = "f",
                                                      new_metric = "c"))

winter_weather <- winter_weather %>% 
  mutate(tmpc = convert_temperature(tmpf,
                                    old_metric = "f", 
                                    new_metric = "c"))
```

We can then calculate the **Humidex** with the `calcHumx()` function from the `comf` package!

For those curious the formula is: $$\large Temperature (Celsius) + 0.5555\left(6.11e^{5417.753(\frac{1}{273.16}-\frac{1}{273.15+Dew Point})} - 10\right)$$

The interpretation of the humidex is as follows:

-   20-29: Little to no discomfort
-   30-39: Some discomfort
-   40-45: Great discomfort (avoid exertion)
-   45+ : Dangerous (possibility of heat stroke)

``` r
library(comf)

summer_weather <- summer_weather %>% 
                    mutate(humidex = calcHumx(ta = tmpc, rh = dwpc))

summer_data <- summer_weather %>% 
                 group_by(station) %>% 
                 summarize(summer_avg_temp = mean(tmpc, na.rm = TRUE),
                           summer_humidex = mean(humidex, na.rm = TRUE))

winter_data <- winter_weather %>% 
                 group_by(station) %>% 
                 summarize(winter_avg_temp = mean(tmpc, na.rm = TRUE))
```

Join summer and winter together using the `left_join()` operation! Then, join with the `jp_airport_codes` data set to add in city names to airport code data set, combine them by the airport ICAO code.

``` r
climate_japan <- left_join(summer_data, winter_data, by = "station")

climate_japan <- left_join(climate_japan, jp_airport_codes,
                           by = c("station" = "ICAO"))

glimpse(climate_japan)
```

    ## Observations: 48
    ## Variables: 6
    ## $ station         <chr> "RJAA", "RJAH", "RJBB", "RJBE", "RJCB", "RJCC"...
    ## $ summer_avg_temp <dbl> 24.20110, 23.46787, 26.08489, 26.42125, 18.908...
    ## $ summer_humidex  <dbl> 22.32085, 21.24909, 24.80028, 25.49317, 15.330...
    ## $ winter_avg_temp <dbl> 5.5732117, 4.9624521, 8.2165839, 8.0681648, -5...
    ## $ Airport         <chr> "Narita International Airport", "Ibaraki Airpo...
    ## $ City            <chr> "Tokyo", "Tokyo", "Osaka", "Kobe", "Obihiro", ...

Looking at what we have... we can remove Narita Airport's data as not it's not *really* Tokyo, it's located far out in Chiba, and besides the airport there's nothing of interest (to tourists at least) out there anyways! Haneda Airport's data is more representative of Tokyo's weather, although it is stuck out in Tokyo Bay.

Also we need to remove Kansai International Airport, as it is around 20 miles away from all the attractions in Osaka. Fun fact: Kansai Int'l was built to relieve congestion in Osaka Airport (also included in this data set) and only handles international flights!

``` r
climate_japan <- climate_japan %>% filter(station != "RJAA")    # RJAA == Narita Airport

climate_japan <- climate_japan %>% filter(station != "RJBB")    # RJBB == Kansai Int'l Airport
```

For some odd reason Ibaraki Airport is listed as Tokyo, when it is anything but! Also, we should shorten Kochi's label, the plot is going to be cluttered enough as it is!

``` r
climate_japan$City[climate_japan$station == "RJAH"] <- "Ibaraki"   # Tokyo >>> Ibaraki

climate_japan$City[climate_japan$station == "RJOK"] <- "Kochi"     # Kochi, Kochi >>> Kochi
```

Iwakuni appears twice for some reason... very odd, but we can remove it by using the `unique()` function which filters out any duplicate rows.

``` r
climate_japan <- climate_japan %>% unique()

glimpse(climate_japan)
```

    ## Observations: 45
    ## Variables: 6
    ## $ station         <chr> "RJAH", "RJBE", "RJCB", "RJCC", "RJCH", "RJCK"...
    ## $ summer_avg_temp <dbl> 23.46787, 26.42125, 18.90891, 18.28105, 19.112...
    ## $ summer_humidex  <dbl> 21.24909, 25.49317, 15.33031, 14.82229, 15.733...
    ## $ winter_avg_temp <dbl> 4.9624521, 8.0681648, -5.6058944, -4.8474507, ...
    ## $ Airport         <chr> "Ibaraki Airport", "Kobe Airport", "Obihiro Ai...
    ## $ City            <chr> "Ibaraki", "Kobe", "Obihiro", "Sapporo", "Hako...

Great! Our data set looks ready!

Plotting!
---------

Well, before actually plotting, we have to install the **xkcd** font and package. You can read about how to install it [here](https://cran.r-project.org/web/packages/xkcd/xkcd.pdf).

``` r
library(ggplot2)
library(ggrepel)
library(xkcd)
library(extrafont)

xrange <- range(climate_japan$summer_humidex)
yrange <- range(climate_japan$winter_avg_temp)

set.seed(8)

climate_japan %>% 
  ggplot(aes(summer_humidex, winter_avg_temp)) +
  geom_point() +
  geom_text_repel(aes(label = City), 
                  family = "xkcd",
                  max.iter = 50000) +
  ggtitle("Where to live in Japan based on your temperature preferences",
          subtitle = "Data from airport weather stations 2016-2017") +
  xlab("Humidex: summer heat and humidity") +
  ylab("Avg. winter temperature in Celsius") +
  xkcdaxis(xrange = xrange,
           yrange = yrange) +
  theme_xkcd() +
  theme(text = element_text(size = 16, family = "xkcd")) +
  theme(text = element_text(size = 16, family = "xkcd")) +
  annotate("text", x = 14, y = 1.25, label = "Hokkaido Island", family = "xkcd", size = 5) +
  annotate("segment", y = 1.25, yend = -5.5, x = 16, xend = 17.5, color = "blue", size = 1.5) +
  annotate("segment", y = -4.25, yend = -6.5, x = 11.75, xend = 13.5, color = "blue", size = 1.5) +
  annotate("text", x = 25, y = 20, label = "Okinawa and \nRyukyu Islands", family = "xkcd", size = 5) +
  annotate("segment", y = 17.5, yend = 15, x = 26, xend = 29.5, color = "darkred", size = 1.5) +
  annotate("segment", y = 22, yend = 22, x = 27, xend = 30.5, color = "darkred", size = 1.5) +
  annotate("text", x = 16.5, y = 10, label = "Honshu, Kyushu, \n and Shikoku Islands", family = "xkcd", size = 5.5)
```

<img src="../assets/2017-11-22-japan-xkcd-weather-index_files/xkcd-graph-1.png" style="display: block; margin: auto;" />

The graph looks like a map of Japan... with cities in Hokkaido on the bottom left instead of the top right, vice-versa for Okinawa! Let's try plotting our data onto an actual map of Japan to get a different perspective.

Weather data on the map of Japan
--------------------------------

First we need to acquire the longitude and latitude data for Japan with the `map_data()` function in ggplot2. We also need to add in the coordinate data into our climate\_japan dataset.

``` r
JPN <- map_data(map = "world", region = "Japan")

lat_lon <- summer_weather %>% 
  group_by(station) %>% 
  summarize(lat = mean(lat), lon = mean(lon))

climate_japan_map <- left_join(climate_japan, lat_lon, by = "station") 

glimpse(climate_japan_map)
```

    ## Observations: 45
    ## Variables: 8
    ## $ station         <chr> "RJAH", "RJBE", "RJCB", "RJCC", "RJCH", "RJCK"...
    ## $ summer_avg_temp <dbl> 23.46787, 26.42125, 18.90891, 18.28105, 19.112...
    ## $ summer_humidex  <dbl> 21.24909, 25.49317, 15.33031, 14.82229, 15.733...
    ## $ winter_avg_temp <dbl> 4.9624521, 8.0681648, -5.6058944, -4.8474507, ...
    ## $ Airport         <chr> "Ibaraki Airport", "Kobe Airport", "Obihiro Ai...
    ## $ City            <chr> "Ibaraki", "Kobe", "Obihiro", "Sapporo", "Hako...
    ## $ lat             <dbl> 36.1817, 34.6328, 42.7333, 42.7742, 41.7700, 4...
    ## $ lon             <dbl> 140.4147, 135.2239, 143.2172, 141.6926, 140.82...

To be able to view the map better, we can cut out the Okinawa and Ryukyu Islands to create space by filtering out latitudes below 30°. We will create a separate map for those islands too.

``` r
# Winter avg. temp: ####

climate_japan_map %>% 
  filter(lat > 30) %>% 
  ggplot(aes(lon, lat)) +
  geom_point(aes(color = winter_avg_temp), size = 3.5) +
  geom_text_repel(aes(label = City),
                  family = "xkcd", size = 4.5,
                  max.iter = 50000) +
  geom_polygon(data = JPN %>% filter(lat > 30), aes(x = long, y = lat, group = group), 
               fill = NA, color = "black") +
  coord_map() +
  labs(title = "Avg. Winter Temperature in Japan",
       subtitle = "Data from Iowa Environment Mesonet 2016-2017",
       x = "", y = "") +
  theme_xkcd() +
  theme(text = element_text(family = "xkcd", size = 14)) +
  scale_color_gradient(low = "#08306B")
```

<img src="../assets/2017-11-22-japan-xkcd-weather-index_files/Japan-maps-1.png" style="display: block; margin: auto;" />

``` r
# Humidex: ####

climate_japan_map %>% 
  filter(lat > 30) %>% 
  ggplot(aes(lon, lat)) +
  geom_point(aes(color = summer_humidex), size = 3.5) +
  geom_text_repel(aes(label = City),
                  family = "xkcd", size = 4.5,
                  max.iter = 50000) +
  geom_polygon(data = JPN %>% filter(lat > 30), aes(x = long, y = lat, group = group), 
               fill = NA, color = "black") +
  coord_map() +
  labs(title = "Summer Humidex across Japan",
       subtitle = "Data from Iowa Environment Mesonet 2016-2017",
       x = "", y = "") +
  theme_xkcd() +
  theme(text = element_text(family = "xkcd", size = 14)) +
  scale_color_gradient(low = "#FCBBA1", high = "#67000D")
```

<img src="../assets/2017-11-22-japan-xkcd-weather-index_files/Japan-maps-2.png" style="display: block; margin: auto;" />

A large area in the middle of Honshu Island that does not have any data is the Central Highland region, which is a very mountainous region and therefore there aren't any airport weather stations located there for our plot. This is a great area to go if you love to ski and relax in an onsen! In Nagano Prefecture you can go to [Jigokudani Monkey Park](http://en.jigokudani-yaenkoen.co.jp/) where you can see snow monkeys relaxing in the onsen!

![](https://i.imgur.com/AmNHCTz.jpg)

Now for the Okinawa and Ryukyu Islands:

``` r
climate_japan_map %>% 
  filter(lat < 30) %>% 
  ggplot(aes(lon, lat)) +
  geom_point(aes(color = winter_avg_temp), size = 3.5) +
  geom_text_repel(aes(label = City),
                  family = "xkcd", size = 4.5,
                  max.iter = 50000) +
  geom_polygon(data = JPN %>% filter(lat < 30 & long < 133), aes(x = long, y = lat, group = group), 
               fill = NA, color = "black") +
  coord_map() +
  labs(title = "Summer Humidex in Okinawa and Ryukyu Islands",
       subtitle = "Data from Iowa Environment Mesonet 2016-2017",
       x = "", y = "") +
  theme_xkcd() +
  theme(text = element_text(family = "xkcd", size = 14)) +
  scale_color_gradient(low = "#08306B")
```

![](..\assets\2017-11-22-japan-xkcd-weather-index_files\Okinawa-Ryukyu-map-1.png)

``` r
climate_japan_map %>% 
  filter(lat < 30) %>% 
  ggplot(aes(lon, lat)) +
  geom_point(aes(color = winter_avg_temp), size = 3.5) +
  geom_text_repel(aes(label = City),
                  family = "xkcd", size = 4.5,
                  max.iter = 50000) +
  geom_polygon(data = JPN %>% filter(lat < 30 & long < 133), aes(x = long, y = lat, group = group), 
               fill = NA, color = "black") +
  coord_map() +
  labs(title = "Avg. Winter Temperature in Okinawa and Ryukyu Islands",
       subtitle = "Data from Iowa Environment Mesonet 2016-2017",
       x = "", y = "") +
  theme_xkcd() +
  theme(text = element_text(family = "xkcd", size = 14)) +
  scale_color_gradient(low = "#FCBBA1", high = "#67000D")
```

![](..\assets\2017-11-22-japan-xkcd-weather-index_files\Okinawa-Ryukyu-map-2.png)

As we can see from all the maps, the differences are pretty obvious. The segmentations we saw in the Humidex/Avg. Winter Temperature graph can be clearly seen with the map. With Japan being such a narrow chain of islands going from as far north as Hokkaido to the warm beaches of Okinawa there aren't many surprises in the data. As Japan is known for it's very distinct four seasons, maybe I'll incorporate spring and autumn data for different blog post...! It can be **very** humid in Japan during the summer time, it feels like you are melting constantly and I much prefer the spring months of Japan, the beginning of which is heralded by the blooming of the sakura/cherry blossoms!

*Sidenote*: If you want to take a look at some data viz stuff I did with sakura blooming time data, check it out [here](https://ryo-n7.github.io/2017-09-10-sakura-bloom/)!

My next steps in this analysis would be to try to recreate a Köppen climate classification map of Japan using ggplot2 (learning how to use shape files and adding in layers on maps!) and also to try using `leaflet` to create a map of Japan with the winter temperature and humidex data that we gathered with the added bonus of tourist information in each of the city markers!

A screenshot of my leaflet sample:

![leaflet](https://i.imgur.com/6bgewvq.png)
