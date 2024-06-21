# Input & output datasets 

## Folder Structure

The folder is structured as follows:

```
## Unchanged data folders                         <- Provided by the course, no changes made                 
|── fragcurves
|── hydrology
|── losses_tables
|── muskingum
|── rating_curves 
|
## Unchanged data                                 <- Provided by the course, no changes made
|── dikeIjssel_alldata.xlsx    
|── dikeIjssel.xlsx
|── EWS.xlsx
|── rfr_strategies.xlsx
|
## Input/output data
|── exploratory_results_40000_one_policy.tar.gz       <- Results of 40.000 experiments with all levers set to 0, output of the Exploratory Modelling.ipynb notebook.
|── exploratory_results_40000_zero_policy.tar.gz      <- Results of 40.000 experiments with all levers set to 1, output of the Exploratory Modelling.ipynb notebook.
|── final_policies.csv                                <- Results of the Policy_robustness.ipynb notebook      
|── policies.csv                                      <- Results of the MOEA.ipynb notebook  
|── prim_results_box_vulnerability.csv                <- Results of the Policy_vulnerability.ipynb notebook
|── prim_results_box.csv                              <- Results of the Scenario_discovery.ipynb notebook
|── robustness_results.tar.gz                         <- Results of the Policy_robustness.ipynb notebook   
|── selected_scenarios.csv                            <- Selected scenarios from the Scenario_discovery.ipynb notebook
|── sequential_results.tar.gz                         <- Results of the SOBOL analysis in GSA.ipynb notebook