# Food Preparation Feature Biographies
This repository holds all data and code for the  paper "Bulbs and Biographies, Pine nuts and Palimpsests: Exploring Plant Diversity and Earth Oven Reuse at a Late Period Plateau Site." Below, we include all code for reproducing the statistical analyses and graphs.

Additional files include supplemental tables and csv files for visualizations.

-supplemental_tables.xlxs
	-ST1 Recalibrated radiocarbon dates
	-ST2 Count and weight sample results
	-ST3 Counts and weights standardized by density
	-ST4 Spot samples
	-ST5 Archaeological Upper Columbia River plant taxa
	-T1 Reprinted Table 1 in spreadsheet format
-seeds.csv
-veg.csv
-wood.csv

## R code
### Packages
```r
library("factoextra")
library("ggplot2")
library("dplyr")
library("tidyr")
library("fpc")
library("ggpubr")
library("RColorBrewer")
```

### Create color palette for visualizing paleobotanical data
```r
color <- get_palette(palette = "RdYlBu", 16) #color accessible
contrast_color <- get_palette(palette = "Paired", 16) #contrasting colors
contrast_color[11] <- "#900C3F" #change one color in above palette
```

### Fig 2 density bar chart
```r
#Seed data prep and visualization
seeds <- read.csv(file.choose(), fileEncoding="UTF-8-BOM")#read in seeds.csv
row.names(seeds) <- seeds$taxa
seeds[1] <- NULL
#translate seed density data to percentages
seed_percentage <- apply(seeds,  2, function(x){x*100/sum(x,na.rm=T)})
#Fig 4.2a barchart for seeds
plot.new()
barplot(seed_percentage, col = contrast_color)
#Visualize legend; legends are added in an image processing program since legend is large
plot.new()
legend("center", legend = c("Amaranth", "Bearberry", "Goosefoot",
                            "Hawthorn", "Sedge", "Spikerush", "Wild Buckwheet", 
                            "Frogbit", "Sandwort", "Ponderosa pine", "Knotweed", 
                            "Chokecherry", "Buttercup", "Dock", "Huckleberry", 
                            "Vetch"),
       col = c("#A6CEE3", "#438EC0", "#63A8A0", "#98D277", "#3BA432", "#B89B74",
               "#F16667", "#E62F27", "#F9A963", "#FE982C", "#900C3F", "#C3AAD2",
               "#7D54A5", "#B9A499", "#EAD27A", "#B15928"),
       pch=20 , pt.cex = 3, cex = 1)

#Vegetation data prep and visualization
veg <- read.csv(file.choose(), fileEncoding="UTF-8-BOM") #read in veg.csv
row.names(veg) <- veg$taxa
veg[1] <- NULL
#translate veg density data to percentages
veg_percentage <- apply(veg,  2, function(x){x*100/sum(x,na.rm=T)})
#remove any taxa that contribute to <1% of the feature's total vegetative material (in g)
veg_percentage[9,3] = 0 #ponderosa needles
veg_percentage[8,3] = 0 #bulb tissue
veg_percentage[7,7] = 0 #lodgepole needles
veg_percentage[8,7] = 0 #ponderosa needles
veg_percentage[1,6] = 0 #onion
veg_percentage[3,6] = 0 #ponderosa bundles
veg_percentage[7,6] = 0 #lodgepole needles
veg_percentage[8,6] = 0 #ponderosa needles
#Fig 4.2b barchart for vegetation
plot.new()
barplot(veg_percentage, col = contrast_color)
#Visualize legend; legends are added in an image processing program since legend is large
plot.new()
legend("center", legend = c("Nodding onion", "Camas", "Pine needle fasicle", "Whitebark pine shoots",
                            "Whole lodgepole pine cones", "Fragmented lodgepole pine cones", "Lodgepole pine needles",
                            "Ponderosa pine needles", "Undet bulb tissue", "Undet fruit tissue"),
       col = c("#A6CEE3", "#438EC0", "#63A8A0", "#98D277", "#3BA432", "#B89B74",
               "#F16667", "#E62F27", "#FF5733", "#FE982C", "#900C3F", "#C3AAD2",
               "#7D54A5", "#B9A499", "#EAD27A", "#B15928"),
       pch=20 , pt.cex = 3, cex = 1)

#Wood charcoal data prep and visualization
wood <- read.csv(file.choose(), fileEncoding="UTF-8-BOM") #read in wood.csv
row.names(wood) <- wood$taxa
wood[1] <- NULL
#translate wood char density data to percentages
wood_percentage <- apply(wood,  2, function(x){x*100/sum(x,na.rm=T)}) 
#remove any taxa that contribute to <1% of the feature's total wood material (in g)
wood_percentage[2,1] = 0 #pine family
wood_percentage[11,3] = 0 #Willow family
wood_percentage[11,5] = 0 #Willow family
wood_percentage[13,5] = 0 #hardwood
wood_percentage[8,6] = 0 #fir/hemlock
wood_percentage[11,6] = 0 #willow family
wood_percentage[13,6] = 0 #hardwood
wood_percentage[6,7] = 0 #Doug fir
#Fig 4.2c wood charcoal bar graphs
plot.new()
barplot(wood_percentage, col = contrast_color)
#Visualize legend; legends are added in an image processing program since legend is large
plot.new()
legend("right", legend = c("Softwood", "Pine family", "Pine genera", "Lodgepole pine", 
                         "Ponderosa pine", "Doug fir", "Hemlock", "Fir/Hemlock",
                         "Spruce/Larch", "Hardwood", "Willow/Poplar", "Willow", "Undet Angiosperm"),
                         col = c("#A6CEE3", "#438EC0", "#63A8A0", "#98D277", "#3BA432", "#B89B74",
                                 "#F16667", "#E62F27", "#FF5733", "#FE982C", "#900C3F", "#C3AAD2",
                                 "#7D54A5", "#B9A499", "#EAD27A", "#B15928"),
       pch=20 , pt.cex = 3, cex = 1 )
```

