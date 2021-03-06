Erika Ito
Lab Exercise 5

> 18/20

## Problem Set 1
You may not use vegan( ) for this subsection.

1) What is Bivalve generic richness in the Miocene? What code did you use to find
out?

````R
> table(BivalveAbundance["Miocene",] )
> sum(table(BivalveAbundance["Miocene",]))
[1] 2273
> 2273-1639
[1] 634
````

2) What is the Berger-Parker Index of Brachiopods genera in the Pliocene? What code did you use to find out? [Hint: the function max( ) may help you).
(abundance of most common species / totalabundance all species)

````R
> max(BrachiopodAbundance["Pliocene",])
[1] 22
> table(BrachiopodAbundance["Pliocene",])
   0    1    2    3    4    6    9   11   12   22 
3084   10    3    2    2    1    2    1    1    1 
> sum(BrachiopodAbundance["Pliocene",]
[1] 99
OR
> 1*10+2*3+3*2+4*2+6*1+9*2+11*1+12*1+22*1
 [1] 99
> 22/99
[1] 0.2222222
````

3) What is the Gini-Simpson Index of Brachiopods during the Late Ordovician? What code did you use to find out?
````R
1-sum(n/N)^2 
N=total number of species 
n=abundance each species
> N<-sum(BrachiopodAbundance["Late Ordovician",])
>N
[1] 6154
> n<-BrachiopodAbundance["Late Ordovician",]
> sum((n/N)^2)
[1] 0.02154119
> 1-0.02144119
[1] 0.9785588
````

4) What is the Shannon's Entropy of Bivalves during the Late Cretaceous? What code did you use to find out?
SUM(n/N)ln(n/N)
N= sum total abundance all species
n=abundance each species

````R
> N<-sum(BivalveAbundance["Late Cretaceous",])
>N
[1] 29684
> n<-BivalveAbundance["Late Cretaceous",]
*now get rid of all the zeroes in n...
> thing<-(BivalveAbundance["Late Cretaceous",]!=0)
> n<-BivalveAbundance["Late Cretaceous",thing]
OR5>n<-BivalveAbundance[“Late Cretaceous”,BivalveAbundance[“Late Cretaceous”,]>0]
> -sum((n/N)*log(n/N))
[1] 5.086654
````

5) What is the Shannon's Entropy of Bivalves during the Paleocene? What code did you use to find out?
````R
> N<-sum(BivalveAbundance["Paleocene",])
> N
[1] 4238
> n<-BivalveAbundance["Paleocene", BivalveAbundance["Paleocene",]>0]
> -sum((n/N)*log(n/N))
[1] 4.511875
````

6) What is the percent change in Shannon's Entropy between the Late Cretaceous and the Paleocene? Can you think of any major events that happened between the Late Cretaceous and Paleocene that might be relevant to biodiversity? [Hint: Use google if you don't know.] Is this reflected in this index?

````R
>(5.086654-4.511875)/5.086654
[1] 0.1129975
So it is an 11.3% change. 
K/Pg boundary asteroid impact caused mass extinction. Yes, it is reflected in the large percent change.
````

7) What if you use the exp( ) function to exponentiate the Shannon's Entropies you calculated in questions 4,5, and 6 (i.e.,e^Shannon's Entropy)? What percent of diversity is gained/lost? Does this better reflect the change between the Late Cretaceous and Paleocene? Why or why not?

````R
> exp(4.511875)/exp(5.086654)
[1] 0.5628292
````
56.3%  loss in diversity.

> Nope! The Paleocene is 56.3% as diverse as the Late Cretaceous... so how much was LOST? -1 Points

## Problem Set 2
Install (if you have not already) and load the vegan package into R. Read the help file for the diversity( ) function - ?diversity or help(diversity). You must have already loaded the vegan package in order for it to run.
1) Use the specnumber( ) function (also from the vegan package) to find Bivalve richness in the Miocene. What code did you use to find out?

````R
634
> specnumber(BivalveAbundance ["Miocene",])
[1] 634
````

2) Use the diversity( ) function to find the Gini-Simpson Index of Brachiopods during the Late Ordovician? What code did you use to find out?

````R
0.9784588
> diversity(BrachiopodAbundance, index="simpson", MARGIN=1, base=exp(1))["Late Ordovician"]
````

3) Use the diversity( ) function to find the Shannon's Entropy of Bivalves during the Late Cretaceous? What code did you use to find out?

````R
5.086654 
> diversity(BivalveAbundance,index="shannon",MARGIN=1,base=exp(1))["Late Cretaceous"]
Late Cretaceous 
       5.086654 
````

4) Use the diversity( ) function to find the Shannon's Entropy of Bivalves during the Paleocene? What code did you use to find out?

````R
4.511875 
> diversity(BivalveAbundance,index="shannon",MARGIN=1,base=exp(1))["Paleocene"]
Paleocene 
 4.511875 
````

