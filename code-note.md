### dplyr
```
#apply functions(in the list) to each of the columns
df1[, c('Amyloid_Status',missing_names)] %>%
  group_by(Amyloid_Status) %>%
  summarise_all(.funs = list(missing_count = ~sum(is.na(.)))) 
```


### list
```
l<- list(a=1, b=list(1,2), c=dataframe)
l[2] 
l[[2]]
l[[2]][[1]]
```
- `[i]` gives you the `i`th element of the list, wrapped in a list structure. It maintains the list format and has an index, which can be useful in many contexts.
  
- `[[i]]` gives you the actual content of the `i`th element. If that content is atomic (like a number or a string), you'll get that value directly. If the content is a list or another complex structure (like a data frame), you'll get that structure without additional list wrapping.