###Supp. Fig. 2
```
#Supplemental Figure 2, in accessible color palette
#seed density visualization
#data prep
seeds <- read.csv(file.choose(), fileEncoding="UTF-8-BOM")#read in seeds.csv
row.names(seeds) <- seeds$taxa
seeds[1] <- NULL
#translate seed density data to percentages
seed_percentage <- apply(seeds,  2, function(x){x*100/sum(x,na.rm=T)})
#Fig 4.2a barchart for seeds
plot.new()
barplot(seed_percentage, col = contrast_color)
#Visualize legend; legends are added in an image processing program since legend is large
plot.new()
legend("center", legend = c("Amaranth", "Bearberry", "Goosefoot",
                            "Hawthorn", "Sedge", "Spikerush", "Wild Buckwheet", 
                            "Frogbit", "Sandwort", "Ponderosa pine", "Knotweed", 
                            "Chokecherry", "Buttercup", "Dock", "Huckleberry", 
                            "Vetch"),
       col = c("#A50026", "#C62026", "#E04430", "#F46D43", "#FA9856", "#FDBE70",
               "#FEE090", "#FEF4AF", "#F4FBD2", "#E0F3F7", "#BCE1EE", "#98CAE1",
               "#74ADD1", "#5487BD", "#3E60A9", "#313695"),
       pch=20 , pt.cex = 3, cex = 1)

#Vegetation data visualization
#data prep
veg <- read.csv(file.choose(), fileEncoding="UTF-8-BOM") #read in veg.csv
row.names(veg) <- veg$taxa
veg[1] <- NULL
#translate veg density data to percentages
veg_percentage <- apply(veg,  2, function(x){x*100/sum(x,na.rm=T)})
#Fig 4.2b barchart for vegetation
plot.new()
barplot(veg_percentage, col = color)
#Visualize legend; legends are added in an image processing program since legend is large
plot.new()
legend("center", legend = c("Nodding onion", "Camas", "Pine needle fasicle", "Whitebark pine shoots",
                            "Whole lodgepole pine cones", "Fragmented lodgepole pine cones", "Lodgepole pine needles",
                            "Ponderosa pine needles", "Undet bulb tissue", "Undet fruit tissue"),
       col = c("#A50026", "#C62026", "#E04430", "#F46D43", "#FA9856", "#FDBE70",
               "#FEE090", "#FEF4AF", "#F4FBD2", "#E0F3F7", "#BCE1EE", "#98CAE1",
               "#74ADD1", "#5487BD", "#3E60A9", "#313695"),
       pch=20 , pt.cex = 3, cex = 1)

#Wood charcoal visualization
wood <- read.csv(file.choose(), fileEncoding="UTF-8-BOM") #read in wood.csv
row.names(wood) <- wood$taxa
wood[1] <- NULL
#translate wood char density data to percentages
wood_percentage <- apply(wood,  2, function(x){x*100/sum(x,na.rm=T)}) 
#Fig 4.2c wood charcoal bar graphs
plot.new()
barplot(wood_percentage, col=color)
#Visualize legend; legends are added in an image processing program since legend is large
plot.new()
legend("center", legend = c("Softwood", "Pine family", "Pine genera", "Lodgepole pine", 
                            "Ponderosa pine", "Doug fir", "Hemlock", "Fir/Hemlock",
                            "Spruce/Larch", "Hardwood", "Willow/Poplar", "Willow", "Undet Angiosperm"),
       col = c("#A50026", "#C62026", "#E04430", "#F46D43", "#FA9856", "#FDBE70",
               "#FEE090", "#FEF4AF", "#F4FBD2", "#E0F3F7", "#BCE1EE", "#98CAE1",
               "#74ADD1", "#5487BD", "#3E60A9", "#313695"),
       pch=20 , pt.cex = 3, cex = 1 )
```

### K-means analyses Supp. Figs. 3-5
```r
#wood charcoal k-means analysis
wood_df <- scale(wood) #standardize density data
fviz_nbclust(wood_df, kmeans, method = "silhouette", k.max = 6) #check for clusters
wood.km <- eclust(wood_df, "kmeans", k=2, nstart = 25) #k-means analysis
fviz_cluster(wood.km, ellipse.type = "norm") #visualize k-means
#Remove/transpose data or re-run without outliers or run by features

#Seed data k-means
seeds_df <- scale(seeds) #standardize density data
fviz_nbclust(seeds_df, kmeans, method = "silhouette", k.max = 6) #find number of clusters
seeds.km <- eclust(seeds_df, "kmeans", k=2, nstart = 25) #k-means analysis
fviz_cluster(seeds.km, frame.type = "norm") #visualize kmeans
#Remove/transpose data or re-run without outliers or run by features

#Vegetation k-means analysis
veg_df <- scale(veg) #scale data
fviz_nbclust(veg_df, kmeans, method = "silhouette", k.max=6) #check number of clusters
veg.km <- eclust(veg_df, "kmeans", k=3, nstart = 25) #k-means analysis
fviz_cluster(veg.km, frame.type = "norm") #visualizing k-means
#Remove/transpose data or re-run without outliers or run by features
```

### Fischer's exact test for willow and geophytes
```r
willow_geo <- c(3, 0, 1, 6) #create vector and matrix for presence/absence of willow & geophytes
dim(willow_geo) <- c(2, 2)
fisher.test(willow_geo)
```