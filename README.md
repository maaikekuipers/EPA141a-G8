# Flood Risk Management on the IJssel River: A Delta Commission Perspective

Created by: EPAcourse Group

|    Name               | Student Number |
| :-------------------: | :------------- |
| Maaike Kuipers        | 4882466        |
| Brechje Smits         | 6000983        |
| Cato Martens          | 4799003        |
| Arnoud van Rooijen    | 5674131        |

## Introduction

This project, part of the EPA141A - Model-based Decision-Making course at TU Delft, focuses on developing a flood risk management plan for the upper branch of the IJssel River in the Netherlands. The study employs advanced modeling techniques to assess the vulnerability and criticality of flood protection measures using a simulation model provided by the course. The primary goal is to deliver robust recommendations to the Delta Commission to enhance flood resilience in the region.

## Setup and Installation

To set up the environment for running the simulations and analyses, follow these steps:

1. Ensure you have Python installed on your machine.
2. Clone or download the project files to your local machine.
3. Open a terminal and navigate to the project directory.
4. Install the required Python packages using the following command:

```
$ pip install -r requirements.txt
```

## Folder Structure

The folder is structured as follows:

```
|
|── archives                      <- Archives of MOEA analysis (MOEA.ipynb)
|
|── archives_epsilon              <- Archives of epsilon discovery in MOEA analysis (MOEA.ipynb)
|
├── data                          <- Data folder containing input/output datasets. Read the   
|                                    README.md in this folder for more information.
│
## Unchanged model files          <- Provided by the course, no changes made                 
|── __init__.py  
|── .gitattributes
|── dike_model_function.py
|── dike_model_optimization.py
|── dike_model_simulation.py
|── funs_dikes.py
|── funs_economy.py
|── funs_generate_network.py
|── funs_hydrostat.py
│
## Changed model files            <- Provided by the course, changes were made to speficy the problem formulation
|── problem_formulation.py      
|
## Notebooks                      <- All Jupyter notebooks used for doing analysis and representing the results.
|── Epsilon_investigation.ipynb   <- Discussed in Chapters 3.4 & 4.4 in the report
│── Exploratory_modelling.ipynb   <- Discussed in Chapters 3.1 & 4.1 in the report
|── Extra_trees.ipynb             <- Discussed in Chapters 3.2 & 4.2 in the report
|── GSA.ipynb                     <- Discussed in Chapters 3.2 & 4.2 in the report
|── MOEA_Analysis.ipynb           <- Discussed in Chapters 3.4 & 4.4 in the report 
|── Policy_robustness.ipynb       <- Discussed in Chapters 3.5 & 4.5 in the report
|── Policy_vulnerability.ipynb    <- Discussed in Chapters 3.6 & 4.6 in the report
|── Scenario_discovery.ipynb      <- Discussed in Chapters 3.2 & 4.2 in the report
│
├── README.md                     <- Top-level README for an overview of the project.
│
├── requirements.txt              <- Contains the list of Python packages needed to run the project.
```

## Changes in Problem Formulation Script

### New Features Added:

1. **New Problem Formulation (ID 6)**:
   - Added a comprehensive problem formulation for the Delta Commission.
   - Objectives include:
     - Expected Annual Damage
     - Dike Investment Costs
     - RfR Investment Costs
     - Evacuation Costs
     - Expected Number of Deaths
     - Total Investment Costs

2. **Enhanced Documentation**:
   - Updated descriptions to include the new problem formulation and its objectives.

### Summary of Problem Formulations:

1. **ID 0**: Total cost and casualties
2. **ID 1**: Expected damages, costs, and casualties
3. **ID 2**: Expected damages, dike investment costs, RfR costs, evacuation costs, and casualties
4. **ID 3**: Costs and casualties disaggregated over dike rings, RfR, and evacuation costs
5. **ID 4**: Expected damages, dike investment cost, and casualties disaggregated over dike rings, RfR, and evacuation costs
6. **ID 5**: Disaggregate over time and space
7. **ID 6**: Expected damages, costs, casualties, and total costs for the Delta Commission (new)

### Usage:

To use the new problem formulation, call the `get_model_for_problem_formulation` function with `problem_formulation_id` set to `6`. This will configure the model to include the additional objectives required by the Delta Commission.

### Steps for Running the Analysis

#### Step 1: Exploratory Modelling

The following steps are performed in the `Exploratory Modelling.ipynb` notebook:
1. **Run 40,000 experiments with all levers set to 0.** 
    - This analyzes a base-scenario.
    - Results are saved in `data/exploratory_results_40000_zero_policy.tar.gz`.
