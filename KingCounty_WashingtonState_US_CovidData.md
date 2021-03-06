HW3\_CovidData
================
Olubusayo Bolonduro
7/19/2020

## Overview

Both the first coronavirus case in the US and the first
coronavirus-related death were confirmed in Washington State. The first
case was confirmed on January 21st, while Seattle and King County
confirmed the first death on February 29th. Given that I was born and
raised in the King County Seattle area, these reports truly did hit too
close to home.

For this assignment I wanted to observe county-level, state-level, and
U.S. National-level trends for confirmed COVID-19 cases using COVID-19
data from King County and Washington State.

``` r
library(ggplot2)
library(dplyr)
```

    ## Warning: package 'dplyr' was built under R version 3.6.2

## Importing COVID-19 data

``` r
counties <- read.csv(url("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-counties.csv"))
states <- read.csv(url("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv"))
us <- read.csv(url("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us.csv"))

king_county <- counties %>%
  filter(county == "King")
washington_state <- states%>%
  filter(state == "Washington")
```

## Plotting Data

``` r
## individual plots for Cases

king_county$date <- as.Date(king_county$date)
#2,252,782 King County residents according to 2019 census data
kingcounty_plot <- ggplot(king_county, aes(date, cases/2252782 * 100)) +
  geom_point()+
  labs(x="Month", y = "Percent of Population with Confirmed Cases", title = "King County Confirmed Cases")+
  theme(plot.title = element_text(hjust = 0.5))
  #scale_x_date(date_labels = "%b")
#kingcounty_plot

washington_state$date <- as.Date(washington_state$date)
#7,614,893 Washington state residents accoding to 2019 census data
washingtonstate_plot <-ggplot(washington_state, aes(date, cases/7614893 * 100)) +
  geom_point()+
  labs(x="Month", y = "Percent of Population with Confirmed Cases", title = "Washington State Confirmed Cases")+
  theme(plot.title = element_text(hjust = 0.5))
  #scale_x_date(date_labels = "%b")
#washingtonstate_plot

us$date <-as.Date(us$date)  
#328,239,523 US residents according to 2019 census data
us_plot<- ggplot(us, aes(date, cases/328239523 * 100)) +
  geom_point()+
  labs(x="Month", y = "Percent of Population with Confirmed Cases", title = "United States Confirmed Cases")+
  theme(plot.title = element_text(hjust = 0.5))
  #scale_x_date(date_labels = "%b")
#us_plot
    

##overlayed plot for Cases 

ggplot()+
  geom_line(data = king_county, aes(x = date,y = cases/2252782 * 100, color = 'green')) +
  geom_line(data = washington_state, aes(x = date, y = cases/7614893 * 100, color = 'blue'))+
  geom_line(data = us, aes(x = date, y = cases/328239523 * 100, color  = 'red'))+
  labs(x="Month", y = "Percent of Population with Confirmed Cases", color = "data", title = "Confirmed Cases")+
  theme(plot.title = element_text(hjust = 0.5))+
  scale_x_date(date_labels = "%b")+
  scale_color_discrete(name ="Key", labels = c("King County","Washington State","United States"))
```

![](KingCounty_WashingtonState_US_CovidData_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->
