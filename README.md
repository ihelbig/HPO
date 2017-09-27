# HPO
#HPO analysis of RES families and 2017 HPO update
```
setwd("~/Dropbox/HPO_match/HPO")

obo <- read_lines("hp.obo.txt")

num = which(obo == '[Term]')

obox <- substr(obo[num+1],5,length(obo[num+1]))

#start here
obo_tab <- as.data.frame(matrix(nrow=length(obox),ncol=3))
names(obo_tab) <- c("HPO","is_a","term")
obo_tab[,1] <- obox

obo_counter = 1
for(i in 1:length(obo))
{
  if (obo[i] == "[Term]")
  {
    counter = i+1
    id <- obo[counter]
    name <- obo[counter+1]
    obo1 <- substr(id,5,999)
    obo2 <- substr(name,7,999)
    while(substr(id,1,6) != 'is_a: ')
    {
      counter = counter+1
      id <- obo[counter]
      obo3 <- substr(obo[counter],7,16)
    }
    obo_tab[obo_counter,1] <- obo1
    obo_tab[obo_counter,2] <- obo2
    obo_tab[obo_counter,3] <- obo3
    obo_counter = obo_counter+1
    print(paste(obo1,obo2,obo3))
  }
  
}
#this provides a table with the following properties
#HPO term, name, "is_a"
obo_tab[1:100,]
```
