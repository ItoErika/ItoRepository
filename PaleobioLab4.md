Erika Ito
2/22/16

> 19.5/20

## Paleobiology Lab Exercise 4

## Problem Set I
1) How many unique genera are in the Miocene,Early Jurasic, LateCretaceous, and Pennsylvanian epochs (not total, each)? What code         did you use to find out?

602, 169, 375, 133

```R
> apply(PresencePBDB,1,sum) 

2.  How many geologic epochs in general are in this dataset? What code did you use to find out?
29
code:
> length(PresencePBDB[,1])
29 
````

3) Which epochs contain specimens of the genus Mytilus? What code did you find out.

Pridoli, Early Devonian, Cisuralian, Late Jurassic, Eocene, Late Cretaceous, Early Cretaceous, Middle Jurassic, Paleocene, Oligocene, Miocene, Early Jurassic, Pleistocene, Middle Triassic, Late Triassic, Pliocene, Early Triassic

````R
> which(PresencePBDB[,"Mytilus"]==1)
````

4) Look at the epochs in the geologic timescale. Using your answer to question 3, in which epochs can we infer that Mytilus was present, even though we have no record of them in the Paleobiology Database? How did you deduce this?

Mytilus must have at least been present from the earliest epoch from above (Pridoli) to the latest (Pleistocene). Even if we do not have record of them existing at the time intervals in between, we know Mytilus was present because or else it would not have shown up at the latest epoch (Pleistocene)
        
## Problem Set II

The Jaccard index is the simplest Similarity index. It is the intersection of two samples divided by the union of two samples. In other words, the number of genera shared between two samples, divided by the total number of (unique) genera in both samples. Or put even another way, it is the percentage of genera shared between two samples.

1) Using your own custom R code, find the Jaccard similarity of the Pleistocene and Miocene "samples" in your PresencePBDB matrix. It is possible to code this entirely using only functions discussed in the R Tutorial. The key is to use apply( ), sum( ), table( ), and judicious use of matrix subscriptng.

````R
>Vector1<-PresencePBDB["Miocene",]
>Vector2<-PresencePBDB["Pleistocene",]
>ResultantVector<-Vector1+Vector2
>length(ResultantVector[which(ResultantVector==2)])
[1] 509
> table(ResultantVector)
>ResultantVector
0       1     2         
287 106 510
> 510/(106+510)
[1] 0.8279221
````

2) How can you convert your similarity index into a distance?
> 1-0.8279221
[1] 0.1720779

3) Install and load the vegan package into R. Read the help file for the vegdist function - ?vegdist or help(vegdist). You must have already loaded the vegan package in order for it to run.

Again, calculate the jaccard distance of the "Miocene" and "Pleistocene" samples of PresencePBDB, but this time use the vegdist( ) function. This should be an identical answer to what you got in question 2.

````R
> install.packages("vegan")
> library("vegan")
>vegdist(PresencePBDB,method=”jaccard”,binary=FALSE,diag=FALSE,upper=FALSE,na.rm=FALSE)
````
Data for Pleistocene row and Miocene column
Jaccard distance for Miocene and Pleistocene samples is 0.17207792 (same as answer for number 2).


4) Using the vegdist( ) function. Calculate the Jaccard distances of all the following epochs in PresencePBDB - the "Pleistocene", "Pliocene", "Miocene", "Oligocene", "Eocene", "Paleocene". What code did you use? Which two epochs are the most dissimilar?

```R
> class(PresencePBDB)
[1] "matrix"

> PleistoceneVector<-PresencePBDB["Pleistocene",]
> PlioceneVector<-PresencePBDB["Pliocene",]
> MioceneVector<-PresencePBDB[ "Miocene",]
> OligoceneVector<-PresencePBDB["Oligocene",]
> EoceneVector<-PresencePBDB["Eocene",]
> PaleoceneVector<-PresencePBDB["Paleocene",]
>PBDBMatrix<-rbind(PleistoceneVector,PlioceneVector,MioceneVector,OligoceneVector,EoceneVector,PaleoceneVector)
````

