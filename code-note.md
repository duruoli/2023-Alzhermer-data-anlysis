### dplyr
```
#apply functions(in the list) to each of the columns
df1[, c('Amyloid_Status',missing_names)] %>%
  group_by(Amyloid_Status) %>%
  summarise_all(.funs = list(missing_count = ~sum(is.na(.)))) 
```


### MICE