2. **Run 40,000 experiments with all levers set to 1.**
    - This analyzes the most extreme intervention scenario.
    - Results are saved in `data/exploratory_results_40000_one_policy.tar.gz`.

**Objective:** To show potential tradeoffs.

#### Step 2: Scenario Discovery

The following steps are performed in the `Scenario Discovery.ipynb` notebook:

1. **Scenario Discovery using PRIM:**
    - Apply the Patient Rule Induction Method (PRIM) algorithm to identify critical scenarios affecting flood risk management policies.
    - PRIM helps identify combinations of input parameters that result in particular outcomes, such as the number of deaths, under conditions of deep uncertainty.

2. **Interpretation of PRIM Results:**
    - Focus on key parameters like **A.1_pfail** and **A.3_pfail**, representing the probabilities that dikes at specific locations will withstand hydraulic load.
    - Analyze the constrained ranges and their influence on scenario outcomes.

3. **Parameter Influence Analysis:**
    - Evaluate how ranges of parameters like **A.1_pfail** and **A.3_pfail** influence the scenario outcomes.
    - Understand the critical conditions under which the dikes might withstand the load.

4. **Coverage and Density Assessment:**
    - Determine the coverage and density of the identified high-risk scenarios.
    - High coverage (e.g., 81.5%) indicates a significant portion of relevant cases, while high density (e.g., 88%) indicates precision in the identified scenarios.

5. **Discovered Scenarios:**
    - The discovered scenarios, including the worst case, are saved in `data/selected_scenarios.csv`.

**Objective:** To identify and analyze critical scenarios that could impact the effectiveness of flood defense strategies.

#### Step 3: Global Sensitivity Analysis (GSA)

The following steps are performed in the `GSA.ipynb` notebook:

1. **Global Sensitivity Analysis using Sobol Method:**
    - Perform a global sensitivity analysis to understand how uncertainties influence the outcomes using the Sobol method via the EMA workbench (SaLib).

2. **Visual Analysis:**
    - Visualize the sensitivity indices to identify key uncertainties.

3. **Results Interpretation:**
    - **Expected Annual Damage:**
        - Key uncertainties: **A3_3_pfail** (highest sensitivity), **A1_pfail**.
    - **Expected Number of Deaths:**
        - Key uncertainties: **A1_pfail** (highest sensitivity), **A3_3_pfail**.
        - Other factors: Discount Rate, **A2_Bmax**, **A3_Brate** also impact the outcomes.
    - **Save Results:**
        - Reults are saved in `data/sobol_results.tar.gz`

**Objective:** To determine the most influential uncertainties affecting flood risk scenarios.

#### Step 4: Feature Scoring

The following steps are performed in the `extra_trees.ipynb` notebook:

1. **Feature Scoring:**
    - Evaluate the relevance/contribution of the uncertainties to the outcomes of the model.
    - Outcomes considered: Expected Annual Damage, Dike Investment Costs, RfR Investment Costs, Evacuation Costs, Expected Number of Deaths.

2. **Results Interpretation:**
    - **A1_pfail:**
        - Most critical for Expected Annual Damage (score: 0.56) and significant for Expected Number of Deaths (score: 0.17).
    - **A3_pfail:**
        - Important for Expected Annual Damage (score: 0.19) and most critical for Expected Number of Deaths (score: 0.62).
    - **Discount Rates:**
        - Minor impact on Expected Annual Damage and Expected Number of Deaths.
    - **Other Variables:**
        - Breach width and breach growth rate generally have low influence on the outcomes.

**Objective:** To assess the importance of various uncertainties in determining the model's outcomes.\\

#### Step 5: Policy Discovery
##### Step 5.1: Multi-Objective Evolutionary Algorithm (MOEA) Analysis

The following steps are performed in the `MOEA_Analysis.ipynb` notebook:

1. **Count Total Policies:**
    - Determine the total number of policies present in the results.

2. **Filter Dominated Policies:**
    - Identify and retain only the non-dominated policies from the results.

3. **Calculate Metrics:**
    - Compute various metrics for the archives against a reference set.
    - The archives are saved in the folder `archives`

4. **Plot Metrics:**
    - Visualize the metrics and convergence progress using plots.

5. **Deleting all cases where Total Number of Deaths > 0:**
    - To meet the objecctive of the Delta Commission, all cases where the amount of deaths is higher than 0 are removed.

5. **Safe Results:**
    - Results are saved in `data/policies.csv`

