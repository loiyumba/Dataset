
### This is the r script to extract html table from website.    

```r
require(rvest)
require(stringr)

setwd("...\\Data\\uefa2016\\CompleteData\\corners")

corners <- read_html("http://www.uefa.com/uefaeuro/season=2016/statistics/round=2000448/teams/category=attacking/kind=corners/index.html")

cornersData <- corners %>% 
  html_nodes("table") %>% 
  .[[1]] %>% 
  html_table()

cornersData$Name <- substr(cornersData$Name, 6, 70)
cornersData$Name <- str_trim(cornersData$Name, side = "left")

write.csv(cornersData, "corners.csv", row.names = FALSE)
```
