---

author      : Aishwarya Venkat
job         : Eco Health Net Intern
framework   : deckjs        # {io2012, html5slides, shower, dzslides, ...}
deckjs      : {theme: swiss, transition: fade}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : hemisu-light      # 
widgets     : mathjax            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
assets      : {assets: ../../assets}

---

<center><img src="assets/img/banner.png" width="1500"></center>
<br></br>
<br></br>

# African Sustainable Livestock 2050

### Aishwarya Venkat
### EcoHealth Net Research Exchange Intern, Summer 2017

<img src="assets/img/EHA_logo_wide.jpg" height="150" align="left">

---

## About Me

<center><img src="assets/img/abtme1.png" width="1000"></center>

---

## About Me

<center><img src="assets/img/abtme2.png" width="1000"></center>

---

## African Sustainable Livestock (ASL) 2050

* FAO project funded by USAID
* Goals: 
  - identify opportunities and threats associated with the long-term development of livestock
  - agree upon priority reforms and investments, and the capacity needed for their implementation, to ensure sustainable development of the livestock sector in the next three or four decades.
* Countries:  Burkina Faso, Egypt, Ethiopia, Kenya, Nigeria and Uganda

---

## EHA & ASL 2050

- Metaflu ([Hosseini et al, 2013](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0080091)) package to simulate propagation and impacts of seeded avian influenza outbreaks
  - Kate: variable farm sizes, growth, culling
  - John: presence/absence of markets, effect on households and farms
  - Me: spatial data collection, developing pipeline for 'real world' data input into Metaflu 

<center><img src="assets/img/metaflu.jpg" height="600"></center>

---

## Key Actors

Households
 * Key exposure points for humans
 * 60-85% of livestock sector in ASL countries is driven by household/backyard poultry farming
 * Easy targets for interventions and incentives

Commercial Farms
 * Operations of scale, most impacted by avian influenza outbreaks
 * Most ASL2050 countries aim to expand commercial poultry operations in next decade-incentive for improved biosecurity

Markets
 * Daily, weekly markets frequented by majority of people
 * Locations of high chicken movement between actors

---&twocolfull

## Knowns & Unknowns

*** =left

### Unknowns

* Locations of farms & households
* Flock size at farms & households
* Flock size at markets
<br></br>
<center><img src="assets/img/locationquestion.png" width="300"></center>

*** =right

### Knowns

* Representative areas <br>
  <i>Source: livestock surveys</i>
* Household weights <br>
  <i>Source: livestock surveys</i>
* Commercial farm size information <br>
  <i>Source: literature</i>
* Network of farms and households contributing to markets

---

## Small World Networks

<center><img src="assets/img/WS_SmallWorld.gif" width="1000"></center>