**Objective:** To filter and analyze the optimization results, retaining the most effective policies.

##### Step 5.2: Epsilon Investigation

The following steps are performed in the `Epsilon_investigation.ipynb` notebook:

1. **Analysis and Investigation:**
    - Perform a detailed investigation into the epsilon parameter and its impact on the optimization process.
    - The archives are saved in the folder `archives_epsilon`

2. **Result Interpretation:**
    - Analyze and interpret the results to understand the influence of epsilon on the model outcomes.

3. **Using Epsilon values**
    - The optimal epsilon values are used in the notebook `MOEA_Analysis.ipynb`

**Objective:** To investigate the role of the epsilon parameter in the optimization process and its impact on the model's performance.

#### Step 6: Robustness Analysis

The following steps are performed in the `Policy_robustness.ipynb` notebook:

1. **Re-evaluate Candidate Solutions Under Uncertainty**:
   - Re-evaluate the selected policies from `MOEA_analysis.ipynb` under different deeply uncertain factors.
   - 65 policies have emerged that meet the Delta Commission's hard constraint of zero annual expected deaths.
   - 1000 random scenarios are used for robustness evaluation.

2. **Loading Results**:
   - Import results of the robustness analysis to ensure the correctness of the evaluations.

3. **Evaluating Policy Robustness**:
   - Assess each policy's performance across different outcome indicators under 1000 scenarios.
   - Use metrics such as the signal-to-noise ratio (SNR) to quantify robustness.

4. **Calculation of Signal-to-Noise Ratio (SNR)**:
   - For minimizing outcome indicators, a lower product of mean and standard deviation indicates better performance.
   - For maximizing outcome indicators, a higher mean and lower standard deviation are desired.

5. **Visualization of Robustness**:
   - Visualize robustness using different plots and figures to understand the performance and stability of each policy.

6. **Comparing Robustness Across Policies**:
   - Use scatter plots to compare different policies based on robustness metrics.
   - Policies are analyzed for trade-offs between robustness and performance.

7. **Policy Insights**:
   - Analyze specific policies to understand their strengths and weaknesses.
   - Discuss how some policies show low regret in costs but high regret in damages and fatalities.

8. **Final Policy Selection**:
   - Filter policies based on the 20th quantile of the expected number of deaths to focus on the most critical outcomes.
   - Identify policies that balance costs and fatalities effectively.

9. **Visualization of Final Policies**:
   - Provide a detailed comparison of selected policies, highlighting their investment strategies and outcomes.
   - Discuss policies like Policy_44, Policy_51, Policy_72, and Policy_75 in detail.

**Objective:** To assess and compare the robustness of different policies to ensure effective flood risk management under uncertainty.

#### Step 7: Policy Vulnerability Analysis

The following steps are performed in the `Policy Vulnerability.ipynb` notebook:

1. **Re-evaluate Candidate Solutions Under Vulnerability**:
   - Re-evaluate the selected policies under scenarios where they might fail.
   - Focus on understanding the scenarios that lead to high expected deaths despite the implemented policies.

2. **PRIM Analysis**:
   - Use the Patient Rule Induction Method (PRIM) to identify critical scenarios affecting policy effectiveness.
   - Examine the coverage and density of the identified scenarios to understand their relevance and concentration.

3. **Interpreting PRIM Analysis**:
   - Analyze key parameters like **A.3_pfail**, representing the probability of failure for dike ring A3.
   - Understand how variations in these parameters influence the likelihood of policy failure.

4. **Density and Coverage Interpretation**:
   - Density represents the proportion of scenarios that are relevant to high expected deaths.
   - Coverage shows the proportion of all relevant cases captured by the scenario.

5. **Visualizing Vulnerability**:
   - Visualize the density and distribution of high-risk versus low-risk scenarios for critical parameters.
   - Identify critical thresholds where the likelihood of high-risk scenarios increases.

6. **Policy Insights**:
   - Analyze specific policies to understand their vulnerability points.
   - Discuss the implications of parameter variations on policy effectiveness.

7. **Final Policy Recommendations**:
   - Provide recommendations for improving policy robustness based on vulnerability analysis.
   - Highlight critical ranges for interventions to mitigate flood risks effectively.

**Objective:** To identify and analyze scenarios where the proposed policies may fail, providing insights into improving policy robustness and effectiveness.

## Acknowledgments

This project is part of the coursework for the EPA course EPA141A Model-based Decision-Making. The model and associated documentation were developed to fulfill the project requirements, building upon the foundational model provided by the course.
