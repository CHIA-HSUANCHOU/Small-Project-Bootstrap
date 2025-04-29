# Small-Project-Bootstrap to Salary Analysis for Entry-Level Data Scientists and Machine Learning Engineers
---
Project: Using Bootstrap to Salary Analysis for Entry-Level Data Scientists and Machine Learning Engineers

Author: CHOU CHIA-HSUAN

Date: 2025-04-25

Course: Statistical Computing

---

# 1. Research Motivation
Graduates from statistics departments often pursue careers in data science or machine learning. Given the growing demand in these fields, understanding the salary range for entry-level positions provides valuable insight for students' career planning.
This study aims to analyze the salary distribution of entry-level data scientists and further compare it with that of machine learning engineers to determine if there is a significant difference.

# 2. Research Questions

  1. What is the typical salary range for entry-level data scientists?

  2. What are the average and variability of their annual salaries?

  3. Is there a statistically significant difference between the annual salaries of entry-level data scientists and machine learning engineers?

# 3. Data Source, Description, and Preprocessing
### Data Source:
  Jobs and Salaries in Data Field 2024 – Kaggle Dataset：https://www.kaggle.com/datasets/murilozangari/jobs-and-salaries-in-data-field-2024

### Dataset Description:
  The dataset contains job listings and salary information for data-related positions in 2024, including the following columns:
work_year, experience_level, employment_type, job_title, salary, salary_currency, salary_in_usd, employee_residence, work_setting, company_location, company_size, job_category.

### Preprocessing Steps:

1. Filtered for Entry-Level positions to focus on early-career professionals.

2. Selected records with job titles containing "Data Scientist" or "Data Science", and "Machine Learning Engineer" or "ML Engineer".

3. Converted salary_in_usd to New Taiwan Dollars (TWD) by multiplying by 30 for better local interpretation.

4. Resulted in two groups for comparison:
 (1) Entry-Level Data Scientists
 (2) Entry-Level Machine Learning Engineers


# 4. Bootstrap Analysis
### 4.1 Estimating Bias, Variance, and MSE
The parameter of interest is the mean annual salary (in TWD) for entry-level data scientists.
Due to a small sample size (158 records), Bootstrap simulation with 1000 resamplings was used to estimate the following statistics:

- True Sample Mean: TWD 2,592,996

- True Sample Standard Deviation: TWD 1,269,985

- Bootstrap Mean: TWD 2,594,207

- Bootstrap Bias: TWD 1,211

- Bootstrap Std (SE): TWD 103,882

- Bootstrap MSE: TWD 10,792,866,223

- Conclusion:
The bootstrap simulation shows that the mean annual salary for entry-level data scientists is approximately TWD 2,594,207.
The estimated mean is very close to the original sample mean (difference of only TWD 1,200), indicating that the bootstrap mean is essentially unbiased.
While the original salary values have high variance, the standard error of the bootstrap estimate is relatively low (~TWD 100,000), and the MSE is within a reasonable range, suggesting the bootstrap estimate is reliable.

### 4.2 Confidence Intervals and Hypothesis Testing
#### Confidence Interval Estimation
Four Bootstrap methods were applied to estimate the 95% confidence interval for the mean annual salary of entry-level data scientists:

| Method              | Lower Bound (TWD) | Bootstrap Mean (TWD) | Upper Bound (TWD) |
|---------------------|-------------------|------------------------|--------------------|
| Simple Method       | 2,371,755         | 2,594,207              | 2,788,582          |
| Percentile Method   | 2,397,409         | 2,594,207              | 2,814,237          |
| BC Percentile       | 2,394,523         | 2,594,207              | 2,811,745          |
| BCa Percentile      | 2,394,681         | 2,594,207              | 2,814,237          |


- Observation:

- The Simple Method produced a narrower and lower confidence interval due to its symmetric reflection approach. Given the high salary variance, this method is more sensitive to extreme values.

- The Percentile, BC, and BCa methods yielded similar results. Since the salary distribution for data scientists is not highly skewed, bias correction and acceleration had little impact on the interval width.

#### Hypothesis Testing: Salary Comparison
- Objective:To test whether there is a significant difference in salary between entry-level data scientists and entry-level data engineers.

- Hypotheses:

$H_0$: No difference in salaries between the two groups

$H_1$: There is a significant difference in salaries

Significance Level:
$\alpha = 0.05$

- Methods and Results:

| Test Method              | ASL (p-value) | Decision             |
|--------------------------|---------------|-----------------------|
| Two-sample Bootstrap Test| 0.4920        | Do not reject $H_0$  |
| Permutation Test         | 0.0400        | Reject $H_0$         |

- Interpretation:

Although both bootstrap and permutation tests are valid for comparing mean salaries, their results differ in this study.

- Possible Reasons:

1. Sensitivity to outliers:
The salary distribution for ML Engineers is right-skewed with extreme high values, while that for Data Scientists is more symmetric.
The Permutation Test, which shuffles raw data directly, is more sensitive to such outliers.
The Bootstrap Test reduces their influence due to resampling.

2. Different assumptions:
The Permutation Test assumes exchangeability and similar distributions across groups, making it sensitive to shape differences.
The Bootstrap Test assumes each group is drawn from its own distribution, allowing more flexibility in comparison.
