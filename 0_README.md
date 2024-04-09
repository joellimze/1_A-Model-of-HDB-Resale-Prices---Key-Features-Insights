# A Model of HDB Resale Prices: Key Features & Insights


### <b>1. Introduction : Study's Overview & Objectives</b>

<b>(a) Context: The Value of Modelling HDB Resale Prices</b>

* An overwhelming majority (78%) of resident households in Singapore live in HDB apartments (i.e., public housing)

* There is thus keen interest in identifying features strongly associated with HDB resale prices, as well as being able to predict prices, amongst:

  * Home owners / buyers: to assess what an apartment’s fair value might be, identify apartments that fit their budget/needs
  * Policy makers: to identify features residents value, to aid with town planning

<b>(b) HDB Resale Price Modelling Objectives</b>

* This study thus attempts to provide insight on the above, and has two modelling objectives: 

  * <b>Inference</b>: To separably identify features strongly associated with resale prices, by assessing their *statistical* and *practical* significance
  * <b>Prediction</b>: To predict resale prices well, with as narrow a deviation from transacted prices as possible

<br>

---

### <b>2. Data Used for Modelling</b>

* [HDB resale price data from a Kaggle Challenge](https://www.kaggle.com/competitions/dsi-sg-project-2-regression-challenge-hdb-price/data), covering a significant time span, with a large no. of observations 
  * ~ 9 years (2012 – ‘21)
  * ~ 150,000 recorded transactions

* Incorporating data on a wide range of features (>70), covering the following broad feature categories:
  * Apartment’s
    * Physical characteristics (e.g., floor area, floor level)
    * Remaining lease period
    * Housing block characteristics (e.g., flat type composition)

  * Surrounding
    * Transport infrastructure (e.g., MRT stations)
    * Amenities (e.g., malls, hawker centres)
    * Schools

<br>

---

### <b>3. Modelling Approach</b>

* A multivariate linear regression model with a common set of features will be used for the two streams of analysis, with differences as follows:
  * Inference: Unregularised
  * Prediction: Unregularised, Regularised (Ridge/Lasso) (*to select an approach that offers the best predictive performance*)

* A hypothesis-focused approach to feature selection and engineering has been adopted, as interpretation of regression coefficients is of primary interest for inference
  * Contextual knowledge (e.g., news reports, interview with a practicing property agent), and exploratory data analysis have been utilised to derive features

* Features selected / engineered are as follows:

  |Feature Name                       |Feature Description                                |Feature Type|
  |-----------------------------------|---------------------------------------------------|------------|
  |floor_area_sqm                     |Flat's floor area (sqm)                            |Continuous  | 
  |floor_area_sqm_2                   |Flat's floor area (sqm) ^2                         |Continuous  |
  |floor_level_mid                    |Flat's floor level                                 |Continuous  |
  |floor_level_mid_2                  |Flat's floor level ^2                              |Continuous  |
  |flat_type_dbss                     |Exceptional flat type : if DBSS                    |Dummy       |
  |flat_type_terrace                  |Exceptional flat type : if terrace                 |Dummy       |
  |flat_type_maisonette_loft          |Exceptional flat type : if maisonette or loft      |Dummy       | 
  |flat_type_duxton_s1_s2             |Exceptional flat type : if duxton s1/s2 type       |Dummy       | 
  |remaining_lease_years              |Remaining lease years                              |Continuous  |
  |remaining_lease_years_2            |Remaining lease years ^2                           |Continuous  |
  |blk_rental_present                 |Flat's block: rental units present                 |Dummy       | 
  |mrt_nearest_frm000_500             |Nearest MRT station : within 500m                  |Dummy       | 
  |mrt_nearest_abv500_1000            |Nearest MRT station : >500 to 1000m                |Dummy       | 
  |mrt_nearest_interchange_train_bus  |Nearest MRT station : if MRT & bus interchange     |Dummy       | 
  |mrt_nearest_interchange_train_only |Nearest MRT station : if MRT-only interchange      |Dummy       | 
  |mrt_nearest_interchange_bus_only   |Nearest MRT station : if bus-only interchange      |Dummy       | 
  |bus_stop_nearest_frm000_150        |Nearest bus stop : within 150m                     |Dummy       | 
  |mall_nearest_frm000_500            |Nearest mall : within 500m                         |Dummy       | 
  |mall_nearest_abv500_1000           |Nearest mall : >500 to 1000m                       |Dummy       | 
  |hawker_nearest_frm000_500          |Nearest hawker centre : within 500m                |Dummy       | 
  |hawker_nearest_abv500_1000         |Nearest hawker centre : >500 to 1000m              |Dummy       | 
  |hawker_nearest_size_large          |Nearest hawker centre : large sized (>=100 stalls) |Dummy       | 
  |mrt_travel_cost_cbd                |Travel cost to the CBD via the MRT network         |Continuous  |
  |mrt_travel_cost_cbd_2              |Travel cost to the CBD via the MRT network ^2      |Continuous  |
  |n_brand_pri_sch_within_0-1km       |No. of 'branded' primary schools (<=1km)           |Continuous  |
  |n_brand_pri_sch_within_1-2km       |No. of 'branded' primary schools (>1 to 2km)       |Continuous  |
  |n_brand_sec_sch_within_0-1km       |No. of 'branded' secondary schools (<=1km)         |Continuous  |
  |n_brand_sec_sch_within_1-2km       |No. of 'branded' secondary schools (>1 to 2km)     |Continuous  |
  |town_*                             |Town dummies (ref: Ang Mo Kio)                     |Dummy       | 
  |year_*                             |Transaction year dummies (ref: 2012)               |Dummy       | 


<br>

---

### <b>4. Key Insights</b>

<b>(a) Features Most Strongly Associated with Resale Price</b>

* Expectedly and from a practical standpoint, features found to be most strongly associated with resale price are:
  
  |Feature Category / Features                |                                                                                |
  |-------------------------------------------|--------------------------------------------------------------------------------|
  |Apartment Characteristics 	                |*Exceptional Flat Types, Flat’s Floor Area, Flat’s Remaining Lease Years*       |
  |Public Transport Connectivity              |*Proximity to an MRT Station, Nearest MRT Station Being a Public Transport Hub* |
  |Travel Cost to the CBD via the MRT Network |                                                                                |
  |Town-level (Unobserved) Features           |*Bukit Timah, Marine Parade, Bishan, Sembawang, Chua Chu Kang, Jurong West*     |
  
<b>(b) Model's Predictive Ability</b>

* Model predicts resale prices well, with no discernible difference in predictive performance across 'unregularised', 'ridge' and 'lasso' approaches
  * Mean Absolute Error (MAE) of ~$36,000
  * Mean Absolute Percentage Error of ~8.6%

<br>

---

### <b>5. Discussion & Suggestions for Further Research</b>

* Key insights might be utilised in the following ways by different stakeholders, as follows:
  * Home buyers: as a guide for searching for a suitable apartment, assessing what an apartment’s fair value might be
  * Home owners: to aid with forming expectations regarding resale value enhancement / degradation when features change, assessing what an apartment’s fair value might be
  * Policy makers: consider studying if regional economic centre development plans should be enhanced
  
* Suggestions for further research:
  * Consider including other features in the model, as follows, as these could lend further insight on attributes (not) valued by homeowners, and aid with urban planning cost/benefit analyses:
  
    * Proximity to green spaces 		(e.g., parks, nature reserves)
    * Environmental quality 			(e.g., air quality, ambient noise levels)
    * Proximity to industrial estates 	(e.g.,  by industrial type – heavy / light) 
  
<br>

---

### Available Files

* Jupyter Notebooks (*For Replicating Analyses*)
  * '1_EDA', '2_Data Processing', '3_Data Analysis'

* Additional Python Script (*For Performing Travel Cost to the CBD via the MRT Network Computation*)
  * 'Data_Processing_MRT_Tools' 

* Data Files (Raw, Cleaned & Processed Files)
  * In Folder: '1_Data'

* Slide Deck (*Study's Overview & Results*)
  * 'A Model of HDB Resale Prices - Key Features & Insights' 


<br>

---

### Acknowledgements

This study builds upon an earlier General Assembly Data Science Immersive Project performed jointly with Wei Chiong Tan, Matthew Zhou, and Muhd Faaiz Khan, who have all contributed immensely to its current form. All errors and omissions remain my own. 


