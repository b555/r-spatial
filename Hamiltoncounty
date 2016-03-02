# Code for generating a plot of Hamilton county using the shapefile
# Need to add the necessary variables (eg: Occupancy) to the dbf file before uploading the shapefile
# Code created - Bhargav 10:30 AM 3/1/2016


# Use the below packages as necessary 
# install.packages("rgdal")
# library(rgdal)     # R wrapper around GDAL/OGR
# library(ggplot2)   # for general plotting
# 
# install.packages("geosphere")
# library(geosphere)
# 
# install.packages("rgeos")
# library(rgeos)
# 
# install.packages("maptools")
# library(maptools)

# First read in the shapefile, using the path to the shapefile and the shapefile name minus the
# extension as arguments

require(ggplot2)

shapefile <- readOGR(dsn=path.expand("C:\\Users\\gannavnv\\Downloads\\Maptiles"), layer="tl_2010_39061_tract10")

shapefile@data$id<-rownames(shapefile@data)

# Next the shapefile has to be converted to a dataframe for use in ggplot2
rm(shapefile_df)
shapefile_df <- fortify(shapefile,region="GEOID10")

unique(shapefile_df$id)

colnames(shapefile_df)[6]<-"GEOID10"

require(plyr)
shapefile_final = join(shapefile_df, shapefile@data, by="GEOID10")


map <- ggplot(shapefile_final) +
  geom_polygon(aes(x=long,y=lat,group=GEOID10,fill=OCC14)) +
  geom_path(data = shapefile_final, 
            aes(x = long, y = lat, group = GEOID10),
            color = 'gray', size = .2) + coord_equal() +
theme_bw() + xlab("Longitude") + ylab("Latitude") 

plot(map)