> Sure that works, but it would be much easier to do this
````R
PBDBMatrix<-PresencePBDB[c("Pleistocene","Pliocene","Miocene","Oligocene","Eocene","Paleocene"),]
````

````R
>vegdist(PBDBMatrix,method="jaccard",binary=FALSE,diag=FALSE,upper=FALSE,na.rm=FALSE)
                   PleistoceneVector PlioceneVector MioceneVector OligoceneVector
PlioceneVector         0.12692967                                             
MioceneVector          0.17207792     0.08496732                              
OligoceneVector        0.26910299     0.18968386    0.16065574                
EoceneVector           0.21870048     0.13397129    0.08585056      0.19063005
PaleoceneVector        0.44444444     0.37914692    0.33333333      0.41042345
                          EoceneVector
PlioceneVector              
MioceneVector               
OligoceneVector             
EoceneVector                
PaleoceneVector   0.33385827
````

Jaccard distance for each of the epoch pairs are shown above. The Paleocene and Pleistocene epochs are the most dissimilar because they have the highest Jaccard distance (0.44444444).

## Problem Set III

1) Create a subset of the PresencePBDB matrix which contains just the following rows - "Pliocene", "Oligocene", "Paleocene", "Early Cretaceous", "Late Jurassic", and "Middle Jurassic". Name this subset RandomEpochs. Show your code.

````R
> RandomEpochs<-rbind(PresencePBDB["Pliocene,"],PresencePBDB["Oligocene",],PresencePBDB["Paleocene",],PresencePBDB["Early Cretaceous",],PresencePBDB["Late Jurassic",],PresencePBDB["Middle Jurassic",])
````

> See my answer to Question 4 above to see an easier way to do this.

2) Using vegdist( ) find the dissimilarities of all the epochs in Random Epochs. Show your code.

````R
>vegdist(RandomEpochs,method="jaccard",binary=FALSE,diag=FALSE,upper=FALSE,na.rm=FALSE)
     1          2        3         4        5
2 0.1896839                                        
3 0.3791469 0.4104235                              
4 0.7462908 0.7480315 0.6400742                    
5 0.8652695 0.8653846 0.7902622 0.4703947          
6 0.8852459 0.8814103 0.7931689 0.4883721 0.2962963
````

1 corresponds with Pliocene. 2 corresponds with Oligocene. 3 corresponds with Paleocene. 4 Corresponds with Early Cretaceous. 5 corresponds with Late Jurassic. 6 corresponds with Middle Jurassic. 


3) Find the two epochs that are the most dissimilar and make them the poles. Now, using the dissimilarities, order (ordinate) the remaining epochs based on their similarity to the poles. State the order of your inferred gradient.

````R
>VEGA<-vegdist(RandomEpochs,method="jaccard",binary=FALSE,diag=FALSE,upper=FALSE,na.rm=FALSE)
> max(VEGA)
[1] 0.8852459
````

> What does VEGA mean, btw?

The two most dissimilar epochs are the Middle Jurassic and the Pliocene with a Jaccard distance of 0.8852459.

Ordination: 
1, 2, 3, 4, 5, 6 based on R table above (Pliocene, Oligocene, Paleocene, Early Cretaceous, Late Jurassic, and Middle Jurassic). We can tell this because the higher the Jaccard number, the more dissimilar, the lower the Jaccard number, the more similar. 

4) Can you deduce what "variable" is controlling this gradient (e.g., temperature, water depth, geographic distance)? [Hint: Check the geologic timescale]. State your reasoning.

It seems that all of these variables could have come into play, during the time interval between the Middle Jurassic and the Pliocene, the Earth experienced a number of changes. These changes included climate change (transition into Icehouse Earth during the Miocene for example). Fluctuations in climate cause expansions or contractions of ice sheets in the poles. Therefore, the time interval captured in the inferred gradient experienced a number of transgressions and regressions. This time interval captures the Zuni sequence which began in the Jurassic and peaked in the Cretaceous, when epicontinental seaways covered much of the United States (Western Interior Seaway). This transgression was caused by the hothouse Cretaceous climate that developed as a result of a superplume event. The Zuni sequence ended by the Paleocene, when sea level regressed again. This information implies that these variables mentioned above actually go hand in hand. The temperature/climate changes would have caused sea level fluctuations. The rise and subsequent drop in sea level could have consequently separated species, creating geographic distance, controlling the gradient as well. I would therefore postulate that all of the variables listed controlled the gradient, but perhaps climate would be the main driving force, having a cascading impact on other variables. The water depth changes most likely have the greatest impact on the gradient we see though, since we are looking at marine organisms, which most often have preferential depths at which they can thrive. 

