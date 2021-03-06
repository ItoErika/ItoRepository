## Lab 9
## Problem Set 1

> 20/20

1) Is North America currently (i.e., in the present) to the West or East of its position in the Cretaceous?

West 

2) Look at the following line of code that you used before.

`plot(ModernMap,col=rgb(1,0,0,0.33),lty=0,add=TRUE)`

<<<<<<< Updated upstream
Describe what this code is doing. A good answer will describe what each of theÂ plot( )Â functionÂ argumentsÂ is doing - i.e., what is the meaning of col=, lty= and add=. As well, what does theÂ rgb( )Â function do? What does it mean? Use google or the RÂ help( )Â function.
-the plot function plots R objects - it plots the object, ModernMap we created
-col specifies the plotting color
-the rgb function creates colors of different intensities, between zero and maximum, of red, blue, and green primaries. The first three integers in the parentheses after rgb controls the intensity of the colors red, green, and blue respectively. So the code above should plot in the color red. The fourth integer in the parentheses controls transparency. The rgb code refers to the standard sRGB colorspace.
-lty is the type of line as specified by an integer - having a line between  0 and 1 gives the line transparency
-add=TRUE allows you to add to existing plots, instead of making a new one. 

=======
Describe what this code is doing. A good answer will describe what each of the plot( ) function arguments is doing - i.e., what is the meaning of col=, lty= and add=. As well, what does the rgb( ) function do? What does it mean? Use google or the R help( ) function. 
-the plot function plots R objects - it plots the object, ModernMap we created
-col specifies the plotting color
-the rgb function creates colors of different intensities, between zero and maximum, of red, blue, and green primaries. The first three integers in the parentheses after rgb controls the intensity of the colors red, green, and blue respectively. So the code above should plot in the color red. The fourth integer in the parentheses controls transparency. The rgb code refers to the standard sRGB colorspace.
-lty is the type of line as specified by an integer - having a line between  0 and 1 gives the line transparency
-add=TRUE allows you to add to existing plots, instead of making a new one. 
>>>>>>> Stashed changes

3) Download a map of the middle Cretaceous (Albian Epochs ~110 mys ago). Name itÂ AlbianMap.
> AlbianMap<-downloadPaleogeography(Age=110)

4) AddÂ AlbianMapÂ to the plot you made earlier. The added continents should be colored green, and use the same level of opacity (translucence) as yourÂ CretaceousMapÂ andÂ ModernMap. Show your code!

````R
> plot(AlbianMap,col=rgb(0,1,0,0.33),lty=0,add=TRUE)
````

5) Has there been more movement north and south or east and west in the Eastern Hemisphere since the Albian?
North and South

6) Has there been more movement north and south or east and west in the Western hemisphere since the Albian?
East and West

## Problem Set 2
1) Download and plot a new map of the Paleocene/Eocene boundary (Use google to find the age of this boundary, remember theÂ downloadMap( )Â function only takes whole numbers). You may use any color and level of opacity. Show your code.

````R
> PEMap<-downloadPaleogeography(Age=56)
> plot(PEMap,col=rgb(0,1,1,0.33),lty=0.01)
````

2) Download a dataset of Anthozoan occurrences from the paleobiology database ranging from the Paleocene through Eocene. Consult with previous labs if you do not remember how to do this. Show your code.

````R
DataPBDB<-downloadPBDB(Taxa=c("Anthozoa"),StartInterval="Paleocene",StopInterval="Eocene")
````

3) How many occurences did you download?
2847

````R
> dim(DataPBDB)
[1] 2847   26
````

<<<<<<< Updated upstream

4) What are the names of columns of the PBDB data matrix you just downloaded. What does each column mean? If you do not know, consult with theÂ API documentation.
=======
>>>>>>> Stashed changes

