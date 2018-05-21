# World-Bank-API-explore
Examples of how to find and download vars

# WB - API access

# Setup
setwd('~/R/Rdata')
x = c("wbstats", "data.table", "goolgeVis", "dplyr", "tidyr", "tmap", "stringr")
# install.packages(x)
lapply(x, library, character.only = TRUE)   

# WB
# Explore variables
str(wb_cachelist, max.level = 1)                                       # list of available data
new_cache <- wbcache()

countries <- data.table(wbcountries())                                 # countries
unemploy_vars <- wbsearch(pattern = "unemployment")                    # names of unemploy. vars
blmbrg_vars <- wbsearch(pattern = "Bloomberg", fields = "sourceOrg")   # vars supplied by bloomberg
povemply_vars <- wbsearch(pattern = "poverty|unemployment|employment") # poverty OR unemployment OR employment

# Retrieving data
pop_gdp_long <- wb(country = c("US", "NO"), 
                   indicator = c("SP.POP.TOTL", "NY.GDP.MKTP.CD"),
                   startdate = 1971, enddate = 1971)                   # returns long format by default

pop_gdp_wide <- wb(country = c("US", "NO"), 
                   indicator = c("SP.POP.TOTL", "NY.GDP.MKTP.CD"),
                   startdate = 1971, enddate = 1971, 
                   return_wide = TRUE)                                 # wide format


pop_gdp_wide_10 <- wb(country = c("US", "NO"), 
                   indicator = c("SP.POP.TOTL", "NY.GDP.MKTP.CD"),
                   mrv = 10, 
                   return_wide = TRUE)                                 # mrv to get most recent 'n' periods 
 