## Problem Set 3
1) Is brachiopod richness positively, negatively, or un-correlated with bivalve richness? Show your code?
negatively correlated

````R
> BivRichness<-specnumber(BivalveAbundance)
> is(BivRichness,"vector")

In order of geologic time (oldest->youngest): early ordo, mid ordo, late ordo, landdovery, wenlock, ludlow, pridoli, early dev, mid dev, late dev, miss, penn, cisuralian, guadalupian, lopingian, early tri, mid tri, late tri, early jur, late mid jur, late jur, early cret., late cret., paleocene,eocene,oligocene,miocene,pliocene,pleistocene

To order in geologic time (oldest-> youngest)
>BivRichnessVector<-c(42,48,87,56,66,81,51,111,88,70,99,104,160,191,156,151,101,242,217,202,270 ,393,574,305,512,355,634,534,498)

make sure nothing was skipped:
> sum(BivRichnessVector)
[1] 6398
> sum(BivRichness)
[1] 6398
> length(BivRichness)
[1] 29
> length(BrachRichness)
[1] 29

now for brachiopod richness
> BrachRichness<-specnumber(BrachiopodAbundance)
> BrachRichness
To order in geologic time (oldest -> youngest)
> BrachRichnessVector<-c(141,282,331,271,257,234,138,497,353,274,314,284,564,549,406,63,
111,193,130,175,111,125,96,29,57,30,45,23,19)

check:
>sum(BrachRichness)
[1] 6102
> sum(BrachRichnessVector)
[1] 6102

> cor(BrachRichnessVector,BivRichnessVector)
[1] -0.5702269
````

2) Is brachiopod biodiversity positively, negatively, or un-correlated with bivalve biodiversity when using the Gini-Simpson index? Show your code?
negatively correlated

````R
> BrachDiv<-diversity(BrachiopodAbundance,index="simpson",MARGIN=1,base=exp(1))
> BrachDiv

Order in Geologic Time:
> BrachDivVector<-c( 0.9754801,0.9864630, 0.9784588, 0.9818355,0.9834619,  0.9848907,0.9808705, 0.9903477,0.9814661, 0.9773679 ,0.9831947, 0.9692427, 0.9916219,0.9916507,0.9840791,0.9165190,0.9615971,0.9674429, 0.9582676,0.9692636, 0.9711110, 0.9756485, 0.9444381,0.8641030,0.9406975,0.9441899 ,0.9425318,0.8960310, 0.8999748)


check:
> sum(BrachDiv)
[1] 27.89225
> sum(BrachDivVector)
[1] 27.89225


now bivalve diversity:
> BivDiv<-diversity(BivalveAbundance,index="simpson",MARGIN=1,base=exp(1))
>BivDiv


Order in Geologic Time:
> BivDivVector<-c(0.9540843, 0.9365728 ,0.9488055,0.9221477 ,0.9575669,0.9504394,0.9449848,0.9705751,0.9446541 ,0.9203195,0.9651885,0.9636918,0.9774096,0.9824063,0.9763584, 0.8961555, 0.9727084, 0.9808775, 0.9762395,0.9819201,0.9836451,0.9846595,0.9869740,0.9766257 ,0.9851310,0.9882072 ,0.9914026 ,0.9911654 ,0.9913115)


check:
> sum(BivDiv)
[1] 28.00223
> sum(BivDivVector)
[1] 28.00223


> cor(BivDivVector,BrachDivVector)
[1] -0.2355646
````

3) Looking just at changes in brachiopod richness through time, when did the greatest drop in brachiopod richness occur (i.e., between what two consecutive epochs)?

````R
>BrachRichness
   Mississippian     Pennsylvanian  Early Ordovician Middle Ordovician   Late Ordovician        
  314                   284                  141            282                331 
Llandovery    Wenlock    Ludlow    Pridoli     Early Devonian     Middle Devonian     Late Devonian
   271         257           234       138        497                353              274
Cisuralian             Late Jurassic    Eocene           Late Cretaceous    Early Cretaceous
 564                     111              57                 96                    125 
Middle Jurassic    Paleocene         Lopingian              Early Jurassic       Guadalupian
   175                 29              406                   130                      549
Middle Triassic     Late Triassic     Miocene                 Early Triassic        Pliocene
111                      193            45                         63                 23
Pleistocene          Oligocene
 19                    30

In order of geologic time (oldest->youngest): early ordo, mid ordo, late ordo, landdovery, wenlock, ludlow, pridoli, early dev, mid dev, late dev, miss, penn, cisuralian, guadalupian, lopingian, early tri, mid tri, late tri, early jur, late mid jur, late jur, early cret., late cret., paleocene,eocene,oligocene,miocene,pliocene,pleistocene

Vector in order
> BrachRichnessVector
 [1] 141 282 331 271 257 234 138 497 353 274 314 284 564 549 406  63 111 193 130 175 111 125  96  29  57  30  45  23  19