> Okay, a thorough answer, but not really in the spirit of gradient analysis. We are trying to think of a single continuum that runs from low to high (or high to low) that can explain the separation of samples. The most obvious is time, since the samples are in temporal order in the gradient - i.e., run from oldest to youngest. You do make a good point that temperature, which generally declines over this period could be another gradient. You also mention that the variables "go hand in hand", what did we learn about "complex" or "indirect" gradients in lecture? - 0.5 Points

5). There is a relatively high dissimilarity between the Early Cretaceous and Paleocene epochs. Can you hypothesize why this is? Google these epochs if you need to.

There was a mass extinction event at the boundary between the Cretaceous and the Paleocene (K-Pg boundary) caused by an asteroid impact ~65 Ma ago. It is therefore unsurprising that the Early Cretaceous and the Paleocene epochs show higher dissimilarity, because the extinction event likely drove evolutionary/taxonomic turnover. As stated before, the early Paleocene also marks the end of the Zuni sequence, such drastic sea level changes may also be at play in sparking taxonomic turnover. 

## Problem Set IV

1) Download a dataset from the paleobioogy database of all Ordovician aged animals (i.e., animalia) into R, and name the object Ordovician. This may take a few minutes. What R code did you use?

````R
>Ordovician<-downloadPBDB(Taxa=c("Animalia"),StartInterval="Ordovician",StopInterval="Ordovician")
````

2) Clean up the poorly resolved genus names. What function/code did you use?

````R
>DataOrdovician<-cleanGenus(Ordovician)
````

3) Turn your object Ordovician into a community matrix of samples by genera, where the samples are different geoplatecodes. Geoplate codes denote different ancient paleocontinents - i.e., your community matrix will list which genera were present in which ancient paleocontinent. Cull this matrix so that each sample has a minimum of 25 taxa and each taxon occurs in at least two samples. Show your code.

````R
>OrdoMatrix<-presenceMatrix(DataOrdovician,SampleDefinition="geoplate")
> OrdoMatrix<-cullMatrix(PresencePBDB,minOccurrences=2,minDiversity=25)
````

4) Perform a DCA on your new community matrix. Analyze your new DCA with a plot. Do you think that the orientation of samples along either axis 1 or axis 2 is related to the average latitude or longitude of each plate in question? Explain how you figured this out. Show your code. [Hint: Information about the paleolatitude and paleolongitude of different geoplates is included in your originally downloaded data - i.e., the object Ordovician.]

It appears that the orientation of the samples along axis 1 (horizontal axis) is related to the average latitude for each plate. The plates that are in close horizontal proximity on the DCA plot have average paleolatitudinal values that are fairly similar (most within 10-20 degrees latitude). Geoplates 801, 402, and 401 are a good example of this. They are all relatively close in horizontal proximity on the plot, and are all within about 20 degrees paleolatitude from one another. There may be a weaker relationship between paleolongitude and the orientation on axis 2 (vertical axis), but it is less consistent with the data. Some geoplates in close proximity along the orientation of axis 2 (vertical) have similar longitudinal values and others have dramatically different values, so the relationship here is unclear. 

````R
>OrdovicianDCA<-decorana(OrdoMatrix)
> plot(OrdovicianDCA,display="sites")
> tapply(Ordovician[,"paleolat"],Ordovician[,"geoplate"],mean)
> tapply(Ordovician[,"paleolng"],Ordovician[,"geoplate"],mean)
````

> Interesting, most people did not see a strong latitudinal signal in the data (myself included), but I am pleased by your answer nonetheless.