<br>
Watts, Duncan J., and Steven H. Strogatz. [Collective dynamics of 'small-world' networks](https://www.nature.com/nature/journal/v393/n6684/full/393440a0.html), Nature 393.6684 (1998): 440

--- 

## Goals & Methods

> 1. Ground Metaflu simulations in reality 
  - Country-wide poultry sector information collection
  - Spatial data processing 
      - Probability surface development and spatial sampling for households and farms
      - Assignment of 'farm size' based on extensive/intensive production rasters
> 2. Apply Small World Network principles to Random Spatial Networks
  - Generate network representations of spatial data
    - Define how each actor is connected to the others
    - Parametrize network to allow for testing of intensification and connectivity
> 3. Identify limitations of existing data, and generate models and questions to share with FAO theme leaders


---

## Livestock Survey Data

* Primary data source: Country-level Livestock Survey data aggregated by FAO


```
##    HHID    EAID Latitude Longitude Household.Weight Chickens
## 1 87095 1912049    9.324    38.592             3971        8
## 2 86375 1270896   10.394    38.225             4752        2
## 3 84926 1391416   15.392    39.212             3230        4
```

* Surveys provide approximate location information

* Representative households are actually spread out across survey enumeration areas

--- 

## Approach: Households

> * Household/Backyard chicken production density from [Marius et al, 2015](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0133381#sec002)

<center><img src="assets/img/ext_rast.png" width="600"></center>

> * Use this as probability surface to distribute households within country

---

## Approach: Commercial Farms

>   * Get number and sizes of commercial farms from literature, poultry sector reports (Ethiopia, Kenya, Uganda), or scraped from [OIE](http://www.oie.int/wahis_2/public/wahid.php/Wahidhome/Home) & [FAO EMPRES-I](http://empres-i.fao.org/eipws3g/) outbreak data

>   * Fit lognormal model to farm size, sample randomly from distribution until value adds up to total estimated intensive chicken population

<center><img src="assets/img/lognorm.jpg"></center>

---

## Aproach: Commercial Farms

>   * Distribute points based on intensive poultry production raster

<center><img src="assets/img/int_rast.png" width="600"></center>

---

## Approach: Markets

>   * Ethiopia, Uganda, Kenya: [Intergovernmental Authority on Development (IGAD)](www.igad.int) 

>   * Burkina Faso, Egypt, Nigeria: Populated Places data from [OpenStreetMap](http://download.geofabrik.de/africa/) and [SEDAC GRUMP](http://sedac.ciesin.columbia.edu/data/set/grump-v1-settlement-points-rev01/)

<center><img src="assets/img/ETH_markets.png" width="600"></center>

--- 

## Combining Data

<br>

<center><img src="assets/img/ETH_points.png" width="1000"></center>

---

## Parametrize connectivity

<br>

<center><img src="assets/img/ETH_m1.png" width="1000"></center>

<center>Each household is connected to nearest market</center>

---

## Parametrize connectivity

<br>

<center><img src="assets/img/ETH_mf1.png" width="1000"></center>

<center>Each farm is connected to multiple markets</center>

---

## Parametrize connectivity: households

<br>

<center><img src="assets/img/ETH_mfh_k2.png" width="1000"></center>

<center>Each household is connected to two other households</center>

---

## Parametrize connectivity: households

<br>

<center><img src="assets/img/ETH_mfh_k4.png" width="1000"></center>

<center>Each household is connected to four other households</center>

---

## Connecting poultry sector actors

<br>
$$p_{u,v} = min\Bigg(\kappa_u\kappa_v\frac{f(d_{uv})}{\rho\langle\kappa\rangle},1\Bigg)$$

$u,v = $ two nodes (any of households, markets, farms)
<br>
$ p = $ probability of connection between nodes $u$ and $v$
<br>
$f(d_{uv}) = $ exponential decay kernel connecting nodes, defined by a distance (rate) at which 50% of nodes in country are connected
<br>
$\kappa = $ expected degree of connections per node (Poisson distributed across nodes)
<br>
$\langle\kappa\rangle = $ average degree of connections for all nodes
<br>
$\rho = $ density of nodes within country
<br>
<br>

Lang, John, et al. [Random Spatial Networks: Small Worlds without Clustering, Traveling Waves, and Hop-and-Spread Disease Dynamics](https://arxiv.org/pdf/1702.01252.pdf). arXiv:1702.01252 (2017).

---

## Progress

* Identified data sources for all six countries, validation and review in progress 
* Pipeline for analysis and input into Metaflu defined
* Experiments to test kappas and distances (rates) for reproducibility across countries

## Next Steps

* Network generation for all ASL countries
* Break down network into modules for metaflu simulations 
* Develop risk maps and outbreak probability analyses
* Writing and publication of results 

---

## Skills learned

* GIT!
* Parallel processing 
* Network analysis in igraph
* Sparse matrices
* Geographically weighted principal components analysis (PCA)
* Raster stack manipulation and raster PCA
* Random forest models and boosted regression trees

---&twocolfull

## Acknowledgements   

*** =left

* Noam Ross

* Cale Basaraba

* Allison White 

* Carlos Zambrana-Torrelio

* Modeling & Analytics team

<center><img src="assets/img/EHA_logo_wide.jpg" height="200"></center>

*** =right

* Orsolya Mikecz

* Antonio Mele

* Ugo Pica-Ciamarra

<br><br><br><br>
<center><img src="assets/img/faologo.jpg" height="150"></center>