The largest drop in richness occurs between the Lopingian and the Early Triassic.
A drop from a brachiopod richness of 406 to a brachiopod richness of 63 (343 drop) occurred at this boundary.
```

## Problem Set 4
````R
1) Repeat the above steps, but for the BrachiopodAbundance community matrix. What is the standardized richness you got for brachiopods. Show your code.
> SampleBrachAbundances<-apply(BrachiopodAbundance,1,sum)
> SampleBrachAbundances[which(SampleBrachAbundances==min(SampleBrachAbundances))]
Pleistocene 
         63 
> StandardizedBrachRichness<-apply(BrachiopodAbundance,1,subsampleIndividuals,Quota=63)
> StandardizedBrachRichness[1:6]
   Mississippian     Pennsylvanian  Early Ordovician Middle Ordovician   Late Ordovician        
            43.21             34.64                     38.31                   46.11                     42.52
Llandovery 
          42.41
````


2) How does the standardized brachiopod richness (previous question) compare to the unstandardized brachiopod richness from Problem Set 3? Show your code. Explain your reasoning. [Hint: Don't forget to put your biodiversities in temporal order]
They are very strongly, positive correlated as proven by the coding below. This means they are very similar vectors, so as one increases (or decreases) the other increases (or decreases) in a similar manner through time since the vector data was arranged in proper temporal order.


````R
> StandardizedBrachRichness


Put in temporal Order:
> StandardizedBrachRichVector<-c(38.31,46.11,42.52,42.41 ,43.53 ,44.09 ,40.83,50.34 ,41.54 ,39.30 ,43.21 ,34.64 ,50.76 ,51.30 , 43.58,23.76 ,33.50,36.88,31.01,36.72,34.55,36.90,28.73,16.59,27.14 ,25.54,24.67,18.78 ,19.00 )


check:
> sum(StandardizedBrachRichVector)
[1] 1046.24
> sum(StandardizedBrachRichness)
[1] 1046.24


Compare with BrachRichness Vector from Problem Set 3:
> cor(StandardizedBrachRichVector,BrachRichnessVector)
[1] 0.8834675
````

3) Make a scatter plot of standardized brachiopod richness versus standardized bivalve richness. Make a second scatter plot of unstandardized brachiopod richness versus unstandardized bivalve richness. Compare and contrast the two plots. What are the differences or similarities? Does standardizing or not standardizing matter? Show your code and explain your reasoning in detail. [Hint: If you forgot how to plot, revist the previous lab]

````R
# Standardize Bivalve Richness:
> SampleAbundances<-apply(BivalveAbundance,1,sum)
> SampleAbundances[which(SampleAbundances==min(SampleAbundances))]
Early Ordovician 
             124 
> StandardizedBivalveRichness<-apply(BivalveAbundance,1,subsampleIndividuals,Quota=124)
> SampleAbundances<-apply(BivalveAbundance,1,sum)
> StandardizedBivalveRichness


# put in temporal order:
> StandardizedBivRichVector<-c(42.00,36.79,42.25,37.37,45.72 ,42.69,34.53,51.29 ,35.48 ,33.03 ,47.10,43.47 ,58.10 ,62.99,53.64,28.00,54.52,63.93 ,58.12,61.38,65.35,74.06 ,78.35,62.53 ,72.79,76.47,85.93,84.97,83.84 )
check:
> sum(StandardizedBivRichVector)
[1] 1616.69
> sum(StandardizedBivalveRichness)
[1] 1616.69


# StandardizedBivRichVector = bivalve richness = x-axis
# StandardizedBrachRichVector = brachiopod richness = y-axis
> plot(x=StandardizedBivRichVector,y=StandardizedBrachRichVector)

# From Problem Set 3, plot:
> plot(x=BivRichnessVector,y=BrachRichnessVector)
````  

Both the standardized and unstandardized plots show a general trend of bivalve richness increasing as brachiopod richness decreases. This trend was slightly more clear and consistent using the standardized data. Therefore, it seems to be useful to use standardized data over unstandardized data.


4) Do you believe that there is any evidence in these analyses to support the idea that bivalves outcompeted brachiopods over time? Explain your reasoning.

Yes. In problem set 3 I determined that brachiopod richness has a negative correlation with bivalve richness. SImilarly, I determined that brachiopod diversity has a negative correlation with bivalve diversity. Looking at the brachiopod richness and diversity data from (BrachRichnessVector and BrachDivVector), I can clearly see that brachiopod richness and diversity decrease over geologic time moving toward the present. Conversely, when looking at richness and diversity data for bivalves (BivRichnessVector and BivDivVector) I can see a general increasing trend in both richness and diversity over geologic time moving toward the present. This supports and assists in the interpretation of the negative correlations mentioned. This evidence along with the graph in the previous question, showing bivalve richness increase with decreasing brachiopod richness, are solid indicators that bivalves outcompeted brachiopods over time.

> Hmm... have you ever heard the phrase, "Correlation does not prove causation" used in this context? Just because one is going up as another is going down doesn't mean that one caused the other. -1 Points