````R
> colnames(DataPBDB)
 [1] "occurrence_no"   â€“ a unique number that identifies the occurrence
 [2] "record_type"     - the type of the object, (ex: occ for occurrence) 
 [3] "reid_no"         - a unique identifier for occurrences that have
                       been reidentified â€“ indicates whether or not it is the original identification of the occurrence.         
 [4] "flags"           - R indicates that the record representing an identification has been replaced by a more recent identification       
 [5] "collection_no"   - the identifier for the collection the occurrence belongs to 
 [6] "identified_name" â€“ the taxonomic name the occurrence was identified as
 [7] "identified_rank" â€“ the taxonomic rank of the taxonomic name given
 [8] "identified_no"   - a unique identifier for the taxonomic name 
 [9] "difference"      - gives the reason for which the identified name and 
                       accepted name are not the same. If this is blank, then they are the same. 
[10]"accepted_name"    - the accepted taxonomic name associated with the identified name 
[11] "accepted_rank"   - the taxonomic rank of the accepted name 
[12]"accepted_no"      - a unique identifier for the accepted taxonomic name
[13] "early_interval"  - the geologic interval that begins the range associated with the occurrence. Or geologic time range associated with occurrence
[14] "late_interval"   - the geologic interval that ends the range associated with the occurrence, if itâ€™s different than the early interval.
[15] "max_ma"          - the early bound for the geologic time range for the occurrence (in millions of years ago)
[16] "min_ma"          - the late bound for the geologic time range for the occurrence (in millions of years ago) 
[17] "reference_no"    - the identifier for the reference for the data
[18] "paleomodel"      - the primary model identified by the parameter pgm
[19] "paleolng"        - the paleolongitude of the collection

[20]"paleolat"         - the paleolatitude of the collection
[21] "geoplate"        - the identifier number of the geologic plate the collection came from 
[22]"phylum"           - the name of the phylum the occurrence belongs to 
[23] "class"           - the name of the class the occurrence belongs to 
[24] "order"           - the name of the order the occurrence belongs to 
[25] "family"          - the name of the family the occurrence belongs to 
[26] "genus"           - the name of the genus the occurrence belongs to. 
````

5) Use theÂ points( )Â function to plot each occurrence on the map you made previously (make sure to use the paleolatitude and paleolongitude coordinates). Show your code. If you do not know how to use theÂ points( )Â function, consult the help file or use Google.

````R
> points(x=DataPBDB[,"paleolng"],y=DataPBDB[,"paleolat"])
````

6) Where are most of the Anthozoan occurrences in the Eastern Hemisphere (i.e., what region of the world)? Are Anthozoans primarily marine or freshwater organisms? What can you infer must have existed in this region of the world during this time?

Most of the Anthozoan occurrences in the Eastern Hemisphere are in Europe. Anthozoans are primarily marine organisms. There must have been an epicontinental sea in Europe at this time. 

## Problem Set 3

1) Download a dataset of Perissodactyla occurrences from the PBDB that span the Paleogene. Show your code.

````R
> DataPBDB2<-downloadPBDB(Taxa=c("Perissodactyla"),StartInterval="Paleogene",StopInterval="Paleogene")
````

2) What is the defining attribute of Perissodactyla? What are some prominent examples (e.g., lions, tigers, bears, oh my!)? [Hint: Neither lions, nor tigers, nor bears are members of Perissodactyla.] 

Perissodactyla have are undulates with an odd number of toes. Some examples are zebras, rhinoceros, and tapirs.

3) Find collection number 112723 in the dataset you just downloaded in Question 1. Show your code.

````R
> YAY<-subset(DataPBDB2,DataPBDB2[,"collection_no"]==112723)
````

4) What "geoplate" id (tectonic plate) is associated with this collection? What modern day region of the world does this geoplate id correspond to? The remaining questions will refer to this geoplate/region as region-X.

The "geoplate" id is 501. 

````R
plot(PEMap,col=rgb(0,1,1,0.33),lty=0.01)
>points(x=YAY2[,"paleolng"],YAY2=DataPBDB[,"paleolat"])
````

*YAY2 is defined in the question below*
The geoplate corresponds to modern day India.

5) Subset your dataset of Perissodactyla occurrences to only include occurrences that occur in region-X. How many occurrences are there? Show your code.

84

````R
> YAY2<-subset(DataPBDB2,DataPBDB2[,"geoplate"]==501)
>dim(YAY2)
[1] 84  26
````

