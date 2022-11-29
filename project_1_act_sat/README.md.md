# Problem Statement
Pandemic has thrown things out of balance and, in relevance to this project, forced many universities to change their policies about SAT and ACT tests, which have traditionally been the gold standard to university admissions. 

We want to know how and where did the pandemic change SAT and ACT scores and participation; and how this insight can inform future decision making.

# Background

The SAT and ACT are standardized tests that many colleges and universities in the United States require for their admissions process. This score is used along with other materials such as grade point average (GPA) and essay responses to determine whether or not a potential student will be accepted to the university.

The SAT has two sections of the test: Evidence-Based Reading and Writing and Math ([*source*](https://www.princetonreview.com/college/sat-sections)). The ACT has 4 sections: English, Mathematics, Reading, and Science, with an additional optional writing section ([*source*](https://www.act.org/content/act/en/products-and-services/the-act/scores/understanding-your-scores.html)). ACT has score range between 1 to 36. SAT has score range between 400 to 1600.

* [SAT](https://collegereadiness.collegeboard.org/sat)
* [ACT](https://www.act.org/content/act/en.html)

Standardized tests have long been a controversial topic for students, administrators, and legislators. Since the 1940's, an increasing number of colleges have been using scores from students' performances on tests like the SAT and the ACT as a measure for college readiness and aptitude ([*source*](https://www.minotdailynews.com/news/local-news/2017/04/a-brief-history-of-the-sat-and-act/)). Supporters of these tests argue that these scores can be used as an objective measure to determine college admittance. Opponents of these tests claim that these tests are not accurate measures of students potential or ability and serve as an inequitable barrier to entry. Lately, more and more schools are opting to drop the SAT/ACT requirement for their Fall 2021 applications ([*read more about this here*](https://www.cnn.com/2020/04/14/us/coronavirus-colleges-sat-act-test-trnd/index.html)).

### Datasets

* [`act_2017.csv`](./data/act_2017.csv): 2017 ACT Scores by State
* [`act_2018.csv`](./data/act_2018.csv): 2018 ACT Scores by State
* [`act_2019.csv`](./data/act_2019.csv): 2019 ACT Scores by State
* [`act_2020.csv`](./data/act_2020.csv): 2020 ACT Scores by State
* [`act_2021.csv`](./data/act_2021.csv): 2021 ACT Scores by State
* [`sat_2017.csv`](./data/sat_2017.csv): 2017 SAT Scores by State
* [`sat_2018.csv`](./data/sat_2018.csv): 2018 SAT Scores by State
* [`sat_2019.csv`](./data/sat_2019.csv): 2019 SAT Scores by State
* [`sat_2020.csv`](./data/sat_2020.csv): 2020 SAT Scores by State
* [`sat_2021.csv`](./data/sat_2021.csv): 2021 SAT Scores by State
* [`us-counties-2020.csv`](./data/us-counties-2020.csv): 2020 COVID-19 data by State
* [`us-counties-2021.csv`](./data/us-counties-2021.csv): 2021 COVID-19 data by State
* [`per_student_spend_2017.csv`](./data/per_student_spend_2017.csv): 2017 Per Student Spend by State
* [`per_student_spend_2018.csv`](./data/per_student_spend_2018.csv): 2018 Per Student Spend by State
* [`per_student_spend_2019.csv`](./data/per_student_spend_2019.csv): 2019 Per Student Spend by State
* [`per_student_spend_2020.csv`](./data/per_student_spend_2020.csv): 2020 Per Student Spend by State

### COVID-19

The COVID-19 pandemic is an ongoing global pandemic caused by severe acute respiratory syndrome coronavirus 2 (SARS-CoV-2) ([*source*](https://www.who.int/health-topics/coronavirus#tab=tab_1)). The pandemic has caused not only severe disruptions to social and economic factors but also on education. ([*source*](https://www.washingtonpost.com/local/education/one-million-plus-juniors-will-miss-out-on-sats-and-acts-this-spring-because-of-coronavirus/2020/04/12/4ccc827c-7a95-11ea-b6ff-597f170df8f8_story.html))
- The metric that will be using is the number of cases as compared to ACT and SAT
- [*Data 2020 & 2021*](https://github.com/nytimes/covid-19-data)

### Per Student Spending by State
The public education spending per student of public elementary-secondary school systems by states comprises of Salary and Wages, Employee benefits, Instruction and Support Services. ([*source*](https://worldpopulationreview.com/state-rankings/per-pupil-spending-by-state))
- The metric that will be used is the total per student spending by state as compared to ACT and SAT participation and the total/composite score.
- [*Data 2017*](https://www.census.gov/data/tables/2017/econ/school-finances/secondary-education-finance.html)
- [*Data 2018*](https://www.census.gov/data/tables/2018/econ/school-finances/secondary-education-finance.html)
- [*Data 2019*](https://www.census.gov/data/tables/2019/econ/school-finances/secondary-education-finance.html)
- [*Data 2020*](https://www.census.gov/data/tables/2020/econ/school-finances/secondary-education-finance.html)

#
ACT Datasets after cleaning: act_2017, act_2018, act_2019, act_2020, act_2021
|Feature|Type|Description|
|---|---|---|
|**state**|*object*|50 states in USA and District of Columbia.| 
|**participation**|*float*|The mean participation level in each state.| 
|**composite**|*float*|The mean score of each state.|

#
SAT Datasets after cleaning:  sat_2017, sat_2018, sat_2019, sat_2020, sat_2021
|Feature|Type|Description|
|---|---|---|
|**state**|*object*|50 states in USA and District of Columbia.| 
|**participation**|*float*|The mean participation level in each state.|
|**total**|*float*|The mean score of each state.|

#
COVID Datasets after cleaning: us-counties-2020, us-counties-2021
|Feature|Type|Description|
|---|---|---|
|**state**|*object*|50 states in USA and District of Columbia.| 
|**cases**|*integer*|The number of covid cases in reported daily.|


#
Per Student Spending by State Datasets after cleaning: per_student_spend_2017, per_student_spend_2018, per_student_spend_2019, per_student_spend_2020
|Feature|Type|Description|
|---|---|---|
|**state**|*object*|50 states in USA and District of Columbia.| 
|**per_student_spend**|*integer*|The amount in US dollars that is spend on per student in the year.|


## Summary
#### ACT and SAT
##### ACT
1. From the ACT Participation Levels between 2017-2018, there is an increase in the participation levels. 
2. However, the reduction of participation level was seen starting from 2019 till 2021. 
-   A reduction in the 1.0 participation level and 0.2 participation level.
-   An increase the 0.1 participation level.

- From the ACT Composite Scores, for the year 2021, there is a clear divide in the scores where there are states scoring more than 26.
- In another group of states students scoring the other end of the spectrum (composite scores between 18 to 21)


##### SAT
- From the histogram plots across the years for 2017 to 2019, there is an increase in the participation level.
- For 2020 and 2021, there is a sharp drop in the participation levels. (huge decrease for participation at 1.0 level and 0.7 level, and an increase in 0.5 level and 0.0 level)
- For 2020 to 2021, the total SAT scores did not reach 1300 levels and the score for 1000 are higher than the rest of the years.

Comparing Participation Levels correlation between ACT and SAT
- The ACT participation 2020 has an inverse relation with the SAT participation 2020 of 0.87.
- The ACT participation 2021 has an inverse relation with the SAT participation 2021 of 0.83.

#### COVID19 DATA
- There is a very weak correlation between COVID cases and the relation between ACT and SAT for the years 2020 and 2021.

#### Per Student Spending
- On average there is a 2.5 to 3.8% increase in per student spending from 2017 to 2020
- Across the years between 2017 to 2020, there is a correlation between the spending and ACT composite score of 0.62 to 0.64.
- Across the years between 2017 to 2020, there is a negative correlation between the spending and ACT participation of 0.49 to 0.54.
- The spending has a weak correlation with the SAT participation of 0.39 to 0.46.
- The spending does not have much correlation with SAT total score.

#### Conclusions

1. From the above analysis, there is a fall in the participation level in both the ACT and SAT. There is a divide for the composite/total score for ACT and SAT on either of the spectrum. 
2. There is weak correlation data between the COVID cases in each state versus ACT and SAT participation level and composite/total score.
3. The per student spending has strong correlation with the ACT composite score but a negative correlation on the ACT participation level. Whereas, the per student spending has a weak correlation with the SAT participation level and not much correlation with the SAT total score.

Even though there is a weak correlation data for the COVID cases, it does not mean that the ACT and SAT are independent of COVID. Rather there could be other factors that could be affecting the outcome of ACT and SAT where the study of per student spending shows some relation with ACT.

#### Recommendations
1. Further analysis would need to be explored include mitigation or precaution that was taken to ensure that ACT or SAT could be continue to be taken during COVID at State level.
2. Universities that used other metric for entry requirements and do not require ACT/SAT score for admissions.
3. States that either still maintain or changed their policy on ACT or SAT as a Graduation requirement.
4. Other social economic factors such as income level and family & social support.
5. The analysis could also be performed on county level rather than on state level.
