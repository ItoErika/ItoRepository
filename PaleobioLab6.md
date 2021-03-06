# Lab Exercise 6

20/20

## Problem Set 1

1) As part of our matching procedure between the Macrostrat database and the Paleobiology database, we lost some data - i.e., there was some Paleobiology Database occurrences that could not be matched to the Macrostrat database. How many occurrences were lost? Show your code.

````R
25153
> dim(DataPBDB)
[1] 34166    26
> dim(MacroPBDB)
[1] 9013   13
> 34166-9013
[1] 25153
````

2) Using what you know about the Macrostrat database can you speculate as to why so much data was lost?
Not all of the occurrences in the DataPBDB dataframe are matched to stratigraphic units in Macrostrat because the coverage is limited to North America.

## Problem Set 2

1) A good candidate for classification as a lagerstätten should have high diversity of different taxnomic orders. Calculate the order-level richness of each stratigraphic formation. Find the top 10 candidate units by this criteria. State them and give the code you used. Also, create a character vector( ) listing the names of these stratigraphic units. Name this vector CandidateUnits.
Hints
1. Remember how to calculate the richness of a sample, and apply this to each sample of the OrderMatrix.
2. If you do not remember how to calculate richness, consult the previous lab.
3. Use the sort( ) function to put your richnesses in order.

````R
> RICH<-specnumber(OrderMatrix)
> sort(RICH)
````

top 10:
Forteau Fm, Parker Slate, Snowy Range Fm, Weymouth Fm, Langston Fm, Wheeler Shale, Marjum Limestone, Stephen Fm, Kinzers Fm, Chancellor

````R
> CandidateUnits<-c("Forteau Fm","Parker Slate","Snowy Range Fm","Weymouth Fm","Langston Fm","Wheeler Shale","Marjum Limestone","Stephen Fm", "Kinzers Fm", "Chancellor")
````

2) A good candidate for classification as a lagerstätten should have a large number of genera that are relatively rare. Using the GenusMatrix column to find out how many samples each genus occurs in. Show the code you used. Name your output GenusFrequencies.

```R
> GenusFrequencies<-colSums(GenusMatrix)
````

3) What is the necessary code to make a frequency barplot of the GenusFrequencies?

````R
> barplot(table(GenusFrequencies))
````

4) After looking at this barplot, you should see a familiar paleobiological pattern. What do we call this type of curved distribution in paleobiology and ecology. [Hint: Think back to the lectures]

Hollow Curve

5) Subset your new vector GenusFrequences so that only those genera from the lower 50% of the distribution are present. In other words genera with occurrences <= to the median( ). Show your code. Name this new subset vector as RareGenera.

````R
> RareGenera<-subset(GenusFrequencies,GenusFrequencies<=median(GenusFrequencies))
````

## Problem Set 3
We will now take the list of rare genera you just made, RareGenera and see what percentage of genera in our top 10 candidate stratigraphic units CandiateUnits come from this list. We will then decide which of our 10 candidate units is the most likely to be a Lagerstätte.
1) Subset GenusMatrix so that it only shows the 10 stratigraphic units we determined were potential candidates. Show your code and name your new matrix, CandidateMatrix.
Load in the following code that I wrote for you. It will find the percentage of genera in each sample (stratigraphic unit) that occur in our vector of RareGenera.

````R
> CandidateMatrix<-subset(GenusMatrix[CandidateUnits,])
> percentRare<-function(CandidateUnit,RareGenera) {CandidateUnit<-CandidateUnit[CandidateUnit>0] PercentIn<-length(which(names(CandidateUnit) %in% names(RareGenera)))
TotalGenera<-length(CandidateUnit) 
PercentShared<-PercentIn/TotalGenera
return(PercentShared)}
````

2) Based on the output of PercentShared and your answer to Problem Set 2 - Question 1 - i.e., the ranking of candidate units based on the number of orders represented, which four units do you think are most likely to qualify as Lagerstätten? Explain your reasoning.

The Marjum Limestone, Forteau Fm, Chancellor, and Weymouth Fm are most likely to qualify as Lagerstätten. This is reasonable because as shown in the codes below, these four units contain the highest number of rare genera. These four units also all appear in the top ten in terms of order-level richness which is also an indicator of Lagerstätten. Therefore, these are the units which most like fit the criteria to qualify as Lagerstätten. 

top 10 from Problem Set 2 Question 1:
Forteau Fm, Parker Slate, Snowy Range Fm, Weymouth Fm, Langston Fm, Wheeler Shale, Marjum Limestone, Stephen Fm, Kinzers Fm, Chancellor

````R
> PercentShared<-apply(CandidateMatrix,1,percentRare,RareGenera)
> PercentShared
      Forteau Fm     Parker Slate   Snowy Range Fm      Weymouth Fm      Langston Fm    Wheeler Shale Marjum Limestone       Stephen Fm       Kinzers Fm 
       0.5652174        0.2812500        0.1951220        0.6764706        0.1632653        0.2307692        0.3559322        0.3055556        0.2586207 
      Chancellor 
       0.5714286 

> YAY<-sort(PercentShared)
> YAY[7:10]
Marjum Limestone       Forteau Fm       Chancellor      Weymouth Fm 
       0.3559322        0.5652174        0.5714286        0.6764706 
````

3) Look closer into the into the four units you chose - using Google and information in the Paleobiology Database. One of these should be a very famous Lagerstätten. Which one? What is famous about it? What is its significance to Paleobiology?

The Chancellor group contains the Burgess Shale Formation. The Burgess Shale is about 505 million years old, dating back to the Middle Cambrian. The Burgess Shale contains a high abundance of diverse soft-bodied fossils. It is particularly important because the Burgess Shale Formation provided the first snapshot of the Cambrian Explosion in the fossil record. This is especially relevant in the field of Paleobiology because the Cambrian Explosion was a critical moment in Earth’s evolutionary history, during which nearly all of the marine invertebrate phyla recognized today appeared. This was a moment of rapid diversification, particularly of shelled organisms. Most major animal groups evolved skeletal hard parts. Before the Cambrian Explosion, most organisms were simple, single-celled organisms. The Burgess Shale greatly enhanced the knowledge of the Cambrian Explosion. The causal mechanism for the triggering of the Cambrian Explosion is still debated.
