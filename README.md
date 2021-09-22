---
title: "Biketrip_in_London_2015_to_2017"
author: "Odia"
date: "9/22/2021"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## R Markdown

This is an analysis to show the station with the highest number of bike trip rental in London from 2015 to 2017 and to know more about this analysis you can reach me via email at <odiamarshal7@gmail.com>.

Firstly, I had to clean my dataset and have a good column name and remove duplicate rows 
```{r}
colnames(biketrip)
glimpse(biketrip)
clean_names(biketrip)
biketrip1<-biketrip[!duplicated(biketrip),]
```
secondly, I found out that  Hyde Park Corner, Hyde Park has the highest number of rentals as it accounted for 941 rentals in the year 2015 to 2017
```{r}
biketrip2<-biketrip1%>%
  count(start_station_name)
biketrip3<-biketrip2%>%
  mutate(average_showing_the_time_bike_was_rented_from_this_station=n/36044)
```
Thirdly, I found the station with the highest number of rental in each year which station  Hyde Park Corner, Hyde Park top the list in year 2015= 452,2016= 340,2017=149
```{r}
biketrip1$year<-format(biketrip1$start_date, format="%Y")
biketrip4<-filter(biketrip1,year==2015)
biketrip5<-biketrip4%>%
  count(start_station_name)
biketrip6<-biketrip5%>%
  mutate(average_showing_the_time_bike_was_rented_from_this_station=n/15100)
##this shows that Hyde Park Corner, Hyde Park has the highest number of rentals in the year 2015 with 452 number of rentals
biketrip7<-filter(biketrip1,year==2016)
biketrip8<-biketrip7%>%
  count(start_station_name)
biketrip9<-biketrip8%>%
  mutate(average_showing_the_time_bike_was_rented_from_this_station=n/14800)
##this shows that Hyde Park Corner, Hyde Park has the highest number of rentals in the year 2016 with 340 number of rentals
biketrip10<-filter(biketrip1,year==2017)
biketrip11<-biketrip10%>%
  count(start_station_name)
biketrip12<-biketrip11%>%
  mutate(average_showing_the_time_bike_was_rented_from_this_station=n/6144)
##this shows that Hyde Park Corner, Hyde Park has the highest number of rentals in the year 2017 with 149 number of rentals
```
This shows that hyde park corner,hyde park number of sales has being reducing over the years and it really reduced drastically in year 2017. Therefore, I have to find the reason why.
```{r}
biketrip13<-biketrip1%>%
  count(end_station_name)
biketrip14<-filter(biketrip1,start_station_name=="Hyde Park Corner, Hyde Park",end_station_name=="Speakers' Corner 1, Hyde Park")
biketrip20<-biketrip14%>%
  count(end_station_name)
biketrip15<-filter(biketrip1,start_station_name=="Hyde Park Corner, Hyde Park",end_station_name=="Hyde Park Corner, Hyde Park")
biketrip21<-biketrip15%>%
  count(end_station_name)
biketrip16<-filter(biketrip4,start_station_name=="Hyde Park Corner, Hyde Park",end_station_name=="Hyde Park Corner, Hyde Park")
biketrip22<-biketrip16%>%
  count(end_station_name)
## in the year 2015 105 people booked bike that the end station was Hyde Park Corner, Hyde Park 
biketrip17<-filter(biketrip7,start_station_name=="Hyde Park Corner, Hyde Park",end_station_name=="Hyde Park Corner, Hyde Park")
biketrip23<-biketrip17%>%
  count(end_station_name)
## in the year 2016 80 people booked bike that the end station was Hyde Park Corner, Hyde Park
biketrip18<-filter(biketrip10,start_station_name=="Hyde Park Corner, Hyde Park",end_station_name=="Hyde Park Corner, Hyde Park")
biketrip24<-biketrip18%>%
  count(end_station_name)
## in the year 2017 36 people booked bike that the end station was Hyde Park Corner, Hyde Park
```
this shows part of the reasons why they lost sales was because the number of rentals with end location hyde park corner, hyde park reduced drastically over the years
My recommendation is they should offer discount prices for a period of time to bike rentals which their end station or final destination is also the hyde park corner, hyde park so they could get back their previous customers and also get new customers

This is a graph showing the start_station_name and the end_station_name
```{r}
ggplot(data=biketrip16)+ 
  geom_point(mapping=aes(x=start_station_name,y=end_station_name),color="green")+
  labs(title="Rentals with end station hyde park corner,hyde park at 105", caption="2015")
```
```{r}
ggplot(data=biketrip17)+ 
  geom_point(mapping=aes(x=start_station_name,y=end_station_name),color="green")+
  labs(title="Rentals with end station hyde park corner,hyde park at 80", caption="2016")
```
```{r}
ggplot(data=biketrip18)+ 
  geom_point(mapping=aes(x=start_station_name,y=end_station_name),color="green")+
  labs(title="Rentals with end station hyde park corner,hyde park at 36", caption=2017)
```
