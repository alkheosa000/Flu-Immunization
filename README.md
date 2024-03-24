# Immunization Analysis
## An Analysis of Flu Shots compliance in 2022

## Data Understanding

This project utilized a simulated patient dataset extracted from [Synthea](https://github.com/synthetichealth/synthea). Synthea is a tool that generates synthetic patient populations with realistic medical histories. While not real-world data, it closely resembles real data allowing for exploration of healthcare trends and analysis techniques.

The project was inspired by a YouTube channel called Data Wizardry, but the analysis itself is independent.

## Data Sources and Variables

The data for this project came from three primary tables within the Synthea dataset:

- **Patients:** This table contains demographic information about each patient, such as age, gender, zip code, and socioeconomic factors.
- **Encounters:** This table details patient interactions with the healthcare system, including diagnoses, procedures, medications prescribed, and encounter dates.
- **Immunizations:** This table captures information about immunizations administered to patients, including vaccine type, date administered, and any recorded side effects.

By analyzing these tables and their associated variables, the project aimed to generate a Flu Shots dashboard for the year 2022 consumption among active patients.

## Objectives and Requirements

### Objectives:
The project aims to create a flu shots dashboard for 2022 that accomplishes the following:

1. Total % of patients getting flu shots stratified by:
   - Age
   - Race
   - County (On a Map)
   - Overall
2. Running Total of Flu Shots over the course of 2022
3. Total number of Flu shots given in 2022
4. A list of Patients that show whether or not they received the flu shots

### Requirements:
Patients must have been "Active at our hospital"

## SQL Code

I started by collecting all the information needed in the main query. Then, I started the data cleaning and processing methods where I removed all duplicates and null values by applying the following code in the common table expression.

### Common Table Expressions (CTEs):
- **active_patients:** This CTE selects distinct active patients within the given timeframe (between January 1, 2020, and December 31, 2022), ensuring that patients are alive (deathdate is null) and at least 6 months old by December.
- **flu_shot_2022:** This CTE identifies patients who received flu shots in 2022. I made sure to select the earliest flu shot date for each patient to avoid duplicates.

  ![Picture1](https://github.com/alkheosa000/Flu-Immunization/assets/162853772/18d6ee0b-ff7a-483f-b518-4fe8ade3f5b2)


### Main Query

- The main query selects various patient attributes such as birthdate, race, county, ID, first name, last name, and gender from the patients table. It also calculates the age of patients as of December 31, 2022.
- It left joins the patients table with the flu_shot_2022 CTE on patient ID to determine whether each patient received a flu shot in 2022. If a patient received a flu shot, the column flu_shot_2022 is set to 1; otherwise, it's set to 0.
- The where clause ensures that only active patients are considered by filtering based on the patients' IDs present in the active patients CTE.

  ![Picture2](https://github.com/alkheosa000/Flu-Immunization/assets/162853772/469ae466-f051-45ee-9a03-b55fd731fba9)

![Picture3](https://github.com/alkheosa000/Flu-Immunization/assets/162853772/1fb0f5bc-f20b-47df-968a-b5f17b9cf2ed)


## SQL Results

![Picture4](https://github.com/alkheosa000/Flu-Immunization/assets/162853772/40bd9f07-f457-4276-8492-5bd045ae0beb)


### Data Preparation and Exploration

1. **Data Extraction and Cleaning:** The desired data was extracted from the SQL database and saved as a comma-separated values (CSV) file. This file underwent a thorough cleaning process in Excel to ensure data integrity and readability.
2. **Data Import and Visualization in Tableau:** The cleaned CSV file was imported into Tableau Public Desktop. Various worksheets were created to explore specific aspects of the data.

###

  - Flu Shot by Age: This worksheet investigated the distribution of flu shots across different age groups.

  - Flu Shot by Race: This worksheet examined potential disparities in flu shot administration by race.

  - Flu Shot Percentage by County: This worksheet visualized the geographical distribution of flu shot coverage.

  - Flu Shot List: This worksheet presented a list of all active patients including both who taken the shot and who did not.

  - Total Compliance: This worksheet calculated the overall compliance rate for flu shots.

  - Flu Shots Given: This worksheet tracked the total number of flu shots administered.

  - Running Sum of Flu Shots 2022: This worksheet have displayed the cumulative number of flu shots administered throughout      2022.



## Dashboard Design and Development

Following the creation of these worksheets, appropriate visualizations were selected and developed within Tableau to effectively communicate the insights from each exploration.

[Dashboard link](https://public.tableau.com/views/Immunizationdashboard/Dashboard1?:language=en-US&:sid=&:display_count=n&:origin=viz_share_link)

![Picture5](https://github.com/alkheosa000/Flu-Immunization/assets/162853772/1ca1abb7-76e6-4efe-a2b0-3deaa4ed0890)


## Results

### Key Findings

- **Age Distribution of Flu Shots:** Analysis of the Flu Shots by Age visualization revealed a higher likelihood of flu shot uptake among individuals in the 0-17 and 65+ age groups. Conversely, the 18-49 age group demonstrated a lower vaccination rate.
- **Racial Disparities in Flu Shots:** The Flu Shot by Race visualization indicated a relatively close distribution of flu shots across racial groups. However, a slight trend towards higher acceptance among minorities compared to White people was observed.
- **Geographical Distribution of Flu Shot Compliance:** The Map visualization depicted a geographically consistent flu shot compliance rate across all six counties, with an average of 81.7%.

### Recommendations for Improved Flu Shot Compliance
#### Based on the analysis, here are some recommendations to enhance flu shot compliance rates:
- Targeted Outreach Programs: Develop age-specific outreach campaigns tailored to address the concerns and needs of the 18-  49 age group, historically less likely to receive flu shots.
- Culturally Sensitive Communication: Design culturally sensitive communication materials to address potential concerns and promote flu shot acceptance among minority populations.
- Convenience Initiatives: Explore strategies to increase vaccination accessibility, such as offering flu shot clinics at convenient locations and extended hours.
- Education and Awareness Campaigns: Launch educational campaigns emphasizing the importance of flu shots for individual and community health.
