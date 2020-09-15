# Modeling Toxic Phosphorus Levels on the Potomac River
[Hack_the_Bay](https://hack-the-bay.devpost.com/?ref_content=default&ref_feature=challenge&ref_medium=portfolio)
#### Cheaspeake Bay Water Quality Hackthon 
**organizded by Booz Allen Hamilton**

### Contributors:

[Clay Carson](clayton.pa.carson@gmail.com) <br>
[Bibor Szabo](szabo.bibor@gmail.com) <br>
[Mike Blow](michaelblow@gmail.com)

## Problem Statement

Harmful algal blooms are on the radar of state agencies and local communities alike. From producing toxins harmful to humans and aquatic animals, through forming a thick mat that prevents sunlight from reaching the lower layers, to depleting the oxygen levels needed by aquatic organisms to survive, the rapid growth of algae signify an alarming level of water pollution. But the process, called eutrophication, starts way before we can see algae bloom on the water surface.<br>
<br>
Eutrophication in modern-day societies is sped up by land-use practices that lead to excessive amounts of nutrients entering the water body and thus causing a growth spurt in first the plant (such as algae), then the animal population. In this process, phosphorus as a key nutrient, plays an important role both in producing and in controlling algae blooms. Phosphates are essential to cell reproduction. This means, that the plant population can only grow to the extent supported by the amount of phosphates in the water, regardless of the availability of other nutrients. While, therefore, a high level of phosphorus stimulates rapid algae growth, controlling the level of phosphorus in the water helps maintain a healthy aquatic ecosystem.
 <br>
<br>
The first step towards controlling the total phosphorus amount in the water body is to monitor when levels are reaching a critical point. Our model predicts total phosphorus as three distinct categories: 1) healthy amount, 2) increased amount that stimulates plant growth, and 3) problematic amount that projects unhealthy algae blooms in the Potomac River.


## Data
The original dataset contained water quality data collected in the entire Chesapeake Bay and Watershed by both the [CBP](https://www.chesapeakebay.net/) and the [CMC](https://www.chesapeakemonitoringcoop.org/). <br>
Our model runs on the **Potomac River** subset of the original dataset.<br>
Selection criteria: HUCNAME_ containing 'Potomac'.


[Original Dataset](https://drive.google.com/file/d/12uoFlcn8pgeuxD2-seFak36KTvrFPKCt/view?usp=sharing)<br>
[Clean Dataset](./data/WQ_FINAL_with_Parameters.csv)

## Missing Values
- First, columns with more than 10% of NaN values were either dropped or NaN-s were imputed
- Second, rows with the remaining NaN values were dropped (at this point NaN-s were less than 10% of any one column)

> __Imputations:__<br>
><ins>Tidestage</ins>: Missing values were randomly filled by 'Ebb Tide' and 'Flood Tide'

## Target Variable 
**Total Phosphorus** <br>
__Categories:__ 
- healthy amount (0.01 - 0.03 mg/L)
- increased amount (0.025 - 0.1 mg/L)
- problematic amount (\> 0.1 mg/L)

## Features

- All parameter measures <br>
- Engineered features listed bellow<br>

#### Feature Engineering
__Transformed Variables:__
> - Date_Time -> Year and Months

__Dummified Variables:__
> - HUC12
> - Tide Stage
> - Sample ID


## Model Description

__Random Forest Classifier__<br>
> Hyperparameters:
> - n_estimators: 200
> - min_samples_split: 10
> - max_depth: None

__Evaluation of the Model__<br>

The model predicts whether or not the measured amount of total phosphorus is dangerously high, stimulates plant growth, or is at ta healthy level with a cross-validated __accuracy__ of __96%__. This supports the 96% testing accuracy, supporting the notion that the model generalizes well to yet unseen data. (Training accuracy score: 99%.) 

## Future Directions

- Extend the model to other areas of the Chesapeake Bay Watershed
- Build a timeseries model capable of forecasting increasing phosphorus levels allerting to the potential of harmful algea blooms

## Table of Contents

[Data cleaning](./01_WQ_Cleaning.ipynb)<br>
[Data transformation](./02_WQ_Transformation.ipynb)<br>
[Random Forest](./03_Model.ipynb)<br>
[Presentation](https://docs.google.com/presentation/d/1VRkR6QItJFE4X_mQ_-9SEt9KG4hi2e0wdtYizV-QUO8/edit#slide=id.g98a1113318_0_268)
[Presentation_Video](https://vimeo.com/458003934)


## Resources:
[Phosphates in the Environment - Water Research Center](https://water-research.net/index.php/phosphates)<br>
[Indicator: Phosphorus - U.S. Environmental Protection Agency](https://www.epa.gov/national-aquatic-resource-surveys/indicators-phosphorus)<br>
[Nutrient Pollution - U.S. Environmental Protection Agency](https://www.epa.gov/nutrientpollution/issue#:~:text=Nitrogen%20and%20phosphorus%20are%20nutrients,organisms%20that%20live%20in%20water.)<br>
[Nutrients: Phosphorus, - Minnesota Pollution Control Agency](https://www.pca.state.mn.us/sites/default/files/wq-iw3-22.pdf)<br>
[Harmful Algal Bloom - CDC](https://www.cdc.gov/habs/general.html)<br>
[Satellite Imagery Can Track Harmful Algal Blooms- USGS](https://www.usgs.gov/news/satellite-imagery-can-track-harmful-algal-blooms#:~:text=A%20joint%20collaboration%20between%20EPA,algal%20pigments%20in%20the%20water.)