6) Using the maps we have created previously, making your own new maps, or using the Paleobiology Database Navigator tool, what is the general history of region-X from the Albian through to the present day

Generally, the Indian pate has broken off from Gondwana, moved northward, and has rotated slightly counter-clockwise. It eventually collided with the Eurasian plate about 55 million years ago. This plate movement can be seen using the code below: 

````R
> CretaceousMap<-downloadPaleogeography(Age=66)
> plot(CretaceousMap,col=rgb(0,0,1,0.33),lty=0)
> Timegoeson<-downloadPaleogeography(Age=45)
> plot(Timegoeson,col=rgb(1,1,0,0.33),lty=0,add=TRUE)
> Timegoesonandon<-downloadPaleogeography(Age=25)
> plot(Timegoesonandon,col=rgb(1,0,1,0.33),lty=0,add=TRUE)
> Timegoesonandonandon<-downloadPaleogeography(Age=10)
> plot(Timegoesonandonandon,col=rgb(0,.9,.7,0.33),lty=0,add=TRUE)
> Now<-downloadPaleogeography(Age=0)
> plot(Now,col=rgb(.4,.4,.8,0.33),lty=0,add=TRUE)
> Then<-downloadPaleogeography(Age=90)
> plot(Then,col=rgb(0,.4,.8,0.33),lty=0,add=TRUE)
````


7) There are also many Paleogene occurrences of Perissodactyla in present day China. Using the maps we have created previously, making your own new maps, or using the Paleobiology Navigator tool, evaluate the plausibility of each of the following scenarios?Â ThoroughlyÂ explain your reasoning and how you tested your ideas.

+ Species of Perissodactyla migrated from region-X to China during the Paleogene?

This seems to be the least likely scenario of the three based on the PBDB navigator tool. This is because there are recorded occurrences from the Thanetian stage in what is now Western North America, Europe, and Eastern Asia. Before this, there appear to be occurrences of Perissodactyla from the Danian and Selandian stages only in North America. During this time, what is now Greenland appeared to act as a bridge, connecting North America and Asia. There are no recorded occurrences of Perissodactyla on the Indian plate predating the Ypresian Stage. It therefore seems unlikely that the Perissodactyla migrated from the Indian plate to China during the Paleogene. For this scenario to be correct, it would require that there were Perissodactyla on the Indian plate before they were in Asia (before the Thanetian stage), but none of the fossils of this age of been recovered. This must be true if the species migrated from the Indian plate to China. However, given that the Indian plate has been disconnected from all other plates and isolated by ocean since the Cenomanian stage, this seem extremely unlikely. 

+ Species of Perissodactyla migrated from China to region-X during the Paleogene?

This is more plausible than the previous scenario. As stated above, there are earlier recorded occurrences of Perissodactyla in Asia than on the Indian plate. Based on the occurrence data described above, it seems more likely that Perissodactyla migrated from North America, to Europe between the Selandian and the Thanetian stages. Then it seems that Perissodactyla could have migrated from Europe to Asia to the Indian plate between the Tanetian and the Ypresian stages. This scenario is problematic because based on the Paleobiology navigator map of the tectonic plate locations during these time periods, there is no land bridge shown connecting the Indian plate to any other landmass during these stages. This means that this scenario would require that the estimated locations of the geoplates during these time periods may have been miscalculated. During the Ypresian stage, it appears that India was very close to being connected Asia by the north eastern part of its plate. Then, it is not impossible that it actually was connected to Asia by land at this time. It therefore may be possible that this scenario is correct. 

+ The species of Perissodactyla in China and region-X are unrelated and probably both came from a third region?

This scenario is the most plausible of the three. This is because this scenario does not require that there is any error in plate location estimates, and it does not seem to conflict with the age and location of occurrences of Perissodactyla. I think it is more likely that an ancestor of Perissodactyla evolved and was able to disperse during a time when all of the plates were more or less connected. This would explain why the first recorded occurrences of Perissodactyla on the Indian plate are from the Ypresian stage, when it appears isolated from all other landmasses by ocean water.


