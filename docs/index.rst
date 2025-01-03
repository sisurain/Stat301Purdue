.. STAT 301 documentation master file, created by
   sphinx-quickstart on Sat Aug 17 02:06:35 2024.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

STAT 301 @Purdue
======================
Welcome to the STAT 301 resource site, designed to provide supplementary materials for Purdue University students. As I am new to teaching this course, I will be adding more materials as the semester progresses. Please note that the content here may contain errors or mistakes; if you spot any, I encourage you to contact me.

The views expressed in this document are my own and do not necessarily reflect those of other instructors for this class. STAT 301 is a university-wide undergraduate course that serves a large and diverse student body. If you have any concerns about the materials presented here, please don't hesitate to reach out.

My primary goal with this resource is to support your learning in STAT 301, and to inspire you to explore statistics further. I hope that what you learn in this class will be valuable to you in the future, and that five or ten years from now, you'll still remember something useful from this experience.

Week 14: Special Topic: Simple Least Squares Regression in Matrix Form
=====================================================================

We have a data set consists of :math:`n` paired observations of the predictor/explanatory variable :math:`X` and the response variable :math:`Y`, i.e., :math:`(x_1, y_1), (x_2, y_2), \dots, (x_n, y_n)`. We wish to fit the model with a regression line:

.. math::

   y_n = \beta_0 + \beta_1 x_n + \epsilon_n

where we have the assumptions, :math:`\mathbb{E}[\epsilon_n | x_1, \dots, x_n] = 0`, :math:`\text{Var}[\epsilon_n | x_1, \dots, x_n] = \sigma^2`, and :math:`\epsilon_n` is uncorrelated across measurements. And the parameters are, :math:`\beta_0, \beta_1`, and :math:`\sigma`.

The Matrix Representation
-------------------------

Group all of the observations of the response into a single column :math:`(n \times 1)` matrix :math:`\mathbf{y}`:

.. math::

   \mathbf{y} =
   \begin{bmatrix}
   y_1 \\
   y_2 \\
   \vdots \\
   y_n
   \end{bmatrix}

Similarly, we group both coefficients into a single vector (i.e., a :math:`2 \times 1` matrix):

.. math::

   \beta =
   \begin{bmatrix}
   \beta_0 \\
   \beta_1
   \end{bmatrix}

We’d also like to group the observations of the predictor variable together:

.. math::

   \mathbf{x} =
   \begin{bmatrix}
   1 & x_1 \\
   1 & x_2 \\
   \vdots & \vdots \\
   1 & x_n
   \end{bmatrix}

This is an :math:`n \times 2` matrix, where the first column is always 1, and the second column contains the actual observations of :math:`X`. Then we have:

.. math::

   \mathbf{x}\beta =
   \begin{bmatrix}
   \beta_0 + \beta_1 x_1 \\
   \beta_0 + \beta_1 x_2 \\
   \vdots \\
   \beta_0 + \beta_1 x_n
   \end{bmatrix}

That is, :math:`\mathbf{x}\beta` is the :math:`n \times 1` matrix which contains the predictions. The matrix :math:`\mathbf{x}` is sometimes called the **design matrix**.

So we have:

.. math::

   \mathbf{y} = \mathbf{x}\beta + \mathbf{\epsilon}


Mean Squared Error in Matrix Form
---------------------------------

At each data point, using the coefficients :math:`\hat{\beta}` results in some error of prediction, so we have :math:`n` prediction errors. These form a vector:

.. math::

   \mathbf{e}(\hat{\beta}) = \mathbf{y} - \mathbf{x}\hat{\beta}


When we derived the least squares estimator, we wish to find the :math:`\hat{\beta}` which will minimize mean squared error, defined as:

.. math::

   MSE(\hat{\beta}) = \frac{1}{n} \sum_{i=1}^{n} e_i^2(\hat{\beta})

Again, we can write this equation in matrix form:

.. math::

   MSE(\hat{\beta}) = \frac{1}{n} \mathbf{e}^\top \mathbf{e}

To see this, look at what the matrix multiplication really involves:

.. math::

   \mathbf{e}^\top \mathbf{e} = [e_1, e_2, \dots, e_n]
   \begin{bmatrix}
   e_1, \\
   e_2, \\
   \vdots,\\
   e_n
   \end{bmatrix}

This equals :math:`\sum_i e_i^2`.

Expanding MSE Matrix
--------------------

Let us expand the MSE matrix for further use.

.. math::

   MSE(\hat{\beta}) = \frac{1}{n} \mathbf{e}^\top \mathbf{e} 

   = \frac{1}{n} (\mathbf{y} - \mathbf{x}\hat{\beta})^\top (\mathbf{y} - \mathbf{x}\hat{\beta}) 

   = \frac{1}{n} (\mathbf{y}^\top - \hat{\beta}^\top \mathbf{x}^\top)(\mathbf{y} - \mathbf{x}\hat{\beta}) 

   = \frac{1}{n} (\mathbf{y}^\top \mathbf{y} - \mathbf{y}^\top \mathbf{x}\hat{\beta} - \hat{\beta}^\top \mathbf{x}^\top \mathbf{y} + \hat{\beta}^\top \mathbf{x}^\top \mathbf{x} \hat{\beta}) 


Notice that :math:`(\mathbf{y}^\top \mathbf{x}\hat{\beta})^\top = \hat{\beta}^\top \mathbf{x}^\top \mathbf{y}`. Further notice that this is a :math:`1 \times 1` matrix, a scalar, so :math:`\mathbf{y}^\top \mathbf{x}\hat{\beta} = \hat{\beta}^\top \mathbf{x}^\top \mathbf{y}`. Thus:

.. math::

   MSE(\hat{\beta}) = \frac{1}{n} (\mathbf{y}^\top \mathbf{y} - 2\hat{\beta}^\top \mathbf{x}^\top \mathbf{y} + \hat{\beta}^\top \mathbf{x}^\top \mathbf{x} \hat{\beta}) 

Minimizing the MSE
------------------

First, we find the gradient of the MSE with respect to :math:`\hat{\beta}`:

.. math::

   \nabla MSE(\hat{\beta}) = \frac{1}{n} (\nabla \mathbf{y}^\top \mathbf{y} - 2 \nabla \hat{\beta}^\top \mathbf{x}^\top \mathbf{y} + \nabla \hat{\beta}^\top \mathbf{x}^\top \mathbf{x} \hat{\beta}) 

   = \frac{1}{n} (\mathbf{0} - 2\mathbf{x}^\top \mathbf{y} + 2\mathbf{x}^\top \mathbf{x}\hat{\beta}) 

   = \frac{2}{n} (\mathbf{x}^\top \mathbf{x} \hat{\beta} - \mathbf{x}^\top \mathbf{y})

We now set this to zero to solve the optimum, :math:`\hat{\beta}`:

.. math::

   \mathbf{x}^T \mathbf{x} \hat{\beta} - \mathbf{x}^T \mathbf{y} = \mathbf{0}

This equation, for the two-dimensional vector :math:`\hat{\beta} = [\hat{\beta_0}, \hat{\beta_1}]^\top`.

Solving, we have:

.. math::

   \hat{\beta} = (\mathbf{x}^\top \mathbf{x})^{-1} \mathbf{x}^\top \mathbf{y}

Here are the results from the textbook:

.. figure:: /images/1401.png


Week 13: Ch2.6 Two-Way Tables and Ch9.1 Inference for Two-Way Tables
====================================================================

Objectives
----------

When you complete this section, you will be able to:

* Identify the row variable, the column variable, and the cells in a two-way table.

* Find and interpret the joint distribution in a two-way table.

* Find and interpret the marginal distributions in a two-way table.

* Use conditional distributions to describe the relationship in a two-way table.

* Interpret Simpson’s paradox.

Introduction
------------

When analyzing relationships between two variables, it's important to determine whether the variables are quantitative or categorical:

- **Quantitative variables** are analyzed using scatterplots.

- **Categorical variables** are analyzed using counts (frequencies) or percents (relative frequencies).

The Two-Way Table
-----------------

A **two-way table** displays counts of observations for each combination of values of two categorical variables.

**Example 2.40: Is the calcium intake adequate?**

The table summarizes whether children met the calcium requirement based on their age group (5 to 10 years or 11 to 13 years):

- There are 2,029 children in the study.

- Each child’s calcium intake is classified as meeting or not meeting the requirement.

.. list-table:: Two-way table for Met Requirement and Age
   :header-rows: 1

   * - Met Requirement
     - 5 to 10
     - 11 to 13
   * - No
     - 194
     - 557
   * - Yes
     - 861
     - 417

The **row variable** is "Met Requirement," and the **column variable** is "Age Group."

Adding Margins
--------------

Adding margins helps to summarize the data by showing totals for each row and column.

**Example 2.41: Add the margins to the table**

.. list-table:: Expanded Two-way Table with Margins
   :header-rows: 1

   * - Met Requirement
     - 5 to 10
     - 11 to 13
     - Total
   * - No
     - 194
     - 557
     - 751
   * - Yes
     - 861
     - 417
     - 1,278
   * - Total
     - 1,055
     - 974
     - 2,029

- There were 1,055 children aged 5 to 10 and 974 children aged 11 to 13.

- The total number of children who did not meet the calcium requirement is 751.

Row and Column Variables
------------------------

- The **row variable** indicates whether the requirement was met.

- The **column variable** indicates the age group.

- Each cell in the table corresponds to a specific combination of row and column variables.

Joint Distribution
------------------

The **joint distribution** shows the proportion of each cell in relation to the total sample size.

**Example 2.42: The Joint Distribution**

.. list-table:: Joint Distribution of Met Requirement and Age
   :header-rows: 1

   * - Met Requirement
     - 5 to 10
     - 11 to 13
   * - No
     - 0.0956
     - 0.2745
   * - Yes
     - 0.4243
     - 0.2055

- The sum of the joint distribution proportions is approximately 1 (0.9999 due to rounding).

- This table helps determine targeted interventions based on age groups and calcium intake.

Marginal Distributions
----------------------

A **marginal distribution** provides the distribution of one categorical variable in a two-way table.

**Example 2.43: Marginal Distribution of Age**

.. list-table:: Marginal Distribution of Age
   :header-rows: 1

   * - Age Group
     - Proportion
   * - 5 to 10
     - 0.52
   * - 11 to 13
     - 0.48

- In this sample, 52% of the children are aged 5 to 10, and 48% are aged 11 to 13.

**Example 2.44: Marginal Distribution of Met Requirement**

This table shows the distribution of whether children met the calcium requirement:

.. list-table:: Marginal Distribution of Met Requirement
   :header-rows: 1

   * - Met Requirement
     - Percent
   * - No
     - 37.01%
   * - Yes
     - 62.99%

- The majority of children (63%) meet the recommended calcium intake.

Graphical Representation
------------------------

Marginal distributions can be visualized using bar graphs or pie charts. These graphical displays are useful when summarizing more complex tables. For this example:

- 52% of children are aged 5 to 10.

- 37% of children do not meet the calcium requirement.

Graphical displays help provide a clear and immediate summary of the data, especially when there are multiple rows or columns in the table.

Conditional Distributions
-------------------------

In :ref:`Example 2.45 <example_2_45>`, we examined the conditional distribution of the Met Requirement variable for children aged 5 to 10. This analysis is an example of conditioning on the value of age to calculate the distribution of the Met Requirement.

.. _example_2_46:

**Example 2.46: Conditional Distribution of Met Requirement for Children Aged 5 to 10**

For children aged 5 to 10 years, the conditional distribution of the Met Requirement variable is given as follows:

.. list-table:: Conditional Distribution of Met Requirement for Children Aged 5 to 10
   :header-rows: 1
   :widths: 30 35 35

   * - Met Requirement
     - No
     - Yes
   * - Percent
     - 18.39%
     - 81.61%

- These percentages sum to 100%. In this group, 81.61% met the requirement, while 18.39% did not.

Bar Graphs and Interpretation
-----------------------------

Bar graphs are helpful in visualizing relationships between two categorical variables. They do not provide a single numerical summary like correlation but allow for flexible comparisons based on chosen categories.

.. warning::
   A two-way table contains a great deal of information in a compact form. Accurately interpreting this information often requires calculating appropriate percentages. It is advisable to use software for computations to ensure accuracy when interpreting joint, marginal, and conditional distributions.

Simpson's Paradox
-----------------

An association or comparison that holds for several groups can sometimes reverse direction when the data are combined to form a single group. This reversal is known as **Simpson’s paradox**.

**Example 2.48: Which Team Had Better Shooters?**

Statistics from basketball games include percentages of field goals made. Here are the raw counts for a recent game between Team A and Team B:

.. list-table:: Shooting Performance of Teams
   :header-rows: 1

   * - Outcome
     - Team A
     - Team B
   * - Made
     - 28
     - 26
   * - Missed
     - 32
     - 34
   * - Total Shots
     - 60
     - 60

- **Success Rate**:

  - Team A: :math:`\frac{28}{60} = 46.7\%`

  - Team B: :math:`\frac{26}{60} = 43.3\%`

- Initial observation suggests Team A had better shooters (46.7% vs. 43.3%).

**Example 2.49: Detailed Breakdown of Shooting Data**

When we break down the data by shot type (2-pointers vs. 3-pointers), we see a different result:

.. list-table:: Breakdown by Type of Shot
   :header-rows: 1

   * - Outcome
     - 2-pointers (Team A)
     - 2-pointers (Team B)
     - 3-pointers (Team A)
     - 3-pointers (Team B)
   * - Made
     - 25
     - 16
     - 3
     - 10
   * - Missed
     - 25
     - 14
     - 7
     - 20
   * - Total Shots
     - 50
     - 30
     - 10
     - 30

- **Success Rates**:

  - **2-pointers**:

    - Team A: :math:`\frac{25}{50} = 50.0\%`

    - Team B: :math:`\frac{16}{30} = 53.3\%`

  - **3-pointers**:

    - Team A: :math:`\frac{3}{10} = 30.0\%`

    - Team B: :math:`\frac{10}{30} = 33.3\%`

- Although Team A had a higher overall success rate, Team B performed better for both 2-pointers and 3-pointers.

**Analysis**:

- The difference in results can be attributed to the type of shot (2-pointers vs. 3-pointers), which serves as a lurking variable.

- Team A took more of the easier 2-pointers (:math:`\frac{50}{60} = 83.3\%`), while Team B had fewer (:math:`\frac{30}{60} = 50.0\%`).

- This example illustrates **Simpson’s paradox**, where observed associations can be misleading when data are aggregated without considering important lurking variables.

Conclusion
----------

Simpson’s paradox shows that conclusions drawn from aggregated data may differ from those drawn from the analysis of disaggregated data. Always consider the possibility of lurking variables when interpreting statistical results.

**Additional Example Intuition**:

Imagine two hospitals, A and B, where the success rate of a certain surgery appears higher for Hospital A when considering all surgeries together. However, if we separate the surgeries based on whether they were for high-risk or low-risk patients:

- Hospital B might have better success rates for both high-risk and low-risk surgeries.

- Hospital A may have treated a disproportionately higher number of low-risk patients (easier surgeries), inflating its overall success rate.

Thus, the aggregation ignores the differences in patient risk, leading to a misleading conclusion.

**Summary**:
Simpson’s paradox reveals how misleading it can be to interpret aggregated data without considering the influence of lurking variables. It demonstrates the importance of:

- Breaking down the data by relevant subgroups.

- Accounting for confounding factors in the analysis.

- Interpreting results carefully, especially when making decisions based on combined statistics.

.. warning::
   Always check for lurking variables or potential confounding factors when interpreting aggregated data. Simpson’s paradox serves as a reminder that aggregated statistics can be misleading without careful analysis of underlying subgroups.


Week 13: Inference of Two-Way Tables
====================================

Crosstabs (Contingency Tables)
------------------------------

A **crosstab** or **contingency table** displays the frequency distribution of variables and is often used to analyze the relationship between two categorical variables. Each cell shows the count of occurrences for each combination of categories.

**Example: Gender and Product Preference**

Consider a study examining the relationship between **gender** and **product preference**:

.. list-table:: Gender and Product Preference
   :header-rows: 1

   * - 
     - **Product A**
     - **Product B**
     - **Total**
   * - **Male**
     - 40
     - 20
     - 60
   * - **Female**
     - 50
     - 30
     - 80
   * - **Total**
     - 90
     - 50
     - 140

Here:

- The rows represent **gender** (Male and Female).

- The columns represent **product preference** (Product A and Product B).

- Each cell contains the count of observations for each combination.

Chi-Square Test of Independence
-------------------------------

The **Chi-Square Test of Independence** is used with contingency tables to determine if there is a significant association between two categorical variables.

- **Null Hypothesis** (:math:`H_0`): The two variables are independent.

- **Alternative Hypothesis** (:math:`H_a`)**: The two variables are not independent.

Calculating Expected Counts
~~~~~~~~~~~~~~~~~~~~~~~~~~~

The **expected count** for each cell is calculated assuming that the two variables are independent. The formula for the expected count in each cell is:

.. math::
   E = \frac{(\text{Row Total} \times \text{Column Total})}{\text{Grand Total}}

Using the table above:

- **Row Totals**: Male = 60, Female = 80

- **Column Totals**: Product A = 90, Product B = 50

- **Grand Total**: 140

Let's calculate the expected counts for each cell:

- Expected Count for (Male, Product A):

  .. math::
     E_{\text{Male, Product A}} = \frac{(60 \times 90)}{140} = \frac{5400}{140} = 38.57

- Expected Count for (Male, Product B):

  .. math::
     E_{\text{Male, Product B}} = \frac{(60 \times 50)}{140} = \frac{3000}{140} = 21.43

- Expected Count for (Female, Product A):

  .. math::
     E_{\text{Female, Product A}} = \frac{(80 \times 90)}{140} = \frac{7200}{140} = 51.43

- Expected Count for (Female, Product B):

  .. math::
     E_{\text{Female, Product B}} = \frac{(80 \times 50)}{140} = \frac{4000}{140} = 28.57

Summary Table with Observed and Expected Counts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: Observed and Expected Counts
   :header-rows: 1

   * - 
     - **Product A (O)**
     - **Product A (E)**
     - **Product B (O)**
     - **Product B (E)**
   * - **Male**
     - 40
     - 38.57
     - 20
     - 21.43
   * - **Female**
     - 50
     - 51.43
     - 30
     - 28.57

Calculating the Chi-Square Statistic
------------------------------------

The Chi-Square statistic is calculated using the formula:

.. math::
   \chi^2 = \sum \frac{(O - E)^2}{E}

where:

- \( O \) is the observed frequency in each cell.

- \( E \) is the expected frequency in each cell.

We calculate \( \frac{(O - E)^2}{E} \) for each cell:

- For (Male, Product A):

  .. math::
     \frac{(O - E)^2}{E} = \frac{(40 - 38.57)^2}{38.57} = \frac{1.43^2}{38.57} \approx 0.053

- For (Male, Product B):

  .. math::
     \frac{(O - E)^2}{E} = \frac{(20 - 21.43)^2}{21.43} = \frac{1.43^2}{21.43} \approx 0.095

- For (Female, Product A):

  .. math::
     \frac{(O - E)^2}{E} = \frac{(50 - 51.43)^2}{51.43} = \frac{1.43^2}{51.43} \approx 0.040

- For (Female, Product B):

  .. math::
     \frac{(O - E)^2}{E} = \frac{(30 - 28.57)^2}{28.57} = \frac{1.43^2}{28.57} \approx 0.072

Adding these values together gives us the total Chi-Square statistic:

.. math::
   \chi^2 = 0.053 + 0.095 + 0.040 + 0.072 = 0.26

Degrees of Freedom
------------------

The degrees of freedom for a Chi-Square test of independence is:

.. math::
   \text{df} = (r - 1) \times (c - 1)

where \( r \) is the number of rows and \( c \) is the number of columns.

In our example:

.. math::
   \text{df} = (2 - 1) \times (2 - 1) = 1

Interpreting the Results
------------------------

To interpret the results, we compare the Chi-Square statistic to a critical value from the Chi-Square distribution with 1 degree of freedom at a 0.05 significance level.

Using a Chi-Square table:

- The critical value for \( \chi^2 \) with 1 degree of freedom at \( \alpha = 0.05 \) is 3.84.

Since our calculated \( \chi^2 = 0.26 \) is much less than 3.84, we do not reject the null hypothesis. This suggests there is no significant association between gender and product preference in this data.

.. admonition:: Important
   Always ensure that expected counts are sufficiently large (typically at least 5) for the Chi-Square test to be valid. If any expected count is less than 5, consider using Fisher's Exact Test instead.

.. warning::
   Interpreting results without considering the assumptions of the test can lead to misleading conclusions. Verify that the sample size is adequate and that the expected counts meet the minimum requirements.


When is it Okay to Perform a Chi-Square Test?
---------------------------------------------

Checking the assumptions is essential before performing a Chi-Square test:

- **For tables larger than 2x2**:

  - All cells should have an **expected** count of at least 1 **and**.

  - Less than 20% of cells should have **expected** counts under 5.

- **For a 2x2 table (smallest contingency table)**:

  - All cells must have an **expected** count of 5 or more.

Expected Count Formula
----------------------

The formula for the expected count in a contingency table is:

.. math::
   \text{Expected count} = \frac{\text{(Row total)} \times \text{(Column total)}}{\text{Overall total}}.

Intuition Behind the Formula
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- The expected count represents what we would expect to see in each cell of the contingency table if the two variables were **independent**.

- Independence means that the probability of one variable’s category does not depend on the other variable’s category.

Deriving the Formula
~~~~~~~~~~~~~~~~~~~~

Under the assumption of independence:

- Let the probability of observing category \( A_i \) be:

  .. math::
     P(A_i) = \frac{\text{Row total for } A_i}{n}.

- Let the probability of observing category \( B_j \) be:

  .. math::
     P(B_j) = \frac{\text{Column total for } B_j}{n}.

- If \( A \) and \( B \) are independent, then the joint probability is:

  .. math::
     P(A_i \cap B_j) = P(A_i) \times P(B_j).

- The expected count for cell \((i, j)\) is:

  .. math::
     \text{Expected count} = n \times P(A_i \cap B_j) = n \times \left(\frac{\text{Row total for } A_i}{n}\right) \times \left(\frac{\text{Column total for } B_j}{n}\right).

- Simplifying this gives:

  .. math::
     \text{Expected count} = \frac{(\text{Row total}) \times (\text{Column total})}{\text{Overall total}}.

Standardized Residual
---------------------

The standardized residual is given by:

.. math::
   Z = \frac{\text{Observed count} - \text{Expected count}}{\sqrt{\text{Expected count}}}.

Intuition Behind the Standardized Residual
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- The standardized residual measures how far the observed count is from the expected count, relative to the variability (standard deviation) of the count.

- If the observed and expected counts are close, the value of \( Z \) is small. Large values indicate a significant deviation.

Derivation Using the Central Limit Theorem
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For large sample sizes:

- The observed count \( O_{ij} \) can be approximated by a **Poisson** or **binomial** distribution, which is approximately normal due to the Central Limit Theorem.

- The variance of the observed count is approximately equal to the expected count:

  .. math::
     \text{Var}(O_{ij}) \approx E_{ij}.

- The standardized residual becomes:

  .. math::
     Z = \frac{O_{ij} - E_{ij}}{\sqrt{E_{ij}}}.

- Under the null hypothesis (independence), \( Z \) follows an approximate **standard normal distribution**, \( Z \sim N(0, 1) \).

Chi-Square Statistic
--------------------

The Chi-Square statistic aggregates the squared standardized residuals across all cells:

.. math::
   \chi^2 = \sum \frac{(O_{ij} - E_{ij})^2}{E_{ij}}.

Degrees of Freedom
~~~~~~~~~~~~~~~~~~

The degrees of freedom (DF) for the Chi-Square test are calculated as:

.. math::
   \text{DF} = (\text{number of rows} - 1) \times (\text{number of columns} - 1).

Interpreting the Chi-Square Statistic
-------------------------------------

- If the calculated \( \chi^2 \) value is close to zero, the observed counts are similar to the expected counts, supporting the null hypothesis of independence.

- If the calculated \( \chi^2 \) value is large, it suggests a significant deviation, providing evidence against the null hypothesis and indicating an association between the variables.

.. admonition:: Important
   Before using the Chi-Square test, ensure that the expected counts meet the necessary assumptions. If any expected count is less than 5, consider using an alternative test such as **Fisher’s Exact Test**.

.. warning::
   The Chi-Square test assumes a sufficiently large sample size. If the sample size is small, or if the expected counts are low, the results may not be reliable.


Week 13: Sample Proportions
===========================

The sample proportion (:math:`\hat{p}`) is used to estimate the population proportion (:math:`p`):

.. math::

   \hat{p} = \frac{X}{n}

where:

- :math:`X`: Count of successes in the sample.

- :math:`n`: Size of the sample.

.. warning::
   Be sure to distinguish between the count :math:`X` (an integer value) and the proportion :math:`\hat{p}` (a decimal value between 0 and 1).

Example 5.23: Shopping Online
-----------------------------

A survey reports that 60% of college students agree with a statement about online shopping satisfaction. Given a sample of 2500 students, the probability that the sample proportion is at least 58% can be found using software:

.. math::

   P(\hat{p} \geq 0.58) = 0.9802

Mean and Standard Deviation of Sample Proportion
------------------------------------------------

The mean (:math:`\mu_{\hat{p}}`) and standard deviation (:math:`\sigma_{\hat{p}}`) of a sample proportion are:

.. math::

   \mu_{\hat{p}} = p, \quad \sigma_{\hat{p}} = \sqrt{\frac{p(1-p)}{n}}

This formula is valid for binomial settings and provides a good approximation for large sample sizes.

**Example 5.24: Mean and Standard Deviation Calculation**

Given a sample proportion with :math:`p = 0.6` and :math:`n = 2500`:

.. math::

   \mu_{\hat{p}} = 0.6, \quad \sigma_{\hat{p}} = \sqrt{\frac{0.6 \times 0.4}{2500}} = 0.0098

**Explanation**:

The mean of :math:`\hat{p}` is unbiased, and the variability decreases as the sample size increases, following the formula :math:`\sqrt{p(1-p)/n}`.

.. _normal-approximation:

Normal Approximation for Counts and Proportions
-----------------------------------------------

Using simulations, it was observed that the sampling distribution of a sample proportion :math:`\hat{p}` is approximately Normal. The distribution of :math:`\hat{p}` can be expressed as the binomial count divided by the sample size :math:`n`. This aligns with the Central Limit Theorem.

The sum of independent random variables :math:`S_i` (taking the value 1 if a success occurs and 0 otherwise) can be represented as:

.. math::

    X = S_1 + S_2 + \cdots + S_n

The sample proportion :math:`\hat{p} = \frac{X}{n}` behaves like the sample mean and is approximately Normal when the sample size :math:`n` is large.

.. figure:: /images/1301.png
   :alt: Probability histogram of sample proportion
   :width: 70%

   Probability histogram of the sample proportion :math:`\hat{p}` based on a binomial distribution with :math:`n = 2500` and :math:`p = 0.6`.

Normal Approximation Formula
----------------------------

For large samples, the distributions of the count :math:`X` and the sample proportion :math:`\hat{p}` can be approximated as follows:

.. math::

    X \sim N\left(np, \sqrt{np(1-p)}\right)
   
    \hat{p} \sim N\left(p, \sqrt{\frac{p(1-p)}{n}}\right)

Rule of Thumb
-------------

Use the Normal approximation when:

.. math::

    np \geq 10 \quad \text{and} \quad n(1 - p) \geq 10

This ensures that both the count and the sample proportion have distributions close to Normal.

**Example: Normal Approximation vs. Exact Calculation**

We want to calculate :math:`P(\hat{p} \geq 0.58)` for a sample size of :math:`n = 2500` and a population proportion :math:`p = 0.6`. Using the Normal approximation:

.. math::

    \mu_{\hat{p}} = p = 0.6

    \sigma_{\hat{p}} = \sqrt{\frac{p(1-p)}{n}} = \sqrt{\frac{0.6 \times 0.4}{2500}} = 0.0098

    P(\hat{p} \geq 0.58) = P\left(\frac{\hat{p} - 0.6}{0.0098} \geq \frac{0.58 - 0.6}{0.0098}\right)

    = P(Z \geq -2.04) = 0.9793


The probability that :math:`\hat{p} \geq 0.58` is approximately 0.9793.

Conclusion
----------

The Normal approximation is very accurate for large samples. In this case, the approximation only differs from the exact software calculation (0.9802) by 0.0009.

.. admonition:: Important
   The Normal approximation is valid only when the sample size is large enough (i.e., when both \( np \) and \( n(1-p) \) are at least 10). For smaller samples, consider using the exact binomial distribution instead.

.. warning::
   Be cautious when interpreting results from the Normal approximation, especially with small sample sizes or when the sample proportion is close to 0 or 1, as this can lead to inaccurate estimates.

.. _computing_sample_size:

Necessary Sample Size
---------------------

When conducting a study to estimate a population parameter, we usually have an idea of the desired confidence level and the acceptable margin of error for our results. With these criteria defined, we can calculate the minimum sample size required to achieve this level of precision. By using algebra to solve for :math:n, we can determine the necessary sample size. Detailed explanations and examples are covered in Week 07.

.. important::

   **Calculating Sample Size for Estimating a Population Proportion**

   .. math::
      n = \left( \frac{z^*}{M} \right)^2 \, \tilde{p} (1 - \tilde{p})

   - :math:`M` is the margin of error.
   - :math:`\tilde{p}` is an estimated value of the proportion.

If we do not have an initial estimate for the population proportion, we use :math:\tilde{p} = 0.50. This choice is the most conservative because it maximizes the product :math:\tilde{p}(1 - \tilde{p}), leading to the largest possible sample size and ensuring adequate precision regardless of the true proportion.



Week 12: Multiple Regression
============================

Population Multiple Regression Equation
---------------------------------------

The simple linear regression model assumes that the mean of the response variable :math:`y` depends on the explanatory variable :math:`x` according to a linear equation:

.. math::
   \mu_y = \beta_0 + \beta_1 x

For any fixed value of :math:`x`, the response :math:`y` varies normally around this mean and has a standard deviation :math:`\sigma` that is the same for all values of :math:`x`.

In the multiple regression setting, the response variable :math:`y` depends on :math:`p` explanatory variables, denoted by :math:`x_1, x_2, \ldots, x_p`. The mean response depends on these explanatory variables according to a linear function:

.. math::
   \mu_y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \cdots + \beta_p x_p

Similar to simple linear regression, this expression is the *population regression equation*, and the observed values of :math:`y` vary about their means given by this equation.

Subpopulations and Variability
------------------------------

As in simple linear regression, this model can be understood in terms of *subpopulations* of responses. Each subpopulation corresponds to a particular set of values for all explanatory variables :math:`x_1, x_2, \ldots, x_p`. In each subpopulation, :math:`y` varies normally with a mean given by the population regression equation. The regression model assumes that the standard deviation :math:`\sigma` of the responses is the same in all subpopulations.

Example: Predicting Early Success in College
--------------------------------------------

This case study is based on data collected on science majors at a large university. The goal of the study was to develop a model to predict early university success. Success was measured using the cumulative grade point average (GPA) after three semesters. The explanatory variables were achievement scores at the time of enrollment, including average high school grades in mathematics (HSM), science (HSS), and English (HSE).

We use high school grades to predict the response variable GPA, with the following explanatory variables:

* :math:`x_1 = \text{HSM}`

* :math:`x_2 = \text{HSS}`

* :math:`x_3 = \text{HSE}`

These grades are coded on a scale from 1 to 10, defining various subpopulations. For example, the straight-C students are the subpopulation with :math:`\text{HSM} = 4`, :math:`\text{HSS} = 4`, and :math:`\text{HSE} = 4`.

The population multiple regression equation for the mean GPAs is:

.. math::
   \mu_{\text{GPA}} = \beta_0 + \beta_1 \text{HSM} + \beta_2 \text{HSS} + \beta_3 \text{HSE}

For the straight-C subpopulation of students, the equation gives the mean as:

.. math::
   \mu_{\text{GPA}} = \beta_0 + \beta_1 \cdot 4 + \beta_2 \cdot 4 + \beta_3 \cdot 4

Data for Multiple Regression
----------------------------

The data for a simple linear regression problem consist of :math:`n` pairs of a response variable :math:`y` and an explanatory variable :math:`x`. In multiple regression, where there are several explanatory variables, more elaborate notation is needed to describe the data. Each observation (or case) consists of a value for the response variable and for each of the explanatory variables. Let :math:`x_{ij}` represent the value of the :math:`j`th explanatory variable for the :math:`i`th case. The data are then represented as:

- **Case 1:** :math:`(y_1, x_{11}, x_{12}, \ldots, x_{1p})`

- **Case 2:** :math:`(y_2, x_{21}, x_{22}, \ldots, x_{2p})`

- **...**

- **Case n:** :math:`(y_n, x_{n1}, x_{n2}, \ldots, x_{np})`

Here, :math:`n` is the number of cases, and :math:`p` is the number of explanatory variables. Data are often entered into computer regression programs in this format, where each row corresponds to a case, and each column corresponds to a different variable.

Multiple Linear Regression Model
--------------------------------

Similar to simple linear regression, we combine the population regression equation and assumptions about how the observed values of :math:`y` vary around their means to construct the *multiple linear regression model*. The subpopulation means describe the **FIT** part of our conceptual model:

.. math::
   \text{DATA} = \text{FIT} + \text{RESIDUAL}

The **RESIDUAL** part represents the variation of observed :math:`y` about their means.

Residuals and Assumptions
-------------------------

We use the same notation for the residuals as in the simple linear regression model. The symbol :math:`\epsilon` represents the deviation of an individual observation from its subpopulation mean. These deviations are assumed to be:

- Normally distributed with mean 0.
- Have an unknown standard deviation :math:`\sigma`, which is the same for all values of the explanatory variables :math:`x`.

These conditions allow us to examine the residuals similarly to simple linear regression.

Multiple Linear Regression Model Equation
-----------------------------------------

The **multiple linear regression model** is given by:

.. math::
   y_i = \beta_0 + \beta_1 x_{i1} + \beta_2 x_{i2} + \cdots + \beta_p x_{ip} + \epsilon_i

for :math:`i = 1, 2, \ldots, n`.

The mean response :math:`\mu_y` is a linear function of the explanatory variables:

.. math::
   \mu_y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \cdots + \beta_p x_p

This is called the *population regression equation*.

The deviations :math:`\epsilon_i` are assumed to be independent and normally distributed with mean 0 and standard deviation :math:`\sigma`.

The parameters of the model are:

- Regression coefficients :math:`\beta_0, \beta_1, \beta_2, \ldots, \beta_p`

- Regression standard deviation :math:`\sigma`

Interpretation of Regression Coefficients
-----------------------------------------

The assumption that the subpopulation means are related to the regression coefficients :math:`\beta` implies that we can estimate *all* subpopulation means from these estimates, not just those associated with the cases. However, caution is necessary when interpreting the coefficients:

1. The :math:`\beta_0` coefficient represents the mean of :math:`y` when all :math:`x` variables are zero. This subpopulation is often not of interest.

2. The interpretation of each regression coefficient is similar to the slope in simple linear regression but only when *all other explanatory variables are held constant*. This is important because changes in one :math:`x` variable may influence others, affecting the overall change in :math:`y` in ways that one coefficient alone cannot describe.

.. image:: /images/1201.png

Estimation of the Multiple Regression Parameters
------------------------------------------------

Similar to simple linear regression, we use the method of *least squares* to obtain estimators of the regression coefficients :math:`\beta`. Let:

.. math::
   b_0, b_1, b_2, \ldots, b_p

denote the estimators of the parameters :math:`\beta_0, \beta_1, \beta_2, \ldots, \beta_p`.

For the :math:`i` th observation, the predicted response is:

.. math::
   \hat{y}_i = b_0 + b_1 x_{i1} + b_2 x_{i2} + \cdots + b_p x_{ip}

The :math:`i` th residual, the difference between the observed and predicted response, is:

.. math::
   e_i = \text{observed response} - \text{predicted response} 

   = y_i - \hat{y}_i = y_i - (b_0 + b_1 x_{i1} + b_2 x_{i2} + \cdots + b_p x_{ip})

Least Squares Criterion
-----------------------

The method of least squares chooses the values of the :math:`b`'s that minimize the sum of squared residuals. In other words, the parameter estimates :math:`b_0, b_1, b_2, \ldots, b_p` minimize the quantity:

.. math::
   \sum (y_i - b_0 - b_1 x_{i1} - b_2 x_{i2} - \cdots - b_p x_{ip})^2

.. warning::
   The formula for the least-squares estimates in multiple regression is complicated. We focus on understanding the principle and rely on software for the computations.

Estimating Variability
----------------------

The parameter :math:`\sigma^2` measures the variability of the responses about the population regression equation. Like in simple linear regression, we estimate :math:`\sigma^2` by averaging the squared residuals. The estimator is:

.. math::
   s^2 = \frac{\sum e_i^2}{n - p - 1} = \frac{\sum (y_i - \hat{y}_i)^2}{n - p - 1}

where :math:`n - p - 1` represents the **degrees of freedom**. The degrees of freedom are calculated as the sample size :math:`n`, minus :math:`(p + 1)`, which accounts for the number of :math:`\beta` parameters estimated in the model. In simple linear regression (where :math:`p = 1`), the degrees of freedom are :math:`n - 2`.

To estimate the regression standard deviation :math:`\sigma`, we use:

.. math::
   s = \sqrt{s^2}

.. image:: /images/1202.png

Confidence Intervals and Significance Tests for Regression Coefficients
-----------------------------------------------------------------------

We can obtain confidence intervals and perform significance tests for each of the regression coefficients :math:`\beta_j` as in simple linear regression. The standard errors of the estimates :math:`b_j` have more complex formulas, but they are all multiples of the estimated model standard deviation :math:`s`. We rely on statistical software to perform these calculations.

.. warning::
   Be cautious when interpreting the t-tests and confidence intervals for individual regression coefficients.

   In simple linear regression, the model states that:

   .. math::
      \mu_y = \beta_0 + \beta_1 x.

   The null hypothesis :math:`H_0: \beta_1 = 0` suggests that the explanatory variable :math:`x` has no predictive value for the response :math:`y`, meaning there is no linear relationship between :math:`x` and :math:`y`.

   In multiple regression, the null hypothesis for a coefficient, such as :math:`H_0: \beta_1 = 0`, indicates that :math:`x_1` provides no additional predictive information about :math:`y` beyond what is already accounted for by the other explanatory variables :math:`x_2, x_3, \ldots, x_p`. This distinction reflects the conditional contribution of each predictor when others are included in the model.

.. image:: /images/1203.png

Confidence Intervals for Mean Response and Prediction
-----------------------------------------------------

Regression is often used for prediction, and multiple regression models can construct confidence intervals for a mean response and prediction intervals for a future observation. The fundamental principles are similar to those in simple linear regression.

In most software, the same commands that generate confidence and prediction intervals for simple linear regression apply to multiple regression. The difference is that, in multiple regression, we specify a list of explanatory variables instead of a single variable, allowing software to handle complex calculations efficiently.

ANOVA Table for Multiple Regression
-----------------------------------

In simple linear regression, the :math:`F` test from the ANOVA table is equivalent to the two-sided :math:`t` test for the hypothesis that the slope of the regression line is zero. For multiple regression, the ANOVA :math:`F` test evaluates the hypothesis that all the regression coefficients (except the intercept) are zero. Here is the general form of the ANOVA table for multiple regression:

.. list-table:: ANOVA Table for Multiple Regression
   :header-rows: 1

   * - Source
     - Degrees of Freedom
     - Sum of Squares
     - Mean Square
     - :math:`F`
   * - Model
     - :math:`p`
     - :math:`\sum (\hat{y}_i - \bar{y})^2`
     - :math:`\text{SSM} / \text{DFM}`
     - :math:`\text{MSM} / \text{MSE}`
   * - Error
     - :math:`n - p - 1`
     - :math:`\sum (y_i - \hat{y}_i)^2`
     - :math:`\text{SSE} / \text{DFE}`
     -
   * - Total
     - :math:`n - 1`
     - :math:`\sum (y_i - \bar{y})^2`
     -
     -

where:

- :math:`SST = SSM + SSE`

- :math:`DFT = DFM + DFE`

The estimate of the variance :math:`\sigma^2` is given by :math:`\text{MSE}`, the mean square error in the ANOVA table. The ratio :math:`\text{MSM} / \text{MSE}` is the :math:`F` statistic for testing the null hypothesis:

.. math::
   H_0: \beta_1 = \beta_2 = \cdots = \beta_p = 0

against the alternative hypothesis:

.. math::
   H_a: \text{at least one of the } \beta_j \text{ is not zero.}

The null hypothesis indicates that none of the explanatory variables predict the response variable, while the alternative suggests that at least one explanatory variable is a predictor.

The :math:`F` statistic has an :math:`F(p, n - p - 1)` distribution under :math:`H_0`. Large values of :math:`F` indicate evidence against :math:`H_0`.

.. image:: /images/1204.png

.. warning::
   A common error in multiple regression analysis is assuming that all regression coefficients are statistically different from zero whenever the :math:`F` statistic is significant. Remember, the :math:`F` test assesses the overall model's significance, while individual :math:`t` tests evaluate each variable's contribution, accounting for the presence of other variables.

   The :math:`F` test handles collinearity better than individual :math:`t` tests, especially when two or more explanatory variables are highly correlated.

Squared Multiple Correlation :math:`R^2`
----------------------------------------

In simple linear regression, the square of the sample correlation can be written as the ratio of the sum of squares for the model (SSM) to the total sum of squares (SST). This ratio represents the proportion of variation in :math:`y` explained by :math:`x`. In multiple regression, the ratio :math:`\text{SSM} / \text{SST}` represents the proportion of explained variation in :math:`y`, now relating to the collection of explanatory variables in the model.

.. admonition:: Squared multiple correlation

   **The statistic**

   .. math::
      R^2 = \frac{\text{SSM}}{\text{SST}} = \frac{\sum (\hat{y}_i - \bar{y})^2}{\sum (y_i - \bar{y})^2}

   :math:`R^2` is the proportion of the variation in the response variable :math:`y` that is explained by the explanatory variables :math:`x_1, x_2, \ldots, x_p` in a multiple linear regression.

The capital letter :math:`R` indicates that this statistic depends on a collection of explanatory variables. Often, :math:`R^2` is multiplied by 100 and expressed as a percentage. The square root of :math:`R^2`, called the *multiple correlation coefficient*, represents the correlation between the observations :math:`y_i` and the predicted values :math:`\hat{y}_i`. Some software provides a scatterplot of this relationship to help visualize the model's predictive strength.

.. image:: /images/1205.png

11.2: A Case Study
===================

Regression on High School Grades
-------------------------------

To explore the relationship between explanatory variables and the response variable GPA, several multiple regression models are run. The explanatory variables fall into three categories:
- **High School Grades**: HSM (Math), HSS (Science), HSE (English)

- **Standardized Test Scores**: Three SAT scores (Math, Critical Reading, Writing)

- **Sex**: Represented by the variable `SEX`

The first model uses only high school grades to predict GPA.

**ANOVA Output**
- The ANOVA table and parameter estimates are obtained with 150 cases.

- **Degrees of Freedom**:

  - Model (DFM): :math:`p = 3`

  - Error (DFE): :math:`n - p - 1 = 150 - 3 - 1 = 146`

  - Total (DFT): :math:`n - 1 = 149`

**F-Test Results**
- The ANOVA :math:`F` statistic is 14.35, with a very small :math:`P`-value (<0.0001), indicating the model is significant.

- Null hypothesis: :math:`H_0: \beta_1 = \beta_2 = \beta_3 = 0`.

- Given the :math:`F(3, 146)` distribution, this :math:`F` value strongly suggests that at least one of the regression coefficients for high school grades differs from zero.

**Model Fit Statistics**
- **Root MSE**: 0.726, an estimate of the standard deviation :math:`\sigma` of GPA about the regression line.

- :math:`R^2`: 0.23, meaning 23% of the variation in GPA is explained by high school grades.

**Regression Equation**
- The fitted regression equation is:
 
  .. math::
     \hat{\text{GPA}} = 0.069 + 0.123\text{HSM} + 0.136\text{HSS} + 0.058\text{HSE}

- Example prediction:

  - For a student with HSM = 9, HSS = 8, and HSE = 7, the predicted GPA is:
   
    .. math::
       \hat{\text{GPA}} = 0.069 + 0.123(9) + 0.136(8) + 0.058(7) = 2.67

**Significance of Individual Predictors**

- **HSM** is significant (p = 0.0262), meaning high school math grade has a unique predictive contribution to GPA.

- **HSS** and **HSE** are not significant at the 0.05 level, suggesting they do not independently predict GPA when HSM is in the model.

Interpretation of Results
-------------------------

The significance tests for individual regression coefficients may appear contradictory to initial correlation analysis.

**Key Observations**

- **Correlation Analysis**:

  - GPA correlations with HSS and HSE are 0.44 and 0.36, respectively, both with p < 0.0005.

  - Using HSS or HSE alone could yield significant regression coefficients.

**Multicollinearity**

- **Collinearity**: High correlation among explanatory variables, particularly HSM, HSS, and HSE, leads to **multicollinearity**.

  - Correlation coefficients:

    - HSM and HSS: 0.67

    - HSM and HSE: 0.49

- Multicollinearity can obscure individual predictors’ contributions due to shared predictive information among correlated variables.

**Implications of Multicollinearity**

- Each predictor’s significance depends on the other predictors in the model.

- Including HSM with HSS and HSE reduces the individual significance of HSS and HSE.

- Despite not being significant alone, HSS and HSE together may add value to the model, but determining their exact contribution requires further analysis.

**Summary**

- Multicollinearity is a major challenge in multiple regression, complicating interpretation of individual coefficients. HSM remains the most significant predictor of GPA when considered alongside other high school grades.

Mean of Response and Adjusted :math:`R^2`
-----------------------------------------

**Mean of Response**

The *Mean of Response* is the average value of the dependent (response) variable, :math:`y`, across all observations in the dataset.

- It serves as a baseline for understanding the central tendency of the response variable.

- For example, if GPA is the response variable, the mean of response would be the average GPA of all students in the dataset.

- In regression analysis, the model’s goal is to explain or predict the variability around this mean. The mean of the response is sometimes used as a benchmark for interpreting the model’s :math:`R^2`, as :math:`R^2` indicates how much of the variation around this mean is explained by the model.

**Adjusted** :math:`R^2` (:math:`R^2_{\text{adj}}`)

*Adjusted* :math:`R^2`, denoted :math:`R^2_{\text{adj}}`, is a modified version of the regular :math:`R^2` (coefficient of determination) that accounts for the number of predictors in the model.

- **Standard** :math:`R^2` measures the proportion of variance in the response variable that is explained by the model. It ranges from 0 to 1, with higher values indicating better model fit. However, :math:`R^2` tends to increase as more predictors are added to the model, even if those predictors are not actually useful.
 
- **Adjusted** :math:`R^2` adjusts for the number of predictors and the sample size, providing a more accurate measure of model fit when multiple predictors are included. It’s calculated as follows:

  .. math::
      R^2_{\text{adj}} = 1 - \left( \frac{(1 - R^2)(n - 1)}{n - p - 1} \right)

  where:
 
  - :math:`n` = number of observations

  - :math:`p` = number of predictors (excluding the intercept)

- **Why Use Adjusted** :math:`R^2`?
 
  - Adjusted :math:`R^2` increases only if the new predictor improves the model fit more than would be expected by chance.

  - It penalizes the addition of unnecessary predictors, making it useful for model selection when comparing models with different numbers of predictors.
 
- **Interpretation**: A higher :math:`R^2_{\text{adj}}` indicates a better balance between model complexity and explanatory power, whereas an increase in standard :math:`R^2` without an increase in adjusted :math:`R^2` suggests that the additional predictors may not be meaningful.

**Summary**

- *Mean of Response* provides the average value of the response variable, giving a central value around which the model tries to explain variance.

- *Adjusted* :math:`R^2` offers a refined measure of model fit that accounts for the number of predictors, providing a more reliable metric for comparing models, especially in multiple regression.

Model Selection
---------------

When a model contains a large number of insignificant variables, it is common to refine the model through a process called *model selection*. We generally prefer smaller models over larger ones because they are easier to interpret and work with. However, multiple regression can be complex, and there is no universal "best" approach to refine a model. Additionally, there is no guarantee that only one acceptable refined model exists.

**Statistical Software for Model Selection**

Many statistical software packages can summarize all possible models from a set of :math:`p` variables. This capability allows for reducing the number of candidate models. For example, if there are 6 variables (:math:`p = 6`), the total number of possible models is 63. By examining a list of possible models, we can identify the best or a set of best models to consider further. Consulting an expert is recommended if in doubt.

For instance, the output of model selection software might show the two best models in terms of highest :math:`R^2` values for models with different numbers of predictors (from :math:`p = 1` to :math:`p = 6`). Such lists help reduce the number of models to review. If the :math:`R^2` values show little difference once the model includes at least three explanatory variables, we may focus on models with :math:`p = 3` or :math:`p = 4`.

**Adjusted** :math:`R^2`

Another approach to model selection involves choosing models based on *Adjusted :math:`R^2`* or *Mean Squared Error (MSE)*. Finding a model that minimizes MSE or maximizes adjusted :math:`R^2` penalizes larger models, thus favoring more parsimonious options.

Adjusted :math:`R^2` differs from regular :math:`R^2` by taking into account the number of parameters in the model. In an example list from software, the models with :math:`p = 3` and :math:`p = 4` have the two smallest MSEs, making them the best refined models according to this criterion.

**Summary**

- Model selection is essential in regression analysis to refine models and improve interpretability.

- Software can provide summaries of potential models, helping to reduce the number of candidate models.

- Both adjusted :math:`R^2` and MSE are useful metrics in model selection, as they account for model complexity.

Multiple Logistic Regression
----------------------------

Many studies involve yes/no or success/failure response variables. For instance, a surgery patient either lives or dies; a consumer either does or does not purchase a product after seeing an advertisement. In multiple regression, the response variable is typically assumed to follow a Normal distribution, making standard regression unsuitable for predicting binary outcomes. However, models like *logistic regression* apply the ideas of regression to response variables with only two possible outcomes.

**Logistic Regression**

*Logistic regression* is a model that applies to binary outcome variables by using one or more explanatory variables to explain the probability of success. This model is based on a binomial framework. Although logistic regression is more complex than multiple linear regression, the fundamental ideas remain similar. The details of multiple logistic regression are further explained in Chapter 14.

**Example: Tipping Behavior in Canada**

The Consumer Report on Eating Share Trends (CREST) dataset includes data on away-from-home food purchases by approximately 4000 households across Canada per quarter. From this dataset of 73,822 observations, researchers created “high” and “low” tipping variables:

- **High Tip**: Defined as tip rates above 20%.

- **Low Tip**: Defined as tip rates below 10%.

Logistic regression was used to identify explanatory variables associated with either high or low tips. The model included over 25 explanatory variables, categorized as either “control” variables or “stereotype-related” variables. Examples of stereotype-related variables include:

- :math:`x_1`: A variable equal to 1 if the diner was older than 65, 0 otherwise.

- :math:`x_2`: Equal to 1 if the meal occurred on a Sunday, 0 otherwise.

- :math:`x_3`: Equal to 1 if English was the diner’s second language, 0 otherwise.

- :math:`x_4`: Equal to 1 if the diner was a French-speaking Canadian, 0 otherwise.

- :math:`x_5`: Equal to 1 if alcoholic drinks were served with the meal, 0 otherwise.

- :math:`x_6`: Equal to 1 if the meal involved a lone male, 0 otherwise.

**Chi-Square Test**

In logistic regression, a chi-square test is used to test the null hypothesis that *all* coefficients of the explanatory variables are zero, similar to the :math:`F` test in multiple regression. Individual coefficients are tested using chi-square tests with 1 degree of freedom to assess whether they are significantly different from zero. In this example, most variables in the model had p-values below 0.01, indicating significance.

**Logistic Regression Model for High Tips**

The logistic regression model for predicting high tips using stereotype-related variables is expressed as:

.. math::
   \log\left(\frac{p}{1 - p}\right) = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \cdots + \beta_6 x_6

where :math:`p` is the probability of a high tip. The interpretation of coefficients in logistic regression can be challenging due to the logarithmic transformation, but each coefficient represents the effect of a predictor on the log odds of the outcome.

Chi-Square Test in Multiple Logistic Regression
----------------------------------------------

In multiple logistic regression, the chi-square test is used to test whether the coefficients of the explanatory variables are significantly different from zero. This helps determine if the predictors contribute meaningfully to the model.

The chi-square test in logistic regression can be used in two main ways:

1. **Overall Model Test**: Tests the null hypothesis that *all* coefficients are zero, meaning none of the predictors have a statistically significant relationship with the response variable.

2. **Individual Coefficient Test**: Tests each predictor’s coefficient to assess whether individual variables contribute to the model.

**Steps to Conduct the Chi-Square Test**

1. **Set Up Hypotheses**:

   - **Overall Test**:

     - Null Hypothesis (:math:`H_0`): All coefficients, except the intercept, are equal to zero. Mathematically, :math:`\beta_1 = \beta_2 = \cdots = \beta_k = 0`.

     - Alternative Hypothesis (:math:`H_a`): At least one coefficient is not zero, indicating that at least one predictor contributes to the model.

   - **Individual Test** (for each coefficient :math:`\beta_j`):

     - Null Hypothesis (:math:`H_0`): :math:`\beta_j = 0`, meaning the predictor has no effect on the log-odds of the outcome.

     - Alternative Hypothesis (:math:`H_a`): :math:`\beta_j \neq 0`, meaning the predictor significantly affects the log-odds.

2. **Calculate the Test Statistic**:

   - The chi-square test statistic for the overall model is based on the *likelihood-ratio test*. This statistic is calculated as:

     .. math::
        \chi^2 = -2 \left( \text{log-likelihood of the null model} - \text{log-likelihood of the fitted model} \right)

   - **Null Model**: The model without any predictors (only the intercept).

   - **Fitted Model**: The full logistic regression model with all predictors included.

   - For each individual coefficient, the chi-square statistic with 1 degree of freedom is used. This value can be obtained directly from the logistic regression output in most statistical software.

3. **Determine Degrees of Freedom**:

   - For the overall test, the degrees of freedom are equal to the number of predictors, :math:`p`.

   - For individual tests, the degrees of freedom are 1, as each test is evaluating a single coefficient.

4. **Find the p-value**:

   - Compare the calculated chi-square statistic to a chi-square distribution with the appropriate degrees of freedom to find the p-value.

   - If the p-value is less than the significance level (typically 0.05), reject the null hypothesis.

5. **Interpret Results**:

   - **Overall Test**:

     - A significant result (small p-value) indicates that the model with predictors fits significantly better than the null model, meaning that at least one predictor is important.

   - **Individual Test**:

     - A significant p-value for a predictor’s chi-square statistic indicates that the predictor contributes to the model, suggesting it affects the log-odds of the outcome variable.

**Example: Applying the Chi-Square Test in Logistic Regression**

- In the tipping behavior study, suppose we want to test whether the predictors (e.g., age over 65, meal on Sunday) are associated with high tipping.

- The overall chi-square test assesses if any of the stereotype-related variables contribute to predicting high tips.

- Each individual chi-square test evaluates if a specific variable, like whether the diner was alone, is statistically significant in predicting high tips.

**Software Note**

Most statistical software, such as R, SAS, and SPSS, provides the chi-square statistics and p-values directly in the output for logistic regression. For example:

- In R, the `anova()` function can be used on a logistic model to perform the chi-square test.

- In SAS, the `Wald Chi-Square` values are given in the regression output.

By using these steps and software tools, you can conduct chi-square tests to evaluate the overall significance of the logistic regression model and the contribution of each predictor.




Week 11: Ch2 & Ch10 Correlation and Simple Linear Regression
============================================================

Introduction
------------

In Chapter 2, Section 2, we learned about scatter plots, which visually depict the relationship between two variables. Curiosity drives us to explore these relationships, but there are also practical motivations:

- Understanding relationships between variables helps uncover patterns, trends, and mechanisms in the real world.
- Knowing how one variable influences another enables us to forecast the future and make informed decisions.
- Identifying whether one variable causes changes in another is essential for scientific discovery, policy-making, and medical research.

Starting with Two Variables
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. image:: /images/1101.png
.. image:: /images/1102.png

Scatter plots give us clues about the strength and direction of the relationship between two variables. However, visualization alone is not enough. To quantify the relationship, we use **correlation**, a numerical summary of the linear relationship between variables.

Correlation: A Numerical Summary of Linear Relationship
-------------------------------------------------------

Correlation measures the strength and direction of the linear relationship between two variables.

.. image:: /images/1103.png

Why focus on linear relationships, and why is this important?

- A linear relationship between two variables is the simplest way to describe how one variable changes with respect to the other.
- Many natural and economic processes exhibit approximately linear relationships over specific ranges.
- Linear models, such as linear regression, serve as the foundation for many statistical and machine learning methods.

.. image:: /images/1104.png
.. image:: /images/1105.png

The Pearson Correlation Coefficient
-----------------------------------

The Pearson correlation coefficient measures **linear relationships**. Let's explore why it is specifically designed for such relationships.

### Pearson’s Correlation Coefficient Formula

The Pearson correlation coefficient :math:`r` between two variables :math:`X` and :math:`Y` is defined as:

.. math::

    r = \frac{\sum_{i=1}^{n} (X_i - \bar{X})(Y_i - \bar{Y})}
             {\sqrt{\sum_{i=1}^{n} (X_i - \bar{X})^2
                    \sum_{i=1}^{n} (Y_i - \bar{Y})^2}}

where:

- :math:`X_i` and :math:`Y_i` are the individual data points.

- :math:`\bar{X}` and :math:`\bar{Y}` represent the means of the variables :math:`X` and :math:`Y`.

- :math:`n` is the sample size.

The formula essentially **standardizes the covariance** between the variables :math:`X` and :math:`Y`.

Step-by-Step Intuition of Pearson’s :math:`r`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

### Covariance between X and Y

The numerator, :math:`\sum (X_i - \bar{X})(Y_i - \bar{Y})`, measures how much the two variables vary **together**.

- If both :math:`X` and :math:`Y` increase or decrease simultaneously, the **covariance** is positive and large.
- If one increases while the other decreases, the **covariance** becomes negative.

### Normalization

The denominator ensures that the **correlation coefficient** :math:`r` lies between -1 and 1 by dividing the covariance by the standard deviations of :math:`X` and :math:`Y`. This makes the result **unitless**.

### Linear Nature

The formula captures only **linear relationships** because it focuses on products of deviations from the mean: :math:`(X_i - \bar{X})(Y_i - \bar{Y})`.

- If the relationship is **non-linear**, the product of deviations may not consistently align in one direction.
- Consequently, positive and negative contributions might cancel each other out, yielding a correlation close to 0 even if a non-linear relationship exists.

Interpreting Correlation from a Scatter Plot
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. list-table:: Interpreting Correlation from a Scatter Plot
   :widths: 15 40 45
   :header-rows: 1

   * - Value of r
     - Pattern in Scatter Plot
     - Description
   * - r = 1
     - All points lie perfectly on a straight line sloping upward
     - Perfect positive correlation
   * - 0 < r < 1
     - Points scattered around an upward-sloping line
     - Positive correlation (weaker as r approaches 0)
   * - r = 0
     - No discernible pattern, random scatter
     - No linear relationship
   * - -1 < r < 0
     - Points scattered around a downward-sloping line
     - Negative correlation (weaker as r approaches 0)
   * - r = -1
     - All points lie perfectly on a straight line sloping downward
     - Perfect negative correlation

Simple Linear Regression: Zooming into Scatter Plots
----------------------------------------------------

Correlation is only the beginning. By zooming in on scatter plots, we can uncover more through **simple linear regression**.

Analyzing Data Points
~~~~~~~~~~~~~~~~~~~~~

When scatter plots contain numerous data points, it becomes challenging to discern relationships clearly. For each value on the x-axis, we focus on the corresponding data points with the same x-value, treating them as a **subpopulation**. By calculating the **means** of these points, we can better understand the relationship.

.. image:: /images/1106.png

Summarizing with a Line
~~~~~~~~~~~~~~~~~~~~~~~

A line summarizes the **linear relationship** of the conditional mean of the data points. Linear regression goes beyond correlation by providing a **predictive equation** in the original units of the variables. While correlation measures **association**, linear regression focuses on **prediction** and quantifying the effect of one variable (X) on another (Y).

Exploring Lines in Scatter Plots
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

We can draw various lines to explore the relationship.

.. image:: /images/1107.png

1. First, a simple straight line:

.. image:: /images/1108.png

2. Next, we examine the distances between data points and the line to find a **special line** that minimizes these distances:

.. image:: /images/1109.png

3. Additional:

.. image:: /images/1110.png

.. image:: /images/1111.png

.. image:: /images/1112.png

Interpreting the Slope Coefficient Formula
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- :math:`r`: The correlation coefficient measures the **strength and direction** of the linear relationship between :math:`X` and :math:`Y`.

- :math:`\frac{s_y}{s_x}`: This ratio of the standard deviations of :math:`Y` and :math:`X` accounts for the **units** of the variables, ensuring the slope reflects how much :math:`Y` changes for a one-unit change in :math:`X`.

Understanding :math:`R^2` and Its Relationship to Correlation
-------------------------------------------------------------

1. **What is** :math:`R^2`?

:math:`R^2` is the **coefficient of determination**, measuring how well the regression line fits the data. It quantifies the proportion of the variance in the dependent variable :math:`Y` explained by the independent variable(s) :math:`X`.

The formula for :math:`R^2` is:

.. math::

    R^2 = \frac{\sum (\hat{y} - \bar{y})^2}{\sum (y - \bar{y})^2}

where:

- :math:`\bar{y}` is the mean of the observed values of :math:`Y`.
- :math:`\hat{y}` is the predicted value of :math:`Y` from the regression model.
- :math:`y` is the observed value of :math:`Y`.

The formula compares:

- **Total variance** in :math:`Y`: :math:`\sum (y - \bar{y})^2`
- **Explained variance** by the regression model: :math:`\sum (\hat{y} - \bar{y})^2`

:math:`R^2` represents the fraction of total variance explained by the model.

2. **Intuition of the Ratio**

Without a predictor, the **total variation** in :math:`Y` is:

.. math::

    \sum (y - \bar{y})^2

This measures how much data points deviate from the mean.

With a predictor :math:`X`, the model generates predictions :math:`\hat{y}` that capture the variation in :math:`Y` explained by :math:`X`:

.. math::

    \sum (\hat{y} - \bar{y})^2

The ratio measures how much better the regression model performs compared to using the mean alone:

.. math::

    R^2 = \frac{\text{Explained Variation}}{\text{Total Variation}} = \frac{\sum (\hat{y} - \bar{y})^2}{\sum (y - \bar{y})^2}

3. **Relationship Between** :math:`R^2` **and Correlation** :math:`r`

In **simple linear regression** with one predictor, :math:`R^2` equals the **square of the Pearson correlation coefficient** :math:`r`:

.. math::

    R^2 = r^2

This shows how much of the variation in :math:`Y` is explained by the linear relationship with :math:`X`.

4. **Range of** :math:`R^2`

- **Typical Range:** :math:`0 \leq R^2 \leq 1`

  - :math:`R^2 = 0`: The model explains none of the variability in :math:`Y`.

  - :math:`R^2 = 1`: The model explains all the variability in :math:`Y`.

- **Can** :math:`R^2` **be negative?**  

  Yes. When the model performs worse than simply using the mean of :math:`Y` for predictions, the **residual sum of squares** exceeds the **total sum of squares**, resulting in a negative :math:`R^2`.

  **Intuition of Negative** :math:`R^2`:

  A negative :math:`R^2` suggests a poor fit, worse than using the mean as the prediction for all observations.

- **Can** :math:`R^2` **exceed 1?**

  In properly defined least-squares regression, :math:`R^2` cannot exceed 1. However, in cases of **non-linear models** or **overfitting**, values greater than 1 can occur, signaling potential issues with the model or metric usage.

.. image:: /images/1113.png

Key Differences Between Linear Regression and Correlation
---------------------------------------------------------

.. list-table::
   :widths: 20 40 40
   :header-rows: 1

   * - **Aspect**
     - **Correlation**
     - **Linear Regression**
   * - **What it Measures**
     - Strength and direction of a linear relationship between two variables.
     - How changes in the independent variable affect the dependent variable.
   * - **Symmetry**
     - Symmetric: :math:`r(X, Y) = r(Y, X)`.
     - Asymmetric: Predicts :math:`Y` from :math:`X`.
   * - **Equation Involved**
     - Pearson’s :math:`r` (a unitless measure).
     - Regression line: :math:`Y = \beta_0 + \beta_1 X + \varepsilon`.
   * - **Units**
     - Unit-free (standardized).
     - Keeps the original units of :math:`X` and :math:`Y`.
   * - **Goal**
     - Measures association.
     - Provides a predictive equation and quantifies the effect of :math:`X` on :math:`Y`.
   * - **Interpretation**
     - Descriptive: How well the two variables move together.
     - Predictive: How much :math:`Y` changes, on average, with a 1-unit change in :math:`X`.

**Association does not mean causation**

Simple Linear Regression
------------------------

### Model Intuition

Looking closely at the initial plot, we see that fixing the x-values results in data points that form distributions around their mean. This spread around the mean suggests that we need a parameter :math:`\sigma` to model this variability.

.. image:: /images/1114.png

### Simple Linear Regression Model

1. **Model Assumptions**:

   - For each value of the explanatory variable :math:`x`, the response variable :math:`y` is **normally distributed** with a mean that depends on :math:`x`.

   - The **mean of the response** is represented by :math:`\mu_y`. In simple linear regression, these means form a **straight line** when plotted against :math:`x`.

2. **Linear Model Components**:

   - **Mean Response Line**:

     .. math::

        \mu_y = \beta_0 + \beta_1 x

     This equation represents the **population regression line**, indicating how the mean response :math:`\mu_y` changes with :math:`x`.

   - **Distribution Around the Mean**:

     - For each subpopulation defined by :math:`x`, the response values :math:`y` are normally distributed around the mean response :math:`\mu_y`.

     - The spread around the mean is measured by the **standard deviation** :math:`\sigma`, which remains constant across all values of :math:`x`.

3. **Visualization Explanation**:

   - The figure displays several **Normal distributions** for different values of :math:`x`.

   - Each curve is centered at the corresponding **mean response** :math:`\mu_y` for the given :math:`x`.

   - All curves have the **same spread**, measured by the standard deviation :math:`\sigma`.

Statistical Model for Linear Regression
---------------------------------------

1. **Model Assumptions**:

   - The response variable (e.g., BMI) follows a **normal distribution** with a mean that changes **linearly** with the explanatory variable :math:`x`:

     .. math::

        \mu_y = \beta_0 + \beta_1 x

   - This equation represents the **population regression line**, showing the expected response (e.g., average BMI) for a given value of :math:`x`.

2. **Data = Fit + Residual**:

   - The linear regression model decomposes the data as:

     .. math::

        \text{DATA} = \text{FIT} + \text{RESIDUAL}

   - **FIT**: Represents the predicted mean response, :math:`\beta_0 + \beta_1 x`.

   - **RESIDUAL**: Represents the random deviations from the mean, captured by :math:`\varepsilon`.

3. **Residuals/Error**:

   - Residuals :math:`\varepsilon_i` account for unexplained variability in the response variable.

   - Key assumptions about residuals:

     - Residuals are **independent**.

     - They follow a **normal distribution** with mean 0 and standard deviation :math:`\sigma`.

4. **Linear Regression Model**:

   - For each observation :math:`(x_i, y_i)`, the relationship is expressed as:

     .. math::

        y_i = \beta_0 + \beta_1 x_i + \varepsilon_i

   - **Parameters**:

     - **Intercept**: :math:`\beta_0`

     - **Slope**: :math:`\beta_1`

     - **Standard deviation of residuals**: :math:`\sigma`

.. image:: /images/1115.png

Estimating the Standard Deviation of Residuals (:math:`\sigma`)
---------------------------------------------------------------

1. **What is :math:`\sigma`?**

   - :math:`\sigma` measures the **spread of the response variable** :math:`y` around the population regression line.

   - It represents the **standard deviation of the residuals** :math:`\varepsilon_i`.

   - Since residuals are not directly observable, we estimate :math:`\sigma` using the residuals :math:`e_i`.

2. **Definition of Residuals**:

   - For the :math:`i`-th observation, the residual :math:`e_i` is:

     .. math::

        e_i = y_i - \hat{y}_i = y_i - (b_0 + b_1 x_i)

3. **Using Residuals to Estimate Model Deviations**:

   - Residuals :math:`e_i` estimate the deviations :math:`\varepsilon_i`.

   - The sum of residuals is 0, and they are assumed to have a mean of 0.

4. **Estimating Variance and Standard Deviation**:

   - The variance :math:`\sigma^2` is estimated by averaging the squared residuals, divided by :math:`n - 2` degrees of freedom:

     .. math::

        s^2 = \frac{\sum e_i^2}{n - 2} = \frac{\sum (y_i - \hat{y}_i)^2}{n - 2}

   - Dividing by :math:`n - 2` ensures the estimate is **unbiased**.

5. **Model Standard Deviation (Regression Standard Error)**:

   - The regression standard error :math:`s` is:

     .. math::

        s = \sqrt{s^2}

.. image:: /images/1116.png

.. image:: /images/1117.png

Confidence Intervals and Significance Tests
-------------------------------------------

.. image:: /images/1118.png

Confidence Intervals and Hypothesis Tests for Intercept
-------------------------------------------------------

1. **Confidence Intervals and Significance Tests for the Intercept**:

   - Confidence intervals and significance tests for the **intercept** :math:`\beta_0` are computed similarly to those for the slope :math:`\beta_1`, but with :math:`b_0` and :math:`SE_{b_0}` replacing :math:`b_1` and :math:`SE_{b_1}`.

   - Testing the hypothesis :math:`H_0: \beta_0 = 0` is often **not practically useful** since the intercept represents the **mean response when** :math:`x = 0`.

   - In many cases, the subpopulation where :math:`x = 0` may not exist or be relevant to the study.

2. **Interpretation of the Intercept**:

   - The intercept :math:`\beta_0` represents the **mean response** when the explanatory variable :math:`x` equals 0.

   - In some contexts, such as studies on physical activity, the intercept may provide meaningful insights. In others, it might not hold practical value.

3. **Testing the Slope**:

   - The hypothesis test :math:`H_0: \beta_1 = 0` is generally more useful.

   - If the hypothesis is true, the slope term :math:`\beta_1` drops out, leaving:

     .. math::

        \mu_y = \beta_0

   - This indicates that the **mean of** :math:`y` does **not vary with** :math:`x`, meaning there is no **linear relationship** between the two variables.

4. **Key Insight**:

   - If :math:`H_0: \beta_1 = 0` is true, the regression model provides **no meaningful predictive value** for :math:`y`. There would be no significant relationship between the predictor :math:`x` and the response :math:`y`.

Confidence Intervals and Prediction Intervals in Linear Regression
------------------------------------------------------------------

1. **Confidence Intervals for Mean Response**:

   A **confidence interval for the mean response** estimates the range in which the **true mean** of the response variable is likely to fall for a specific value of the predictor variable :math:`x`.

   - **Formula for Mean Response**:

     .. math::

        \mu_y = \beta_0 + \beta_1 x^*

   - **Sample Estimate**:

     .. math::

        \hat{\mu}_y = b_0 + b_1 x^*

   - **Confidence Interval Formula**:

     .. math::

        \hat{\mu}_y \pm t^* SE_{\hat{\mu}_y}

     where :math:`t^*` is the critical value from the :math:`t`-distribution with :math:`n - 2` degrees of freedom.

   - **Interpretation**:

     This confidence interval provides the likely range for the **mean response** at a given value of :math:`x^*`, indicating the uncertainty in predicting the average outcome for a subpopulation.

2. **Prediction Intervals**:

   A **prediction interval** estimates the range in which an **individual future observation** of :math:`y` is likely to fall for a given value of :math:`x`.

   - **Formula for Predicted Response**:

     .. math::

        \hat{y} = b_0 + b_1 x^*

   - **Prediction Interval Formula**:

     .. math::

        \hat{y} \pm t^* SE_{\hat{y}}

     where :math:`t^*` is the critical value from the :math:`t`-distribution with :math:`n - 2` degrees of freedom.

   - **Difference Between Prediction and Confidence Intervals**:

     Prediction intervals are **wider** than confidence intervals because they account for:
     
     1. The variability of individual observations around the mean.

     2. The uncertainty in the estimated regression line.

   - **Interpretation**:
     If the process is repeated many times, 95% of the prediction intervals will contain the new observation's value.

.. image:: /images/1119.png

.. image:: /images/1120.png

Difference Between Confidence Interval and Prediction Interval
--------------------------------------------------------------

1. **What They Estimate**:

   - **Confidence Interval (CI)**: Estimates the **range where the true mean response** (:math:`\mu_y`) is likely to fall for a given value of the predictor :math:`x`.

   - **Prediction Interval (PI)**: Estimates the **range where a single future observation** of :math:`y` is likely to fall for the same value of :math:`x`.

2. **Scope of Uncertainty**:

   - **CI**: Accounts for the **uncertainty in estimating the mean** response.

   - **PI**: Accounts for both:

     1. Uncertainty in estimating the mean response.

     2. **Random variation of individual observations** around the mean.

3. **Width**:

   - **PI** is always **wider** than the CI because it includes both **model uncertainty** and **random variability** of individual observations.

4. **Formulas**:

   - **Confidence Interval for Mean Response**:

     .. math::

        \hat{\mu}_y \pm t^* SE_{\hat{\mu}_y}

   - **Prediction Interval for Future Observation**:

     .. math::

        \hat{y} \pm t^* SE_{\hat{y}}

   - Both intervals rely on the :math:`t`-distribution with :math:`n - 2` degrees of freedom. However, :math:`SE_{\hat{y}}` in the prediction interval accounts for more sources of variability.

5. **Interpretation**:

   - **CI**: Provides a range where the **average response** is likely to fall for a given value of :math:`x`.

   - **PI**: Provides a range where a **new individual observation** is likely to fall for the same value of :math:`x`.

6. **Example**:

   - **CI**: If the CI for mean BMI at 9000 steps/day is :math:`23.7 \pm 0.5`, the **average BMI** for individuals with this habit is likely between 23.2 and 24.2.

   - **PI**: If the PI for an individual's BMI at 9000 steps/day is :math:`23.7 \pm 2.0`, a **single person’s BMI** with this habit could fall between 21.7 and 25.7.

Analysis of Variance for Regression (ANOVA)
-------------------------------------------

1. **Concept of ANOVA for Regression**:

   ANOVA decomposes the **variation in the data** into two components: the **fit** (variation explained by the model) and the **residuals** (unexplained variation). This follows the conceptual equation:

   .. math::

      \text{DATA} = \text{FIT} + \text{RESIDUAL}

2. **Decomposing Total Variation**:

   - The total variation in the response variable :math:`y` is measured by deviations from the mean :math:`y_i - \bar{y}`.

   - This total variation is partitioned into:

     1. **Explained Variation (SSM)**: Variation due to changes in the predictor variable :math:`x`.

     2. **Unexplained Variation (SSE)**: Scatter of individual observations around the fitted values.

   - Mathematically:

     .. math::

        (y_i - \bar{y}) = (\hat{y}_i - \bar{y}) + (y_i - \hat{y}_i)

3. **Sum of Squares (SS) Decomposition**:

   The total sum of squared deviations (SST) can be decomposed as:

   .. math::

      \sum (y_i - \bar{y})^2 = \sum (\hat{y}_i - \bar{y})^2 + \sum (y_i - \hat{y}_i)^2

   This is equivalent to:

   .. math::

      SST = SSM + SSE

   where:

   - **SST**: Total Sum of Squares (total variation),

   - **SSM**: Model Sum of Squares (explained variation),

   - **SSE**: Error Sum of Squares (unexplained variation).

4. **Degrees of Freedom and Mean Squares**:

   - The **degrees of freedom** are divided as follows:

     - **DFT** (Total): :math:`n - 1`,

     - **DFM** (Model): 1 (for estimating the slope :math:`\beta_1`),

     - **DFE** (Error): :math:`n - 2` (one for the intercept, one for the slope).

   - The **mean square** (MS) is calculated as the ratio of the sum of squares to the corresponding degrees of freedom:

     .. math::

        MS = \frac{\text{Sum of Squares}}{\text{Degrees of Freedom}}

5. **Mean Square Error (MSE)**:

   - **MSE** is the average squared deviation of the observed values from the fitted values, providing an estimate of the variance of the errors:

     .. math::

        MSE = s^2 = \frac{\sum (y_i - \hat{y}_i)^2}{n - 2}

   - MSE estimates the variance of the residuals, :math:`\sigma^2`.

6. **Special Cases**:

   - If the slope :math:`b_1 = 0`, the model explains no variation (SSM = 0), and all the variation is due to error (SSE = SST).

   - If all observations lie perfectly on the regression line, SSE = 0, and SST = SSM.

.. image:: /images/1121.png

Interpretation of :math:`r^2`
-----------------------------

1. **Definition of :math:`r^2`**:

   - :math:`r^2` is the **fraction of the total variation** in the response variable :math:`y` that is explained by the **least-squares regression** of :math:`y` on :math:`x`.

2. **Sum of Squares Relationship**:

   - The relationship between the **total variation (SST)** and the **explained variation (SSM)** offers a precise way to interpret :math:`r^2`:

     .. math::

        r^2 = \frac{SSM}{SST} = \frac{\sum (\hat{y}_i - \bar{y})^2}{\sum (y_i - \bar{y})^2}

3. **Meaning of SST and SSM**:

   - **SST** (Total Sum of Squares): Measures the total variation in the response variable :math:`y`.

   - **SSM** (Model Sum of Squares): Measures the variation in :math:`y` that is explained by the regression model.

4. **Interpretation**:

   - :math:`r^2` quantifies the **proportion of the total variation** in :math:`y` that is explained by the predictor variable :math:`x` in the linear regression model.

The ANOVA F-Test for Regression
-------------------------------

1. **Purpose of the F-Test**:

   - The F-test examines the null hypothesis :math:`H_0: \beta_1 = 0`, indicating that the response variable :math:`y` is **not linearly related** to the predictor :math:`x`.

   - If the null hypothesis holds, the predictor :math:`x` does not explain any variation in :math:`y`.

2. **F-Statistic Formula**:

   - The F-statistic compares the **explained variance** (Mean Square Model, MSM) to the **unexplained variance** (Mean Square Error, MSE):

     .. math::

        F = \frac{MSM}{MSE}

3. **Degrees of Freedom**:

   - The F-statistic follows an **F-distribution** with:

     - **Numerator degrees of freedom**: 1 (for the slope).

     - **Denominator degrees of freedom**: :math:`n - 2` (for the error term).

4. **Interpretation of the F-Statistic**:

   - If :math:`H_0` is true, the F-statistic follows the F-distribution.

   - If :math:`H_0` is false (:math:`\beta_1 \neq 0`), MSM tends to be larger than MSE, resulting in a larger F-statistic. A large F-value provides evidence against :math:`H_0`.

5. **The F-Distribution**:

   - The F-distribution is **right-skewed** and takes only positive values.

   - It is defined by two parameters: the degrees of freedom for the **numerator** (MSM) and the **denominator** (MSE).

6. **Comparison with t-Tests**:

   - In simple linear regression, the F-test for :math:`H_0: \beta_1 = 0` is equivalent to the square of the t-statistic:

     .. math::

        t^2 = F

   - The t-test is preferred for testing one-sided hypotheses and constructing confidence intervals for :math:`\beta_1`.

7. **ANOVA Table Structure**:

   The results of ANOVA for regression are summarized in the following table:

   .. list-table:: ANOVA Table for Simple Linear Regression
      :widths: 20 20 30 20 10
      :header-rows: 1

      * - **Source**
        - **Degrees of Freedom**
        - **Sum of Squares**
        - **Mean Square**
        - **F**
      * - Model
        - 1
        - :math:`\sum (\hat{y}_i - \bar{y})^2`
        - :math:`MSM = \frac{\sum (\hat{y}_i - \bar{y})^2}{1}`
        - :math:`F = \frac{MSM}{MSE}`
      * - Error
        - :math:`n - 2`
        - :math:`\sum (y_i - \hat{y}_i)^2`
        - :math:`MSE = \frac{\sum (y_i - \hat{y}_i)^2}{n - 2}`
        - 
      * - Total
        - :math:`n - 1`
        - :math:`\sum (y_i - \bar{y})^2`
        - 
        - 

8. **Using F-Tables**:

   - F-tables provide **critical values** for the F-distribution, which are used when software cannot compute p-values directly.

   - The tables display critical values for typical significance levels (e.g., 0.10, 0.05, 0.01) based on the degrees of freedom in the numerator and the denominator.

9. **Conclusion**:

   - The F-test determines if the predictor :math:`x` explains a **significant amount of variation** in the response variable :math:`y`.

   - If the p-value for the F-statistic is small, we reject the null hypothesis :math:`H_0: \beta_1 = 0` and conclude that a linear relationship exists between :math:`x` and :math:`y`.

.. image:: /images/1122.png

Inference for Slope and Intercept
-------------------------------------------

1. **Purpose of Standard Errors**:

   - Confidence intervals and significance tests for the **slope** (:math:`\beta_1`) and **intercept** (:math:`\beta_0`) use the estimated coefficients :math:`b_1` and :math:`b_0` along with their **standard errors**.

2. **Standard Deviations of Slope and Intercept**:

   - **Standard Deviation of the Slope**:

     .. math::

        \sigma_{b_1} = \frac{\sigma}{\sqrt{\sum (x_i - \bar{x})^2}}

   - **Standard Deviation of the Intercept**:

     .. math::

        \sigma_{b_0} = \sigma \sqrt{\frac{1}{n} + \frac{\bar{x}^2}{\sum (x_i - \bar{x})^2}}

   - In practice, the population standard deviation :math:`\sigma` is replaced by its estimate :math:`s`.

3. **Standard Errors of Estimated Coefficients**:

   - **Standard Error of the Slope**:

     .. math::

        SE_{b_1} = \frac{s}{\sqrt{\sum (x_i - \bar{x})^2}}

   - **Standard Error of the Intercept**:

     .. math::

        SE_{b_0} = s \sqrt{\frac{1}{n} + \frac{\bar{x}^2}{\sum (x_i - \bar{x})^2}}

4. **Inference Using Small Samples**:

   - With small samples, the regression line might suggest a strong relationship. **Significance testing** for the slope helps determine whether the relationship is statistically significant.

Derivation of Standard Errors for Slope and Intercept (Optional)
----------------------------------------------------------------

1. **Standard Error of the Slope**:

   The slope estimator :math:`b_1` is calculated as:

   .. math::

      b_1 = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sum (x_i - \bar{x})^2}

   Using the assumption of independent and identically distributed (i.i.d.) errors, the variance of :math:`b_1` is:

   .. math::

      \text{Var}(b_1) = \frac{\sigma^2}{\sum (x_i - \bar{x})^2}

   The standard error of the slope is the square root of the variance:

   .. math::

      SE_{b_1} = \frac{s}{\sqrt{\sum (x_i - \bar{x})^2}}

2. **Standard Error of the Intercept**:

   The intercept estimator :math:`b_0` is given by:

   .. math::

      b_0 = \bar{y} - b_1 \bar{x}

   The variance of the intercept is:

   .. math::

      \text{Var}(b_0) = \frac{\sigma^2}{n} + \bar{x}^2 \frac{\sigma^2}{\sum (x_i - \bar{x})^2}

   The standard error of the intercept is:

   .. math::

      SE_{b_0} = s \sqrt{\frac{1}{n} + \frac{\bar{x}^2}{\sum (x_i - \bar{x})^2}}

.. image:: /images/1123.png

Confidence Intervals vs. Prediction Intervals
---------------------------------------------

1. **Two Uses of the Estimated Response**:

   - **Mean Response** (:math:`\mu_y`): Estimates the mean value of the response variable for a given predictor value :math:`x^*`.

   - **Prediction for a New Observation** (:math:`\hat{y}`): Predicts the response for a new individual observation at :math:`x^*`.

2. **Differences Between Confidence and Prediction Intervals**:

   - **Confidence Intervals**:

     - Estimate the **mean response**.

     - Typically **narrower** than prediction intervals.

   - **Prediction Intervals**:

     - Account for individual-level variability, making them **wider** than confidence intervals.

3. **Standard Errors**:

   - **Standard Error for the Mean Response**:

     .. math::

        SE_{\hat{\mu}_y} = s \sqrt{\frac{1}{n} + \frac{(x^* - \bar{x})^2}{\sum (x_i - \bar{x})^2}}

   - **Standard Error for Predicting a New Observation**:

     .. math::

        SE_{\hat{y}} = s \sqrt{1 + \frac{1}{n} + \frac{(x^* - \bar{x})^2}{\sum (x_i - \bar{x})^2}}

4. **Key Difference in Formulas**:

   - The prediction interval formula includes an **extra "1" under the square root**, reflecting the additional variability in individual predictions.

   - This makes **prediction intervals wider** than confidence intervals.

5. **Illustrative Example**:

   - **Gestational Age Prediction**:

     - A **confidence interval** provides the likely range for the **average gestational age** based on predictor variables.

     - A **prediction interval** gives the range for a **new fetus**, accounting for individual deviations.

Role of :math:`x^*` in Confidence and Prediction Intervals
------------------------------------------------------------

1. **Confidence Interval for the Mean Response**:

   - **Purpose**: To estimate the **mean response** :math:`\mu_y` at a given value :math:`x^*`.

   - **When Used**: :math:`x^*` can be one of the **observed data points** or any value within the range of the predictor variable.

   .. math::

      SE_{\hat{\mu}_y} = s \sqrt{\frac{1}{n} + \frac{(x^* - \bar{x})^2}{\sum (x_i - \bar{x})^2}}

2. **Prediction Interval for a New Observation**:

   - **Purpose**: To predict the response :math:`y` for a **new observation** with the same value :math:`x^*`.

   - **When Used**: :math:`x^*` may refer to a **new data point** outside the original sample.

   .. math::

      SE_{\hat{y}} = s \sqrt{1 + \frac{1}{n} + \frac{(x^* - \bar{x})^2}{\sum (x_i - \bar{x})^2}}

3. **Key Difference**:

   - Prediction intervals include an additional **1** under the square root, capturing the randomness of individual observations.

   - **Prediction intervals** are **wider** than confidence intervals due to this extra variability.

.. image:: /images/1124.png

Inference for Correlation
--------------------------

1. **Population vs. Sample Correlation**:

   - **Population Correlation** (:math:`\rho`): Measures the strength and direction of a linear association between two variables.

   - **Sample Correlation** (:math:`r`): An estimate of the population correlation based on the sample data.

2. **Inference About Population Correlation**:

   - We use the sample correlation to test hypotheses about the population correlation.

3. **Null Hypothesis**:

   .. math::

      H_0: \rho = 0

   (No linear association between :math:`x` and :math:`y`.)

   - If :math:`H_0` is true and both :math:`x` and :math:`y` are normally distributed, then :math:`x` and :math:`y` are independent.

4. **t-Statistic for Testing Population Correlation**:

   .. math::

      t = \frac{r \sqrt{n - 2}}{\sqrt{1 - r^2}}

   - Where:

     - :math:`n` = sample size

     - :math:`r` = sample correlation

5. **Distribution of the t-Statistic**:

   - The t-statistic follows a **t-distribution** with :math:`n - 2` degrees of freedom.

   - The **P-value** is determined based on the alternative hypothesis:

     - :math:`H_a: \rho > 0 \Rightarrow P(T \geq t)`

     - :math:`H_a: \rho < 0 \Rightarrow P(T \leq t)`

     - :math:`H_a: \rho \neq 0 \Rightarrow 2P(T \geq |t|)`

6. **Conclusion**:

   - If the **P-value** is small, we reject the null hypothesis, indicating a significant linear relationship between :math:`x` and :math:`y`.

.. image:: /images/1125.png


Week 10: Ch13 Two-Way ANOVA  
============================

When there is more than one way to classify the populations, and when you want to assess the effects of two categorical factors and determine whether there is an interaction effect between them, we use **two-way ANOVA**. 

For example: 

- **Factor 1 (Teaching Method)**: Online vs. In-person  

- **Factor 2 (Classroom Type)**: Regular vs. Honors  

- **Dependent Variable**: Test Scores

In two-way ANOVA, there are two factors, each with its own number of levels. For one-way ANOVA, we study the effect of a factor by changing the levels. In two-way ANOVA, we study the effects of two factors, known as **main effects** (the average values for the effects of the two factors). 

However, we are also interested in the **interaction effect**, which occurs when the effectiveness of one factor depends on another factor. One-way designs that vary a single factor and hold other factors fixed cannot detect these interaction effects. If we ignore the interaction, our conclusions might be misleading, even if we follow the correct procedure.

Interaction Effect in Two-Way ANOVA  
-----------------------------------

The interaction effect occurs when the effect of one factor on the response variable depends on the level of the other factor. In other words, the combined influence of the two factors is different from their individual main effects. Ignoring interaction effects can lead to biased results and incorrect conclusions.

If we ignore interaction, the model becomes misspecified, introducing omitted variable bias and missing out on crucial combined effects that explain variability in the response variable.

**Understanding Multiplication as Interaction**  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In a linear regression model with two predictors (without interaction), the relationship between the predictors and the response :math:`Y` is:

.. math::  
   Y = \beta_0 + \beta_1 \cdot X_1 + \beta_2 \cdot X_2 + \epsilon

- :math:`\beta_1`: Measures the effect of :math:`X_1` on :math:`Y` when :math:`X_2` is held constant.  

- :math:`\beta_2`: Measures the effect of :math:`X_2` on :math:`Y` when :math:`X_1` is held constant.

This model assumes that the effect of :math:`X_1` on :math:`Y` is the same no matter the value of :math:`X_2`, and vice versa. However, if the impact of :math:`X_1` on :math:`Y` changes depending on the value of :math:`X_2`, there is an **interaction effect**.

To capture this dependency, we introduce a product term :math:`X_1 \times X_2`. The full model with interaction becomes:

.. math::  
   Y = \beta_0 + \beta_1 \cdot X_1 + \beta_2 \cdot X_2 + \beta_3 \cdot (X_1 \times X_2) + \epsilon

- **Without interaction** (:math:`\beta_3 = 0`):  

  - The effect of :math:`X_1` on :math:`Y` is fixed at :math:`\beta_1`, regardless of the value of :math:`X_2`.  

  - Similarly, the effect of \:math:`X_2` on :math:`Y` is :math:`\beta_2`, no matter the value of :math:`X_1`.

- **With interaction** (:math:`\beta_3 \neq 0`):  

  - The effect of :math:`X_1` on :math:`Y` changes depending on the value of :math:`X_2`. 

  - Similarly, the effect of :math:`X_2` on :math:`Y` depends on the value of :math:`X_1`.

The interaction term :math:`X_1 \times X_2` allows us to model this dependency between the two predictors.

Advantages of Two-Way ANOVA  
---------------------------

There are other advantages to using two-way ANOVA over one-way ANOVA.

.. image:: /images/1001.png

Example 13.1, 2, and 3  
----------------------

These considerations also apply to study designs with more than two factors. The statistical analysis in such cases is broadly called **higher-way ANOVA**. Although the details become more complex, the key ideas are already present in two-way ANOVA settings.

The Two-Way ANOVA Model  
-----------------------

.. image:: /images/1002.png

Much as in the one-way model, the **FIT** part is the group means :math:`\mu_{ij}`, and the **RESIDUAL (Error Term)** part is the deviations :math:`\epsilon_{ijk}` of the individual observations from their group means.

To estimate a group mean :math:`\mu_{ij}`, we use the sample mean of the observations in the samples from this group:

.. math::

   \bar{x}_{ij} = \frac{1}{n_{ij}} \sum_k x_{ijk}

The :math:`k` below the summation sign indicates that we sum the :math:`n_{ij}` observations that belong to the :math:`(i, j)`-th sample.

The RESIDUAL part of the model is represented by the unknown :math:`\sigma`. First, we calculate the sample variances for each SRS. Provided that it is reasonable to assume a common standard deviation (see the rule on page 608), we pool the sample variances to estimate :math:`\sigma^2`:

.. math::

   s_p^2 = \frac{\sum (n_{ij} - 1) s_{ij}^2}{\sum (n_{ij} - 1)}

In this formula:
- The numerator is the **SSE** (Sum of Squares for Error).
- The denominator is the **DFE** (Degrees of Freedom for Error).  
- **DFE** is the total number of observations minus the number of groups:

.. math::

   \text{DFE} = N - IJ

The estimator of :math:`\sigma` is the **pooled standard deviation** :math:`s_p`.

Sum of Squares (SS) Terms and Degrees of Freedom (DF) Terms  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

### Sum of Squares (SS) Terms  

1. **Total Sum of Squares (SST)**

   .. math::

      SST = \sum_{i,j,k} (x_{ijk} - \bar{x}_{..})^2

   - **SST** measures the total variability from the grand mean.  
   - :math:`x_{ijk}` is the \(k\)-th observation for the group with Factor A at level \(i\) and Factor B at level \(j\).  
   - :math:`\bar{x}_{..}` is the grand mean (mean of all observations).

2. **Sum of Squares for Factor A (SSA)**

   .. math::

      SSA = \sum_{i} n_{i\cdot} (\bar{x}_{i\cdot} - \bar{x}_{..})^2

   - **SSA** measures the variability between the levels of Factor A.  
   - :math:`n_{i\cdot}`: Total number of observations for level \(i\) of Factor A.  
   - :math:`\bar{x}_{i\cdot}`: Mean for level \(i\) of Factor A.

3. **Sum of Squares for Factor B (SSB)**

   .. math::

      SSB = \sum_{j} n_{\cdot j} (\bar{x}_{\cdot j} - \bar{x}_{..})^2

   - **SSB** measures the variability between the levels of Factor B.  
   - :math:`n_{\cdot j}`: Total number of observations for level \(j\) of Factor B.  
   - :math:`\bar{x}_{\cdot j}`: Mean for level \(j\) of Factor B.

4. **Sum of Squares for Interaction (SSAB)**

   .. math::

      SSAB = \sum_{i,j} n_{ij} \left( \bar{x}_{ij} - \bar{x}_{i\cdot} - \bar{x}_{\cdot j} + \bar{x}_{..} \right)^2

   - **SSAB** measures the interaction effect between Factors A and B.

5. **Sum of Squares for Residuals/Error (SSE)**

   .. math::

      SSE = \sum_{i,j,k} (x_{ijk} - \bar{x}_{ij})^2

   - **SSE** measures the unexplained variability within groups.  

   - :math:`\bar{x}_{ij}`: Mean for the group with Factor A at level \(i\) and Factor B at level \(j\).

### Relationship Between SS Terms  

.. math::

   SST = SSA + SSB + SSAB + SSE

SSG (Sum of Squares for Groups) is the sum of SSA, SSB, and SSAB.

### Degrees of Freedom (DF) Terms  

1. **Total Degrees of Freedom (DFT)**

   .. math::

      DFT = N - 1

   - \(N\): Total number of observations.

2. **Degrees of Freedom for Factor A (DFA)**

   .. math::

      DFA = I - 1

   - \(I\): Number of levels of Factor A.

3. **Degrees of Freedom for Factor B (DFB)**

   .. math::

      DFB = J - 1

   - \(J\): Number of levels of Factor B.

4. **Degrees of Freedom for Interaction (DFAB)**

   .. math::

      DFAB = (I - 1)(J - 1)

5. **Degrees of Freedom for Residuals (DFE)**

   .. math::

      DFE = N - IJ

### Relationship Between DF Terms  

.. math::

   DFT = DFA + DFB + DFAB + DFE

SSAB: Breaking Down the Formula  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. :math:`\bar{x}_{ij}` 

   – Mean for the group at **level** :math:`i` **of Factor A** and **level** :math:`j` **of Factor B**.  

   - Represents the **observed group mean** for the specific combination of two factor levels.

2. :math:`\bar{x}_{i\cdot}` 
   
   – Marginal mean for **level** :math:`i` **of Factor A**, averaged across all levels of Factor B.  

   - Represents the **main effect of Factor A**, assuming no interaction with Factor B.

3. :math:`\bar{x}_{\cdot j}`

   – Marginal mean for **level** :math:`j` **of Factor B**, averaged across all levels of Factor A.  

   - Represents the **main effect of Factor B**, assuming no interaction with Factor A.

4. :math:`\bar{x}_{..}`
   
   – Grand mean of all observations in the dataset.  

   - Used to adjust for the subtraction of marginal means.

### How the Formula Captures Interaction Effect  

The expression inside the parentheses:

.. math::

   \left( \bar{x}_{ij} - \bar{x}_{i\cdot} - \bar{x}_{\cdot j} + \bar{x}_{..} \right)

captures the **additional variability** that cannot be explained by the main effects of Factor A and Factor B alone.

1. **Subtract** :math:`\bar{x}_{i\cdot}`:  

   - Removes the portion of the group mean :math:`\bar{x}_{ij}` explained by Factor A.

2. **Subtract** :math:`\bar{x}_{\cdot j}`:  

   - Removes the portion of the group mean :math:`\bar{x}_{ij}` explained by Factor B.

3. **Add** :math:`\bar{x}_{..}`:  

   - Adjusts for subtracting the grand mean twice.

.. image:: /images/1003.png
.. image:: /images/1004.png

Example 13.6 and 7: **Repeated-Measures Design**

Example from the Document (Example 13.7)  
----------------------------------------

In this example, the study investigated how well subjects synchronized with music from different cultures. French and Tunisian nationals listened to both French and Tunisian music and were asked to tap in time with the beat.

**Repeated Measurements**:  
Each subject provided data for both types of music (French and Tunisian).

**Dependent Observations**:  
The two synchronization scores for each subject are not independent because they come from the same individual. This design allows researchers to compare synchronization performance for the same subjects under both conditions (French and Tunisian music), helping to control for individual differences.

Advantages of Repeated-Measures Design  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- **Reduces variability**:  
  By using the same subjects across conditions, variability due to individual differences is minimized.

- **Fewer participants needed**:  
  Since each subject provides multiple measurements, fewer participants are required compared to designs with independent groups.

- **Increases statistical power**:  
  The design improves the ability to detect significant differences.

Disadvantages of Repeated-Measures Design  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- **Order Effects**:  
  The order in which treatments are administered may affect the results (e.g., fatigue or practice effects).

  **Solution**: Counterbalance the order of conditions.

- **Carryover Effects**:  
  A treatment may have lasting effects that influence the outcome in later conditions.

  **Solution**: Include a washout period between treatments.

Why Dependent Observations Violate the Assumptions  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Dependency Between Observations** creates correlated data, meaning the observations are no longer independent. In a standard two-way ANOVA, we assume that each observation provides independent information about the group it belongs to. When observations are dependent (e.g., repeated measures), this assumption is violated.

This dependency inflates **Type I error rates**, making the ANOVA model unreliable because it assumes more independent information than what is truly present.

Inference for Two-Way ANOVA  
---------------------------

.. image:: /images/1005.png
.. image:: /images/1006.png
.. image:: /images/1007.png

Proof: Pooled Variance Formula Equivalent to SSE / DFE  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The pooled sample variance :math:`s_p^2` is given by:

.. math::

   s_p^2 = \frac{\sum (n_{ij} - 1) s_{ij}^2}{\sum (n_{ij} - 1)}

We will show that this formula is equivalent to:

.. math::

   s_p^2 = \frac{SSE}{DFE}

where **SSE** is the Sum of Squares for Residuals, and **DFE** is the Degrees of Freedom for Error.

### Step 1: Define the Terms  

1. **Sample Variance for Group** :math:`(i, j)`:

   .. math::

      s_{ij}^2 = \frac{1}{n_{ij} - 1} \sum_{k=1}^{n_{ij}} \left( x_{ijk} - \bar{x}_{ij} \right)^2

   where:

   - :math:`x_{ijk}` is the :math:`k`-th observation in the group :math:`(i, j)`. 

   - :math:`\bar{x}_{ij}` is the mean of the group :math:`(i, j)`.  

   - :math:`n_{ij}` is the number of observations in group :math:`(i, j)`.

2. **Sum of Squares for Group** :math:`(i, j)`:

   .. math::

      SS_{ij} = \sum_{k=1}^{n_{ij}} \left( x_{ijk} - \bar{x}_{ij} \right)^2

3. **Degrees of Freedom for Group** :math:`(i, j)`:

   .. math::

      DF_{ij} = n_{ij} - 1

### Step 2: Rewrite the Pooled Variance Formula  

Substitute the formula for :math:`s_{ij}^2` into the pooled variance equation:

.. math::

   s_p^2 = \frac{\sum (n_{ij} - 1) \cdot \frac{1}{n_{ij} - 1} \sum_{k=1}^{n_{ij}} \left( x_{ijk} - \bar{x}_{ij} \right)^2}{\sum (n_{ij} - 1)}

The :math:`(n_{ij} - 1)` terms cancel out:

.. math::

   s_p^2 = \frac{\sum \sum_{k=1}^{n_{ij}} \left( x_{ijk} - \bar{x}_{ij} \right)^2}{\sum (n_{ij} - 1)}

### Step 3: Express the Numerator as SSE  

The numerator represents the **Sum of Squares for Residuals (SSE)**:

.. math::

   SSE = \sum_{i,j} \sum_{k=1}^{n_{ij}} \left( x_{ijk} - \bar{x}_{ij} \right)^2

Thus, the pooled variance formula becomes:

.. math::

   s_p^2 = \frac{SSE}{\sum (n_{ij} - 1)}

### Step 4: Define Degrees of Freedom for Error (DFE)  

The **Degrees of Freedom for Error (DFE)** is the sum of the degrees of freedom for all groups:

.. math::

   DFE = \sum_{i,j} (n_{ij} - 1)

### Step 5: Substitute DFE into the Pooled Variance Formula  

Now, substitute the expression for **DFE** into the pooled variance formula:

.. math::

   s_p^2 = \frac{SSE}{DFE}

We have shown that the pooled variance formula:

.. math::

   s_p^2 = \frac{\sum (n_{ij} - 1) s_{ij}^2}{\sum (n_{ij} - 1)}

is equivalent to:

.. math::

   s_p^2 = \frac{SSE}{DFE}

This completes the proof. The pooled variance :math:`s_p^2` is simply the **mean squared error (MSE)**, which is the residual sum of squares (SSE) divided by the degrees of freedom for error (DFE).

Assumptions for Two-Way ANOVA  
-----------------------------

Two-way ANOVA analyzes the effects of two categorical independent variables (factors) on a dependent variable, along with the interaction between the two factors. The assumptions are similar to those for one-way ANOVA, but with some additional considerations.

### Independence of Observations  

- As with one-way ANOVA, observations within and between groups must be independent.

### Normality of Residuals  

- The residuals from the two-way ANOVA should be normally distributed.  
- This assumption applies to the residuals of the model, not necessarily the raw data.

### Homogeneity of Variances  

- The variances across all groups (combinations of the two factors) should be equal.  
- This assumption ensures that the spread of the data is consistent across all factor levels.

**How to check:**
- Use **Levene’s** or **Bartlett’s test**.  
- If violated, consider transforming the data or using a **robust ANOVA method**.

### Additivity  

- The effects of the two independent variables on the dependent variable should be **additive**, unless an interaction term is included in the model.  
- If there is an interaction between the two factors, the interpretation of the main effects changes.

### Balanced Design (Optional but Recommended)  

- While not a strict assumption, a **balanced design** (equal sample sizes in all groups) helps ensure the results are more reliable.  
- Unequal group sizes can reduce the power of the test and complicate the interpretation of interactions.





Week 09: Ch12: One-Way Analysis of Variance
===========================================

In week 07, we talked about how to compare two means from two independent groups. But what if we have more than two independent groups, and we want to see if the means are different from each other? A natural extension is to perform multiple :math:`t`-tests for each pair of two independent samples. However, this approach presents two major problems:

1. The number of tests grows quickly with the number of groups, :math:`k`. Specifically, we need :math:`k(k-1)/2` such tests, which becomes impractical for large :math:`k`.
2. With many tests, the chance of a **Type I error** increases, meaning that we are more likely to incorrectly reject a null hypothesis just by chance.

Thus, we need another approach to solve this problem. This leads us to the **One-Way Analysis of Variance (ANOVA)** and the :math:`F` statistic/test.

There are two types of ANOVA:

One-Way ANOVA
-------------

One-way ANOVA is used when there is **one way (one factor)** to classify the populations of interest. For example, if we want to compare the average exam scores of students from three different classrooms (the factor being "Classroom" with three levels), one-way ANOVA is appropriate.

Two-Way ANOVA
-------------

Two-way ANOVA is used when there are **two factors**. For example, we might assess the effects of two factors: **teaching method** (online or in-person) and **classroom type** (regular or honors) on student performance. The goal is to determine not only the individual effects of each factor but also whether there is an **interaction effect** between them.

**We will focus on one-way ANOVA first.**

Setting for One-Way ANOVA
--------------------------

The data for one-way ANOVA are collected similarly to the two-sample case. Either:
- We draw a random sample from each population, or
- We randomly assign subjects to different treatments.

The resulting data are used to test the **null hypothesis** that the means are all equal. That is, are the observed differences in sample means due to chance, or do they provide strong evidence of significant differences among the group means?

**Example 12.1 and 12.2**

In one-way ANOVA, we consider both **Between-Group Variation** and **Within-Group Variation**.

.. image:: /images/0901.png

Between-Group Variation: Identifying Differences in Means (Signal)
------------------------------------------------------------------

Between-group variation captures how much the group means differ from the overall mean. If the group means are far apart, it suggests meaningful differences among the groups. However, large between-group variation alone isn’t enough unless it is large relative to the within-group variation.

*Example:* If you have three groups with means 10, 30, and 50, the between-group variation is large. However, these differences may not be statistically significant unless the within-group variation is small.

Within-Group Variation: Accounting for Noise
--------------------------------------------

Within-group variation measures how much individual observations deviate from their own group mean. It reflects the natural variability or random noise within the groups.

*Example:* If each group has highly variable observations (e.g., values 5, 50, 100 in a group), the within-group variation will be large. This makes it harder to confidently conclude that the groups differ, even if their means are different.

Let’s illustrate this concept further using the pooled two-sample :math:`t`-statistic.

.. image:: /images/0902.png

Balancing Signal and Noise: The F-Ratio
---------------------------------------

The **F-ratio** in ANOVA compares the **between-group variation (signal)** with the **within-group variation (noise)**:

.. math:: 
   F = \frac{MSB}{MSW}

where:
- **MSB (Mean Square Between)**: Captures the variation between the group means.
- **MSW (Mean Square Within)**: Captures the variation within the groups (noise).

A **large F-ratio** suggests that the group means are significantly different. A **small F-ratio** suggests that any differences in group means are likely due to random chance.

Why Both Types of Variation Matter
----------------------------------

If we only look at between-group variation, we might falsely conclude that the groups differ. However, if the within-group variation is large, these differences may not be statistically significant. Conversely, if the within-group variation is small, even small differences in group means can be significant.

Example:

1. **Case 1**: Group means are 10, 20, 30, with low within-group variation. The F-ratio will be high, suggesting significant differences.
2. **Case 2**: Group means are 10, 20, 30, but with high within-group variation. The F-ratio will be small, making it harder to detect differences.

Statistical Intuition: When to Reject the Null Hypothesis
---------------------------------------------------------

The null hypothesis in one-way ANOVA assumes that all group means are equal. To reject it, the between-group variation must be significantly larger than the within-group variation (i.e., the F-ratio must be large).

Summary: Balancing Signal and Noise
-----------------------------------

- **Between-group variation**: Reflects the signal (how much the group means differ).
- **Within-group variation**: Reflects the noise (random variability within each group).

Both types of variation are needed to determine if the differences are statistically significant. A large F-ratio indicates that the signal outweighs the noise.

Introducing Regression: Data = Fit + Residual
---------------------------------------------

Once we understand the intuition, we need to delve into the details of how to calculate the F-test statistic, also known as the F-ratio. Before proceeding, let’s take a brief detour into regression. Regression is a statistical technique that uses a model to make predictions about the data by finding the best fit. The model divides the data into two components:

**Data = Fit + Residual**

- **Fit**: The part of the data explained by the model.
- **Residual**: The leftover part, which the model couldn’t explain.

In our ANOVA setting, the ANOVA model assumes that every observation can be written as:

.. math::

   x_{ij} = \mu_i + \epsilon_{ij}

Where:

- :math:`x_{ij}` is the data point for the j-th observation in the i-th group.
- :math:`\mu_i` is the mean of the i-th group (this is the FIT part).
- :math:`\epsilon_{ij}` is the residual for that observation, representing how far it is from the group mean (this is the RESIDUAL part).

This breakdown means that each observation is made up of:

- A systematic component (the group mean, :math:`\mu_i`).
- A random component (the residual, :math:`\epsilon_{ij}`, which accounts for the natural variability within the group).

.. image:: /images/0903.png

There are two unknown parameters in this statistical model: :math:`\mu` and :math:`\sigma`. 
We estimate :math:`\mu` by :math:`\bar{x}`, the sample mean, and :math:`\sigma` by :math:`s`, the sample standard deviation. 
The differences :math:`e_j = x_j - \bar{x}` are the *residuals* and correspond to the :math:`\epsilon_j` in the statistical model. 

Errors (:math:`\epsilon_j`) refer to the deviations from the true population mean or model. They are part of the underlying population model.  
Residuals (:math:`e_j`) are based on the observed sample data, and they measure the deviation of the sample observations from the sample mean or the fitted model.

Let's go through the math for calculating the **Mean Square Between (MSB)** and the **Mean Square Within (MSW)**, both of which are central to the F-ratio in **one-way ANOVA**.

Suppose:
-------

- We have :math:`k` groups (treatments or categories).
- Each group has a certain number of observations, denoted by :math:`n_i` for group :math:`i` (where :math:`i = 1, 2, \dots, k`).
- The total number of observations across all groups is :math:`N = n_1 + n_2 + \dots + n_k`.

1. **Calculating the Mean Square Between (MSB)**:
--------------------------------------------------

**MSB** measures the variation **between** the group means and the overall mean.

- **Step 1**: Calculate the **group means**:
  For each group :math:`i`, calculate the sample mean :math:`\bar{X}_i`:

  .. math::
     \bar{X}_i = \frac{1}{n_i} \sum_{j=1}^{n_i} X_{ij}

  where :math:`X_{ij}` represents the :math:`j`-th observation in group :math:`i`.

- **Step 2**: Calculate the **overall mean** (:math:`\bar{X}_{\text{overall}}`), which is the mean of all observations across all groups:

  .. math::
     \bar{X}_{\text{overall}} = \frac{1}{N} \sum_{i=1}^{k} \sum_{j=1}^{n_i} X_{ij}

  This is simply the weighted average of all the data points.

- **Step 3**: Compute the **Sum of Squares Between (SSB)**, which measures how much the group means deviate from the overall mean:

  .. math::
     SSB = \sum_{i=1}^{k} n_i (\bar{X}_i - \bar{X}_{\text{overall}})^2

  Here, :math:`n_i` is the number of observations in group :math:`i`, and :math:`(\bar{X}_i - \bar{X}_{\text{overall}})^2` represents the squared difference between the group mean and the overall mean.

- **Step 4**: Calculate the **Mean Square Between (MSB)** by dividing the **SSB** by the **degrees of freedom** between groups:

  .. math::
     MSB = \frac{SSB}{k - 1}

2. **Calculating the Mean Square Within (MSW)**:
-------------------------------------------------

**MSW** measures the variation **within** each group, i.e., the variability of observations around their respective group means.

- **Step 1**: Compute the **Sum of Squares Within (SSW)**:

  .. math::
     SSW = \sum_{i=1}^{k} \sum_{j=1}^{n_i} (X_{ij} - \bar{X}_i)^2

- **Step 2**: Calculate the **Mean Square Within (MSW)** by dividing the **SSW** by the **degrees of freedom** within groups:

  .. math::
     MSW = \frac{SSW}{N - k}

3. **Summarizing the Formulas**:
---------------------------------

- **Mean Square Between (MSB)**:

  .. math::
     MSB = \frac{\sum_{i=1}^{k} n_i (\bar{X}_i - \bar{X}_{\text{overall}})^2}{k - 1}

- **Mean Square Within (MSW)**:

  .. math::
     MSW = \frac{\sum_{i=1}^{k} \sum_{j=1}^{n_i} (X_{ij} - \bar{X}_i)^2}{N - k}

4. **F-Ratio**:
---------------

Finally, the **F-ratio** is the ratio of these two mean squares:

.. math::
   F = \frac{MSB}{MSW}

This F-ratio tells us whether the variation between the groups is significantly greater than the variation within the groups.

Example:
--------

Suppose we have 3 groups with the following data:

- Group 1: :math:`X_1 = \{ 5, 6, 7 \}`
- Group 2: :math:`X_2 = \{ 10, 11, 12 \}`
- Group 3: :math:`X_3 = \{ 20, 21, 22 \}`

1. **Group Means**:
   - :math:`\bar{X}_1 = 6`
   - :math:`\bar{X}_2 = 11`
   - :math:`\bar{X}_3 = 21`

2. **Overall Mean**:

   .. math::
      \bar{X}_{\text{overall}} = \frac{(5 + 6 + 7 + 10 + 11 + 12 + 20 + 21 + 22)}{9} = 13

3. **Calculate SSB**:

   .. math::
      SSB = 3(6 - 13)^2 + 3(11 - 13)^2 + 3(21 - 13)^2 = 3(49) + 3(4) + 3(64) = 351

4. **Calculate MSB** (with 2 degrees of freedom, :math:`k - 1 = 3 - 1`):

   .. math::
      MSB = \frac{351}{2} = 175.5

5. **Calculate SSW**:

   .. math::

   SSW = (5 - 6)^2 + (6 - 6)^2 + (7 - 6)^2 
       + (10 - 11)^2 + (11 - 11)^2 + (12 - 11)^2 
       + (20 - 21)^2 + (21 - 21)^2 + (22 - 21)^2 
       = 6


6. **Calculate MSW** (with 6 degrees of freedom, :math:`N - k = 9 - 3`):

   .. math::
      MSW = \frac{6}{6} = 1

7. **Calculate the F-ratio**:

   .. math::
      F = \frac{MSB}{MSW} = \frac{175.5}{1} = 175.5

Interpretation:
---------------

A large F-ratio like 175.5 indicates that the between-group variation is much larger than the within-group variation, suggesting that the group means are significantly different.

This is how you calculate **MSB** and **MSW**, which leads to the F-ratio used in the one-way ANOVA test to evaluate whether the group means are statistically significantly different.

You can also find an example here: `https://online.stat.psu.edu/stat200/lesson/10/10.2 <https://online.stat.psu.edu/stat200/lesson/10/10.2>`_.

Examing Standard Deviation
--------------------------

.. image:: /images/0904.png

Pooled Estimator
----------------

.. image:: /images/0905.png

Hypothesis Testing
------------------

.. image:: /images/0906.png

.. image:: /images/0907.png

.. image:: /images/0908.png

Assumptions for One-Way ANOVA
-----------------------------

One-way ANOVA compares the means of three or more independent groups to determine if there is a statistically significant difference between them. For the results of the ANOVA to be valid, several key assumptions must be met.

Independence of Observations
----------------------------

- The observations within each group and between groups must be independent of each other.  
- This means that **one observation should not influence another**.  
- Independence ensures that each data point contributes uniquely to the analysis, avoiding biases.

Normality of Residuals (or Data)
-------------------------------

- The residuals (the differences between observed values and group means) should be **normally distributed**.
- This assumption ensures that any deviations from the group means follow a **bell-shaped (normal) distribution**. 

**How to check:**
- Use **visual tools** such as a **Q-Q plot (quantile-quantile plot)** to assess whether the residuals follow a straight line.
- Perform a **Shapiro-Wilk test** for normality. If the p-value is large, the normality assumption is not violated.

Homogeneity of Variances (Homoscedasticity)
-------------------------------------------

- The variances (or standard deviations) across all groups must be **equal or approximately equal**.  
- This assumption ensures that the **spread of the data is similar** across groups, making the F-test valid.

**How to check:**
- Use **Levene's test** or **Bartlett's test** to test for equality of variances.
  - If the p-value is large, the variances are approximately equal.
  - If the assumption is violated, consider using **Welch’s ANOVA**, which doesn’t assume equal variances.

Random Sampling
---------------

- Each group should consist of a **random sample** from the population.  
- Random sampling ensures that the results are **generalizable** to the broader population.

Follow-Up Inference Procedures After One-Way ANOVA
--------------------------------------------------

After performing a **one-way ANOVA F-test**, we know whether there are significant differences between the group means. However, the ANOVA F-test only tells us that **at least one group mean differs** but does not indicate **which specific means differ** or provide more nuanced insights.

To gain a deeper understanding, we conduct two common follow-up procedures:
1. **Contrasts (Planned Comparisons)**
2. **Multiple Comparisons (Post-Hoc Tests)**

These procedures allow us to:
- **Contrasts**: Test **specific hypotheses** about the differences between groups.
- **Post-hoc tests**: Explore **all possible pairwise comparisons** when we do not have pre-defined hypotheses, while controlling for Type I error.


1. **Contrasts (Planned Comparisons)**
--------------------------------------

Contrasts are used to test **specific hypotheses** that we develop **before conducting ANOVA**. Each contrast is a **linear combination of group means**, comparing the means in a focused way.

.. image:: /images/0909.png

**Example: Planned Comparison**

Consider three groups with the following sample means and sizes:

- Group 1: :math:`\bar{X}_1 = 10`, :math:`n_1 = 5`  
- Group 2: :math:`\bar{X}_2 = 12`, :math:`n_2 = 5`  
- Group 3: :math:`\bar{X}_3 = 15`, :math:`n_3 = 5`  

We are interested in testing the following contrast:

.. math::
   \psi = -2 \mu_1 + \mu_2 + \mu_3

This tests whether Group 1’s mean is significantly lower than the combined means of Groups 2 and 3.

**Step-by-Step Calculation**

**Step 1: Compute the Sample Contrast Value**

.. math::
   \hat{\psi} = -2(10) + 12 + 15 = -20 + 27 = 7

**Step 2: Calculate the Pooled Standard Deviation**

The **Mean Square Within (MSW)** from the ANOVA is given as 4. The **pooled standard deviation** is:

.. math::
   s_p = \sqrt{MSW} = \sqrt{4} = 2

**Step 3: Calculate the Standard Error (SE) for the Contrast**

.. math::
   SE_{\hat{\psi}} = s_p \sqrt{\frac{(-2)^2}{5} + \frac{1^2}{5} + \frac{1^2}{5}}
   = 2 \sqrt{\frac{4}{5} + \frac{1}{5} + \frac{1}{5}}
   = 2 \sqrt{\frac{6}{5}} = 2 \times 1.095 = 2.19

**Step 4: Calculate the t-Statistic**

.. math::
   t = \frac{\hat{\psi}}{SE_{\hat{\psi}}} = \frac{7}{2.19} \approx 3.2

**Step 5: Conclusion**

If the critical value of :math:`t` at 12 degrees of freedom (for :math:`N - k = 15 - 3 = 12`) is 2.18 for :math:`\alpha = 0.05`, the calculated :math:`t`-statistic (3.2) exceeds the critical value. 

Thus, we **reject the null hypothesis** and conclude that Group 1’s mean is significantly lower than the combined means of Groups 2 and 3.

2. **Multiple Comparisons (Post-Hoc Tests)**
--------------------------------------------

When no specific hypotheses are made before the analysis, **post-hoc tests** are used to compare **all pairs of group means**. These comparisons must control for the **Type I error rate** since many pairwise comparisons increase the chance of false positives.

.. image:: /images/0910.png

**Example: Pairwise Comparisons Using Bonferroni Correction**

Let’s use the same three groups:

- Group 1: :math:`\bar{X}_1 = 10`, :math:`n_1 = 5`  
- Group 2: :math:`\bar{X}_2 = 12`, :math:`n_2 = 5`  
- Group 3: :math:`\bar{X}_3 = 15`, :math:`n_3 = 5`  

**Step 1: Compute Pairwise Differences**

1. Group 1 vs. Group 2:

   .. math::
      \bar{X}_1 - \bar{X}_2 = 10 - 12 = -2

2. Group 1 vs. Group 3:

   .. math::
      \bar{X}_1 - \bar{X}_3 = 10 - 15 = -5

3. Group 2 vs. Group 3:

   .. math::
      \bar{X}_2 - \bar{X}_3 = 12 - 15 = -3

**Step 2: Calculate the Standard Error (SE) for Each Pair**

.. math::
   SE = s_p \sqrt{\frac{2}{n}} = 2 \sqrt{\frac{2}{5}} = 2 \times 0.632 = 1.26

**Step 3: Compute t-Statistics for Each Pair**

1. Group 1 vs. Group 2:

   .. math::
      t = \frac{-2}{1.26} \approx -1.59

2. Group 1 vs. Group 3:

   .. math::
      t = \frac{-5}{1.26} \approx -3.97

3. Group 2 vs. Group 3:

   .. math::
      t = \frac{-3}{1.26} \approx -2.38

**Step 4: Apply Bonferroni Correction**

- **Bonferroni adjusted significance level**:

  .. math::
     \alpha_{\text{adjusted}} = \frac{0.05}{3} \approx 0.0167

**Step 5: Conclusion**

- Compare each :math:`t`-statistic to the critical value for :math:`\alpha = 0.0167` with 12 degrees of freedom.
- If a :math:`t`-statistic exceeds the critical value, the corresponding pair of group means is **significantly different**.

Why Conduct Follow-Up Procedures?
---------------------------------

After an ANOVA F-test, we know that at least one group mean differs from the others, but:

- **Contrasts** help test specific, pre-planned hypotheses that are most relevant to our research questions. They are more **powerful** because they focus only on selected comparisons.
- **Post-hoc tests** allow us to explore **all pairwise comparisons** when we have no prior hypotheses. They provide a comprehensive understanding of the group differences while controlling for **Type I error**.

Both procedures can provide valuable insights that the ANOVA F-test alone cannot offer.

.. image:: /images/0911.png

Key Concepts of the LSD Method
------------------------------

- **Purpose**:  
  The **LSD method** identifies which pairs of means are significantly different after an ANOVA test shows that at least one group mean differs from the others.

- **No Adjustment for Multiple Comparisons**:  
  Unlike other post-hoc tests (e.g., Bonferroni correction or Tukey’s HSD), LSD **does not control for Type I error** when making many pairwise comparisons. This makes it **more liberal** (i.e., more likely to find differences) but at the cost of increased Type I error risk.

Steps of the LSD Method (Optional)
----------------------------------

1. **Conduct ANOVA**:
   - Perform a one-way ANOVA to determine if there is a significant overall difference between the group means.
   - If the ANOVA is significant (p-value < 0.05), proceed to the LSD pairwise comparisons.

2. **Calculate the LSD Value for Each Pair of Means**:
   The LSD test uses the **pooled standard deviation** (or the square root of the **Mean Square Within (MSW)**) from the ANOVA.

   The formula for the **LSD value** is:

   .. math::
      LSD = t_{\alpha, df_{\text{within}}} \times \sqrt{MSW \left(\frac{1}{n_1} + \frac{1}{n_2}\right)}

   where:
   - :math:`t_{\alpha, df_{\text{within}}}` is the critical value of the **t-distribution** at the chosen significance level :math:`\alpha` with the **within-group degrees of freedom** from ANOVA.
   - :math:`MSW` is the **Mean Square Within** from the ANOVA.
   - :math:`n_1` and :math:`n_2` are the sample sizes of the two groups being compared.

3. **Compute the Difference Between Each Pair of Group Means**:
   For each pair of group means, calculate:

   .. math::
      \Delta \bar{X} = \bar{X}_1 - \bar{X}_2

4. **Compare the Absolute Difference to the LSD Value**:
   - If :math:`|\Delta \bar{X}| > LSD`, the difference between the two means is **statistically significant**.
   - If :math:`|\Delta \bar{X}| \leq LSD`, the difference is **not significant**.

Example of LSD Calculation
---------------------------

Let’s use the following data:

.. list-table:: Group Data for LSD Example
   :widths: 10 20 10
   :header-rows: 1

   * - Group
     - Mean (:math:`\bar{X}`)
     - Size (:math:`n`)
   * - 1
     - 10
     - 5
   * - 2
     - 13
     - 5
   * - 3
     - 17
     - 5


From ANOVA:
- **MSW** = 2.5
- **Degrees of freedom** (within) = 12

**Step 1: Calculate the LSD Value**

For a 5% significance level (:math:`\alpha = 0.05`) and 12 degrees of freedom, the critical value from the t-distribution is approximately :math:`t_{0.05, 12} = 2.18`.

.. math::
   LSD = 2.18 \times \sqrt{2.5 \left(\frac{1}{5} + \frac{1}{5}\right)}
   = 2.18 \times \sqrt{2.5 \times 0.4}
   = 2.18 \times \sqrt{1.0} = 2.18

**Step 2: Compute Pairwise Differences**

1. **Group 1 vs Group 2**:

   .. math::
      \Delta \bar{X} = 10 - 13 = -3

   :math:`|-3| = 3 > 2.18`, so the difference is **significant**.

2. **Group 1 vs Group 3**:

   .. math::
      \Delta \bar{X} = 10 - 17 = -7

   :math:`|-7| = 7 > 2.18`, so the difference is **significant**.

3. **Group 2 vs Group 3**:

   .. math::
      \Delta \bar{X} = 13 - 17 = -4

   :math:`|-4| = 4 > 2.18`, so the difference is **significant**.


Conclusion and Limitations of LSD
---------------------------------

The **LSD method** is easy to use and provides quick insights into which groups differ significantly. However, because it performs multiple pairwise t-tests without adjusting the significance level, it **does not control for Type I error** inflation when many comparisons are made.

If you expect to make many comparisons or want stricter control of Type I error, consider using other post-hoc tests such as **Tukey’s HSD** or **Bonferroni correction**.



Week 08: Mid-term Exam Review
=============================

**Probability Statements Related Questions**

In Example 6.15, we see probability statements such as :math:`P(Z \geq 1.05)` and :math:`P(Z \leq -1.05)`. For a two-sided alternative hypothesis test, the P-value is calculated as :math:`2 \times P(Z \geq 1.05)` or :math:`2 \times P(Z \leq -1.05)` because we know that :math:`P(Z \geq 1.05)` and :math:`P(Z \leq -1.05)` give us the same values. This happens because the areas under the left and right tails of the standard normal density curve are identical, as it is symmetric around zero.

Later, you will encounter probability statements like :math:`P(T \geq \text{test statistic})` or :math:`P(F \geq \text{test statistic})`. The uppercase :math:`P` indicates probability, which in this context is equivalent to the area under the density curve. The variables :math:`Z`, :math:`T`, and :math:`F` represent random variables that follow the standard normal, Student’s t, and F distributions, respectively.

Why do we use these random variables? When we draw different samples and calculate sample statistics such as the sample mean (:math:`\bar{x}`), the values will vary across samples. These sample means are realizations (draws) from a random variable with a particular distribution. If the population standard deviation is known, the sample mean follows a normal distribution. To denote this sample mean as a random variable, we use the notation :math:`\bar{X}`. We can then ask the probability that :math:`\bar{X}` is greater than or equal to some number, usually the test statistic calculated in the hypothesis testing context. In Example 6.15, :math:`\bar{x} = 14.3`. 

However, we cannot directly compute :math:`P(\bar{X} \geq 14.3)` because there is no table for this specific distribution. So, we transform both sides of the inequality. The random variable :math:`\bar{X}` becomes :math:`\left(\frac{\bar{X} - \mu_0}{\sigma/\sqrt{n}}\right)`, which follows the standard normal distribution :math:`Z`. The right-hand side becomes :math:`\left(\frac{14.3 - \mu_0}{\sigma/\sqrt{n}}\right) = 1.05`, leading to the calculation of the Z-statistic.

Now, the probability statement becomes :math:`P(Z \geq 1.05)`, meaning you are comparing the observed test statistic (the value you calculated from the sample) to the random variable :math:`Z`, which represents the entire Z-distribution. This represents the probability of observing a value from the Z-distribution greater than your test statistic, given that the null hypothesis is true. This is the meaning of the P-value. For two-sided testing, we use :math:`2 \times P(Z \geq 1.05)` to account for the two extremes in both tails.

**Using the Last Row of the T Table**
-------------------------------------

When using the T-distribution, be aware that the last row of the T table corresponds to large degrees of freedom and approaches the values of the standard normal distribution.

**Box Plot, Modified Box Plot, and Side-by-Side Boxplot**
---------------------------------------------------------

Refer to Chapter 1.3, Example 1.26 and 1.27 for examples. Box plots are graphical representations of the distribution of data, showing the median, quartiles, and potential outliers. Modified box plots highlight potential outliers distinctly.

**Density Curves and Skewness**
-------------------------------

Skewness is easily identified by checking the mean and median. If the mean is larger than the median, the distribution is right-skewed. If the mean is smaller than the median, the distribution is left-skewed.

**Observational Study vs. Experimental Study**
----------------------------------------------

In an **observational study**, researchers simply observe subjects and measure variables of interest without manipulating conditions. They gather data based on naturally occurring variables.

In an **experimental study**, researchers impose a treatment or condition on subjects to study its effects. They control the explanatory variable and observe the response. Experiments allow researchers to determine cause-and-effect relationships by isolating the treatment's effect.

**Design of Experiments and Sampling Design**
---------------------------------------------

- **Experimental Design**: Refers to how subjects are assigned to different treatment groups in an experiment. It involves how we allocate subjects to treatments, ensure randomization, and control variables.
  
- **Sampling Design**: Refers to how the sample is selected from the population. It deals with drawing the sample that will be used in the study, not how treatments are assigned.

**Terms Associated with Experimental Design**:
  
- **Experimental Units**: The individuals, animals, or objects involved in an experiment.
  
- **Subjects**: Human experimental units.
  
- **Treatments**: Conditions applied to the experimental units.
  
- **Outcomes**: Results or measurements observed to compare treatments.
  
- **Factors**: Explanatory variables manipulated to observe their causal effects.
  
- **Blocking Variables**: Variables that are not manipulated, used to control existing variation. They represent characteristics or conditions that experimental units already possess.
  
- **Levels of a Factor**: Specific values or categories of a factor.
  
- **Control Group**: Group receiving no treatment or a standard treatment, used as a baseline.
  
- **Treatment Group**: Group receiving the experimental condition.
  
- **Randomization**: Using chance to assign subjects to treatments, avoiding bias.
  
- **Placebo Effect**: Perceived improvement due to receiving a dummy treatment.
  
- **Comparative Experiment**: Experiment comparing multiple treatments, often including a control group.
  
- **Matched Pairs Design**: Design where subjects are paired based on characteristics and each pair is assigned different treatments.
  
- **Block Design**: Experimental units are grouped into blocks, and randomization occurs within blocks.
  
- **Completely Randomized Design**: All experimental units are randomly assigned to treatments without restriction.

**Terms Associated with Sampling Design**:
  
- **Population**: The entire group being studied.
  
- **Sample**: A subset of the population used to draw conclusions about the whole.
  
- **Simple Random Sample (SRS)**: A sampling method where each individual has an equal chance of selection.
  
- **Stratified Random Sample**: Population divided into strata, and an SRS is taken from each stratum.
  
- **Multistage Random Sample**: Selection happens in stages, often used for large populations.
  
- **Sampling Frame**: List or set of items from which the sample is drawn.
  
- **Undercoverage**: Sampling bias due to missing groups in the population.
  
- **Nonresponse**: When individuals in the sample cannot be contacted or refuse to participate.
  
- **Response Bias**: Bias due to the behavior of respondents or interviewers.
  
- **Voluntary Response Sample**: Participants choose themselves, leading to bias.
  
- **Systematic Random Sample**: Every nth item is chosen after a random starting point.


Week 07: Inference for Means
============================

**Student's** :math:`t` **distribution**

.. image:: /images/0701.png

In real applications, we usually don't know the value of :math:`\sigma`, hence we cannot calculate the :math:`z` statistics directly.

.. image:: /images/0705.png

We need to replace the standard deviation :math:`\sigma` with standard error :math:`s`.

.. image:: /images/0703.png

Hence, we derive our one-sample :math:`t` statistic:

.. image:: /images/0704.png

We then establish the one-sample :math:`t` confidence interval:

.. image:: /images/0706.png

**Comparing with** :math:`t`

.. image:: /images/0702.png

**Example 7.1: Delivery Time for Robot Service**

Additionally, we apply our one-sample :math:`t` test:

.. image:: /images/0707.png

**Examples 7.2 and 7.3: Robot Delivery Service**

**Matched Pairs** :math:`t` **Procedures**

The robot delivery problem in Example 7.1 concerns only a single population. Comparative studies are usually preferred over single-sample investigations because they offer protection against confounding. Therefore, inference about a parameter of a single distribution is less common than comparative inference.

One common comparative design makes use of single-sample procedures. In a matched pairs study, subjects are matched in pairs, and their outcomes are compared within each matched pair.

- **Paired Data:** This arises when the data are naturally paired, such as in studies where the same subjects are measured twice under different conditions (before-and-after studies), or when subjects are matched in pairs based on similar characteristics (e.g., age, baseline characteristics).

- **Before-and-After Studies:** Common in medical, psychological, or social research where the interest lies in observing the effect of a treatment or intervention over time on the same group of subjects.

**Some examples:**

- Pre-test/Post-test Design: Measuring students' math scores before and after attending a tutoring program.

- Medical Intervention: Testing blood pressure levels before and after administering a new medication to the same patients.

- Productivity Study: Measuring employees' productivity before and after implementing new office software for the same group of employees.

**Example 7.7: The Effect of Altering a Software Parameter**

.. note::

   A lack of statistical significance does not prove the null hypothesis is true.

**Example 7.8**

.. image:: /images/0708.png

**Robustness and Non-Normal Populations**

.. image:: /images/0709.png

.. image:: /images/0710.png

.. image:: /images/0711.png

**Comparing Two Means**

Used when comparing two independent groups. Each sample is collected independently from the other, typically from two distinct populations. Two independent samples assess the same response variable.

**Some examples:**

- Comparing Two Diet Plans: Comparing the average weight loss between two groups, one following Diet A and the other following Diet B.

- Marketing Strategy Comparison: Comparing sales performance between two regions where different advertising campaigns were conducted.

- Comparing Two Schools’ Performances: Comparing average SAT scores between students from two different high schools.

- Comparing Male and Female Incomes: Comparing the average incomes for male and female workers across different occupations.

.. image:: /images/0712.png

**Example 7.13: Heights of 10-Year-Old Girls and Boys**

.. image:: /images/0713.png

.. image:: /images/0714.png

**Example 7.16: Is There an Improvement?**

.. image:: /images/0715.png

**The Pooled Two-Sample** :math:`t` **Procedures**

Two normal populations whose means we want to compare are assumed to have the same standard deviation.

.. image:: /images/0716.png

- **Increased Precision**: The pooled two-sample t-test uses a combined estimate of variability (standard deviation), which provides a more precise estimate of the population standard deviation when the two groups are assumed to have the same variance. This pooled variance is a weighted average of the two sample variances, where the weights are the degrees of freedom of each sample.

- **Greater Power**: Because the pooled t-test uses this more precise estimate of variability, it typically offers greater statistical power. This means there is a higher chance of correctly rejecting the null hypothesis when it is false (i.e., detecting a true difference between the group means when one exists).

.. image:: /images/0717.png

**Sample Size Calculations**

Usually, we prefer narrow confidence intervals because they provide a better indication of the range of the parameter value. Therefore, we start with a fixed value of margin of error. We know that we can adjust :math:`n` to increase or decrease the margin of error. Thus, we establish a procedure to find the desired :math:`n` that will give us the desired width of confidence intervals at a specific significance level :math:`\alpha`.

.. image:: /images/0718.png

.. image:: /images/0719.png

**Calculating Power**

First, we calculate the probability of a Type II error, which is the probability that we fail to reject :math:`H_0` when :math:`H_a` is true. The power is then 1 minus this probability.

`Example: How to calculate Power <https://online.stat.psu.edu/stat415/book/export/html/845>`_


Week 06: Intro to Inference
=============================

A lot of times, in real-world applications, we have a sample of data points, observations, outcomes, or cases. However, we don't know the values of parameters (e.g., :math:`\mu` and :math:`\sigma`) for the population. So, we need to use the information from the sample to *guess* the values of parameters. This procedure/process is statistical learning or statistical inference.

Let's first use the textbook Example 6.3 SATM score to illustrate the process. We have only one parameter, which is the population mean, :math:`\mu`, which we don't know in this case and need to estimate.

One approach is that we can record the scores for all the students (:math:`N = 489{,}650`) in the population, and then calculate :math:`\mu`. But this would be time-consuming and costly.

Another, more applicable approach is that we can draw a sample from the whole population, in this case :math:`n = 500` students, and use the sample mean :math:`\bar{x}` to estimate or get a rough idea of the population mean :math:`\mu`.

The sample mean :math:`\bar{x}` is a natural estimator of the unknown population mean :math:`\mu` by our intuition. What's more important, it is an unbiased estimator, and the sample mean must approach the population mean as the size of the sample grows. This means the sample mean has some good properties.

In the textbook, for the first sample, Sample 1, we have :math:`\bar{x} = 505`. From last time, we know that if we draw a number of different samples and calculate the sample means for each sample, then these sample means will form an approximate normal distribution with mean :math:`\mu` and standard deviation :math:`\frac{\sigma}{\sqrt{n}}`.

Because that fact is normal, we know that 95% of these :math:`\bar{x}` will fall into the range of :math:`\left( \mu - 2 \times \frac{\sigma}{\sqrt{n}},\ \mu + 2 \times \frac{\sigma}{\sqrt{n}} \right)`, as shown in the graph below:

.. image:: /images/0601.png

We have:

.. math::

   2 \times \frac{\sigma}{\sqrt{n}} = 2 \times \frac{100}{\sqrt{500}} = 2 \times 4.5 = 9.

If :math:`\bar{x}` lies within :math:`(\mu - 9,\ \mu + 9)`, we can also say that :math:`\mu` lies within :math:`(\bar{x} - 9,\ \bar{x} + 9)`.

**Given:**

.. math::

   \bar{x} \in (\mu - 9,\ \mu + 9)

This means:

.. math::

   \mu - 9 < \bar{x} < \mu + 9

**Step 1:** Subtract :math:`\mu` from all parts of the inequality.

.. math::

   (\mu - 9) - \mu < \bar{x} - \mu < (\mu + 9) - \mu \\
   -9 < \bar{x} - \mu < 9

**Step 2:** Multiply all parts by :math:`-1` to switch the direction of the inequalities.

.. math::

   -1 \times (-9) > -1 \times (\bar{x} - \mu) > -1 \times 9 \\
   9 > \mu - \bar{x} > -9

This simplifies to:

.. math::

   -9 < \mu - \bar{x} < 9

**Step 3:** Add :math:`\bar{x}` to all parts of the inequality.

.. math::

   -9 + \bar{x} < \mu - \bar{x} + \bar{x} < 9 + \bar{x} \\
   \bar{x} - 9 < \mu < \bar{x} + 9

**Conclusion:**

.. math::

   \mu \in (\bar{x} - 9,\ \bar{x} + 9)

Then, we have a confidence interval, or 95% confidence interval. So what does this **95%** mean?

It means that if we draw 100 samples and calculate 100 sample means, and then form 100 of these confidence intervals, 95 times this interval will contain the population mean :math:`\mu`. But for a single confidence interval, we actually do not know whether this interval will contain :math:`\mu` or not. For a single confidence interval, there are only two cases: it contains :math:`\mu` or it does not contain :math:`\mu`.

.. image:: /images/0602.png

Then we can calculate any confidence level intervals.

.. image:: /images/0603.png

.. image:: /images/0604.png

If we don't know :math:`\sigma`, then we can get an estimate of it.

**Example 6.7**

**Estimation (Confidence Intervals)**

- **Purpose:** To estimate population parameters.
- **Method:** Uses confidence intervals to provide a range of plausible values for a population parameter, such as a mean or proportion. The confidence interval tells us, with a certain degree of confidence, where the true parameter value lies.

**Hypothesis Testing (Tests of Significance)**

- **Purpose:** To assess evidence provided by the data in favor of some claim about the population parameters.
- **Method:** Uses tests of significance to determine whether observed data can reasonably occur under a specified null hypothesis. This involves calculating a test statistic, comparing it to a theoretical distribution, and computing a p-value to make a decision about the hypothesis.

The null hypothesis (:math:`H_0`) is always set up to represent the status quo or no change, meaning it reflects the assumption that there is no effect or no difference from the baseline condition. For example, :math:`H_0: \mu = 170\ \text{cm}`.

In hypothesis testing, we try to gather evidence to reject the null hypothesis. Therefore, we start by assuming that nothing has changed.

The alternative hypothesis (:math:`H_a`) is what you're trying to find evidence for. For example, :math:`H_a: \mu \ne 170\ \text{cm}` (two-sided alternative) or :math:`H_a: \mu > 170\ \text{cm}` (one-sided alternative).

Once we form the pair of null and alternative hypotheses, we can assume that if :math:`H_0` is true, under this condition, we calculate the test statistic, such as the z-score from the sample mean.

If it is a two-sided test, then we will look at the areas at the two tails based on z and :math:`-z` values. If it is a one-sided test, we will look at the area at one of the tails depending on the z value and the direction of the inequality sign of :math:`H_a`. This area is also called the p-value.

.. image:: /images/0605.png

**Example 6.12 and Example 6.14**

.. image:: /images/0606.png

.. note::

   The p-value is not the probability that the null hypothesis is true.

Once we have the p-value, we can say we can reject the null at :math:`\alpha` level, or we do not have evidence to reject the null at :math:`\alpha` level. Here, :math:`\alpha` is a small number, and the p-value is the smallest :math:`\alpha` at which you would reject :math:`H_0`.

**Use and Abuse of Tests**

.. image:: /images/0607.png

`Video on p-values <https://www.youtube.com/watch?v=i60wwZDA1CI>`_

**Inference as a Decision**

From previous sections, we know that the test statistic is random. So there is the probability that we make the wrong conclusion. If we use the test to make a decision, we could end up with errors. The first error we encounter is Type I error, which means :math:`H_0` is right, but we reject it. There is another type of error, which is the Type II error, where :math:`H_0` is wrong (:math:`H_a` is right), but we fail to reject it.

.. image:: /images/0609.png

.. image:: /images/0608.png

.. image:: /images/0611.png

.. image:: /images/0612.png

.. image:: /images/0613.png

We cannot make both Type I and Type II errors small.

.. image:: /images/0610.png

**Example: A Judge Sentencing a Defendant**

In the context of a judge sentencing a defendant, the concepts of Type I and Type II errors can be illustrated using the analogy of the judicial decision-making process:

**Type I Error**

- **Definition**: Incorrectly rejecting the null hypothesis when it is true.
- **Judicial Context**: Convicting an innocent person. Here, the null hypothesis (:math:`H_0`) is that the defendant is innocent ("innocent until proven guilty"). A Type I error occurs when the judge (or jury) incorrectly rejects this hypothesis and concludes that the defendant is guilty, despite their innocence.

**Type II Error**

- **Definition**: Failing to reject the null hypothesis when it is false.
- **Judicial Context**: Acquitting a guilty person. In this scenario, the null hypothesis is that the defendant is innocent, and a Type II error occurs when this hypothesis is not rejected despite it being false, meaning the guilty defendant is wrongly found not guilty and is acquitted.

**Implications in Legal Settings**

- **Priority of Errors**: In many legal systems, especially in criminal law, there is a strong emphasis on minimizing Type I errors. The principle "it is better that ten guilty persons escape than that one innocent suffer" (often attributed to English jurist William Blackstone) highlights the preference for avoiding wrongful convictions (Type I errors) even at the risk of increasing wrongful acquittals (Type II errors).
- **Balancing Risks**: However, minimizing Type I errors may increase Type II errors, depending on the standards of evidence required to convict (e.g., "beyond a reasonable doubt" in the United States). The legal system must balance these risks to protect the innocent while also ensuring that the guilty are appropriately convicted.

.. image:: /images/0614.png


Week 05: Ch5.3 Sampling Distributions for Counts and Proportions
================================================================

**Introduction to Bernoulli and Binomial Random Variables**

**Bernoulli Random Variable**

Consider a population of 10,000 coin tosses where each coin has a probability :math:`p` of landing heads (success) and :math:`1 - p` of landing tails (failure). Each toss can be described as a Bernoulli random variable, where:

.. math::
   S_i =
   \begin{cases}
   1, & \text{if heads (success)} \\
   0, & \text{if tails (failure)}
   \end{cases}

The probability distribution for each individual toss is:

.. list-table:: Probability Distribution of a Coin Toss
   :widths: 25 75
   :header-rows: 1

   * - Outcome
     - Probability
   * - Heads (1)
     - :math:`p`
   * - Tails (0)
     - :math:`1 - p`


We can now randomly sample from these 10,000 tosses to form a sample. Let the sample size be :math:`n`.

**Binomial Random Variable**

The sum of :math:`n` independent Bernoulli trials is a Binomial random variable. Let :math:`X` represent the total number of heads (successes) in the sample. This is a Binomial distribution with parameters :math:`n` and :math:`p`:

.. math::
   X \sim Binomial(n, p)

If we define heads as 1 and tails as 0, the number of heads (successes) follows the Binomial distribution. The mean and standard deviation of :math:`X` are:

.. math::
   \mu_X = np, \quad \sigma_X = \sqrt{np(1 - p)}

**Proportion as a Random Variable**

We can also define the proportion of successes in the sample. Let :math:`\hat{p}` be the proportion of heads, defined as:

.. math::
   \hat{p} = \frac{X}{n}

This is another random variable that follows approximately a normal distribution (for large :math:`n`) with mean and standard deviation:

.. math::
   \mu_{\hat{p}} = p, \quad \sigma_{\hat{p}} = \sqrt{\frac{p(1 - p)}{n}}

**Example 1:** Probability of Count Using Binomial and Normal Approximation

Let's calculate the probability that the number of heads (successes) is less than or equal to some number, say :math:`k`. We will do this using both the exact Binomial distribution and the approximate normal distribution.

**Binomial Distribution**

The exact probability for the count is:

.. math::
   P(X \leq k) = \sum_{i=0}^{k} \binom{n}{i} p^i (1-p)^{n-i}

**Normal Approximation**

The normal approximation for large :math:`n` is:

.. math::
   P(X \leq k) \approx \Phi\left(\frac{k - np}{\sqrt{np(1-p)}}\right)

Where :math:`\Phi` is the CDF of the standard normal distribution.

**Example 2:** Probability of Proportion Using Binomial and Normal Approximation

For the proportion of heads, :math:`\hat{p}`, we can calculate a similar probability. Suppose we want to calculate the probability that the proportion of heads is less than or equal to a value :math:`\hat{p}_k`.

**Binomial Proportion Distribution**

The exact probability for the proportion is:

.. math::
   P\left(\hat{p} \leq \hat{p}_k\right) = P\left(X \leq n \hat{p}_k\right)

**Normal Approximation**

The normal approximation for large :math:`n` is:

.. math::
   P\left(\hat{p} \leq \hat{p}_k\right) \approx \Phi\left(\frac{\hat{p}_k - p}{\sqrt{\frac{p(1-p)}{n}}}\right)

**Graphs:** :math:`n = 50`, :math:`p = 0.5`.

.. image:: /images/0507.png

.. image:: /images/0508.png

.. image:: /images/0509.png

**Example 5.25, Figure 5.20**

.. image:: /images/0510.png

.. image:: /images/0511.png

**Poisson Distribution**

The **Poisson distribution** is a probability distribution that models the number of successes (events) occurring within a fixed interval of time or space when those events happen with a constant mean rate and are independent of the time since the last event.

**Key Properties of the Poisson Setting**

1. **Independence**: The number of successes (events) that occur in two non-overlapping intervals are independent of each other. For example, the number of phone calls received in the morning doesn’t affect the number of calls in the evening.
   
2. **Equal Probability**: The probability of a success occurring in any unit of measure (whether it's time, space, or another unit) is the same for all units of equal size. For instance, the likelihood of getting 3 calls in 10 minutes is proportional to the time length, and this probability doesn't change from one 10-minute block to another.

3. **Rare Events**: The probability that more than one event will occur in a very small unit of measure is negligible. Events happen one at a time in these intervals, which is why it is ideal for modeling rare events.

**When to Use the Poisson Distribution**

The Poisson distribution is ideal when you’re counting the number of times an event happens over a fixed interval, such as:

- The number of emails received in an hour.
- The number of accidents at a particular intersection during a week.
- The number of typographical errors on a page of text.

**Poisson Distribution Formula**

The probability that exactly :math:`k` events occur in an interval, where the average number of events is :math:`\mu`, follows the Poisson distribution:

.. math::
   P(X = k) = \frac{e^{-\mu} \mu^k}{k!}

Where:

- :math:`\mu` is the average number of successes in the given interval.

- :math:`k` is the number of successes (events).

- :math:`e` is approximately 2.718 (Euler's number).

The **mean** of the Poisson distribution is :math:`\mu`, and the **standard deviation** is :math:`\sqrt{\mu}`.

**Example Scenario**

Let’s say we want to model the number of customer arrivals at a store in a 1-hour period, and the average number of customers arriving is 5 per hour. This fits the Poisson distribution because:

1. Customer arrivals are independent (one arrival doesn’t influence another).
2. The probability of an arrival is proportional to time (10 minutes is half as likely as 20 minutes for a given number of customers).
3. The likelihood of more than one customer arriving at the exact same time is very small.

In this case, the average number of arrivals :math:`\mu` is 5, and we can use the Poisson distribution to calculate the probability of, say, exactly 3 customers arriving in a given hour:

.. math::
   P(X = 3) = \frac{e^{-5} 5^3}{3!} \approx 0.14

This means there’s about a 14% chance that exactly 3 customers will arrive in one hour.

.. image:: /images/0512.png

**Example 5.32**

Week 05: Ch5.2 The Sampling Distribution of a Sample Mean
=========================================================

**Revisit the sampling distribution of sample mean example**

**Population:** 4,000 students' heights, drawn from a normal distribution with mean :math:`\mu = 170` centimeters and standard deviation :math:`\sigma = 10` cm.

.. image:: /images/0501.png

Now draw 50 samples, each consisting of 50 students (:math:`x_1, x_2, \ldots, x_{49}, x_{50}`). Here we can observe that each individual measurement, say :math:`x_1`, varies across these 50 samples. Therefore, we denote it as :math:`X_1` to indicate it is a random variable, whose realization depends on its random selection from the population.

**Sample 1:**

.. image:: /images/0502.png

**Sample 2:**

.. image:: /images/0503.png

Continuing this process, we can calculate the sample mean, :math:`\bar{x}`, for each of the 50 samples and construct a histogram or distribution of these sample means. We then overlay the density curve on this histogram. Finally, we overlay another normal density curve with mean :math:`\mu` and standard deviation :math:`\frac{\sigma}{\sqrt{n}}` onto the graph.

.. image:: /images/0504.png

Ultimately, we can compare the distribution of the population and the distribution of the sample means.

.. image:: /images/0505.png

**Questions to Consider:**
*What if our population comes from a distribution other than normal?*

**Calculations and Definitions:**

**Population Distribution**

The population distribution of a variable is the distribution of its values for all members of the population. The population distribution is also the probability distribution of the variable when we choose one individual at random from the population.

**Facts About Sample Means**

1. Sample means are less variable than individual observations.
2. Sample means are centered on the population mean.
3. For large :math:`n`, the distribution of sample means is close to Normal.

**Sampling Distribution of a Sample Mean: Normal Population Distribution**

If a population has the :math:`N(\mu, \sigma)` distribution, then the sample mean :math:`\bar{x}` of :math:`n` independent observations has the :math:`N\left(\mu, \frac{\sigma}{\sqrt{n}}\right)` distribution.

**Mean and Variance of Sampling Distribution of a Sample Mean**

The sample mean of an SRS of size :math:`n` is given by:

.. math::
   \bar{x} = \frac{1}{n} \sum_{i=1}^{n} X_i

Where :math:`X_1, X_2, \ldots, X_n` are the observations in the sample.

If the population has mean :math:`\mu`, then :math:`\mu` is the mean of the distribution of each observation :math:`X_i`. To derive the mean of :math:`\bar{x}`, the rules for means of random variables are applied:

.. math::
   \mu_{\bar{x}} = \frac{1}{n} (\mu_{X_1} + \mu_{X_2} + \ldots + \mu_{X_n})
                 = \frac{1}{n} (n\mu)
                 = \mu

Thus, the mean of :math:`\bar{x}` is the same as the mean of the population, making :math:`\bar{x}` an unbiased estimator of the unknown population mean :math:`\mu`.

Assuming the observations are independent, the rule for variances of independent random variables gives:

.. math::
   \sigma_{\bar{x}}^2 = \frac{1}{n^2} \left(\sigma_{X_1}^2 + \sigma_{X_2}^2 + \ldots + \sigma_{X_n}^2\right)
                      = \frac{1}{n^2} (n\sigma^2)
                      = \frac{\sigma^2}{n}

The variance of the sample mean :math:`\bar{x}` decreases with the size of the sample :math:`n`, which demonstrates the statistical principle that averaging reduces variability.

**Decrease in Standard Deviation with Sample Size**

Because the standard deviation of :math:`\bar{x}` is :math:`\frac{\sigma}{\sqrt{n}}`, the standard deviation of the statistic decreases in proportion to the square root of the sample size. This means, for example, that a sample size must be multiplied by 4 in order to divide the statistic's standard deviation in half. By comparison, a sample size must be multiplied by 100 in order to reduce the standard deviation by a factor of 10.

**Central Limit Theorem**

Draw an SRS of size :math:`n` from any population with mean :math:`\mu` and finite standard deviation :math:`\sigma`. When :math:`n` is large, the central limit theorem states that the sampling distribution of the sample mean :math:`\bar{x}` is approximately Normal:

.. math::
   \bar{x} \sim N\left(\mu, \frac{\sigma}{\sqrt{n}}\right)

**Example 5.6 Standard Deviations for Sample Means of Visit Lengths**

.. image:: /images/0506.png

**Example 5.7, 5.8, and 5.11**

Week 04: Ch1.4 Density Curves and Normal Distributions
======================================================

**The normal distribution is fully defined by its mean 
:math:`\mu` and variance :math:`\sigma^2` because:**

- **Mean** :math:`\mu` determines the center or location of the distribution (where the peak of the bell curve is).
- **Variance** :math:`\sigma^2` (or **standard deviation** :math:`\sigma`) determines the spread or scale of the distribution (how wide or narrow the bell curve is).

Since the shape of the normal distribution is always symmetric and bell-shaped, the only variables we need to adjust are its center and spread, which are described by the mean and variance.

.. image:: /images/0405.png

**Questions to Consider:** 

- Why is the **normal distribution** important in statistics and data analysis?

The **area** under the normal curve to the left of a data point :math:`x`, This area represents the **cumulative probability** of a value being less than or equal to that data point in the distribution. 

**Why We Need to Know This Area:**

- The area helps us calculate the **percentile** of a value, i.e., the percentage of data points that are below a certain value.

.. image:: /images/0407.png

**How to calculate this area?**

If a data point comes from a **standard normal distribution** with a mean of 0 and a standard deviation of 1, we can use the **z-table** to find the area (the cumulative probability) under the curve. 

For data points from other normal distributions (non-standard normals), we can transform the data point into a **z-score**, which standardizes the value. Once transformed, we can use the z-table to find the area for the corresponding z-score.

**What is a Z-Score?**

A **z-score** measures how many **standard deviations** a particular value is from the mean of the dataset. It helps us understand where a data point stands relative to the rest of the distribution. A positive z-score indicates the data point is above the mean, while a negative z-score means it is below the mean.

The formula to calculate the z-score is as follows:

.. image:: /images/0408.png
   :alt: Z-Score Formula

**Examples:**

- A **z-score of 2** means the data point is **2 standard deviations above** the mean.
- A **z-score of -1.5** means the data point is **1.5 standard deviations below** the mean.

Once you have the z-score, use the z-table to find the area (cumulative probability) that corresponds to that score.


**The 68-95-99.7 rule** 

.. image:: /images/0409.png

**SAT Example: Calculate Percentile from a Score**

You scored **1300** on the SAT. The nationwide SAT scores follow a normal distribution with:
- Mean (\ :math:`\mu` ) = **1050**
- Standard deviation (\ :math:`\sigma` ) = **217**

1. **Step 1: Calculate the Z-Score**

   Use the z-score formula:

   .. math::
      z = \frac{x - \mu}{\sigma}

   Where:
   - :math:`x = 1300` (your SAT score),
   - :math:`\mu = 1050` (average SAT score),
   - :math:`\sigma = 217` (standard deviation).

   Substituting the values:

   .. math::
      z = \frac{1300 - 1050}{217} \approx 1.15

2. **Step 2: Use the Z-Table to Find the Percentile**

   A **z-score of 1.15** corresponds to approximately **87.49%** in the z-table. This means you are in the **87th percentile**, meaning about **87.49%** of test-takers scored lower than you.

**Reverse: Find the SAT Score for a Specific Percentile**

Suppose you want to be above the **90th percentile**. Here's how to calculate the score you need:

1. **Step 1: Find the Z-Score for the 90th Percentile**

   From the z-table, the **90th percentile** corresponds to a **z-score of 1.28**.

2. **Step 2: Convert the Z-Score to an SAT Score**

   Use the reverse z-score formula:

   .. math::
      x = \mu + z \cdot \sigma

   Substituting the values:

   .. math::
      x = 1050 + 1.28 \times 217 \approx 1328

   To score above the **90th percentile**, you would need to score approximately **1328** on the SAT.

**Normal quantile plot**

.. image:: /images/0410.png

.. image:: /images/0411.png

Week 04: Ch1.3 Describing Distributions with Numbers
====================================================

The IQ dataset:
5, 6, 16, 18, 18, 20, 24, 26, 27, 34, 42, 51, 54, 59, 64, 70, 72, 73, 78, 80

1. **Mean**:

   .. math::

      \mu = \frac{1}{n} \sum_{i=1}^{n} x_i

   Example:

   .. math::

      \mu = \frac{5 + 6 + 16 + 18 + 18 + ... + 70 + 72 + 73 + 78 + 80}{20} = 40.1

2. **Median**:

   If n is odd, the median is the middle value. If n is even, the median is the average of the two middle values.

   Example:

   .. math::

      Median = \frac{27 + 34}{2} = 30.5

3. **Lower Quartile (Q1) / 25th Percentile**:
   
   Q1 is the median of the lower half of the dataset.

   Example:

   .. math::

      Q1 = \frac{18 + 20}{2} = 18.5

4. **Upper Quartile (Q3) / 75th Percentile**:
   
   Q3 is the median of the upper half of the dataset.

   Example:

   .. math::

      Q3 = \frac{64 + 70}{2} = 67

5. **Maximum (Max)**:
   
   The maximum is the largest value in the dataset.

   Example:

   Max = 80

6. **Minimum (Min)**:
   
   The minimum is the smallest value in the dataset.

   Example:

   Min = 5

7. **Interquartile Range (IQR)**:
   
   .. math::

      IQR = Q3 - Q1

   Example:

   .. math::

      IQR = 67 - 18.5 = 48.5

8. **Outlier Threshold (1.5 * IQR)**:
   
   Outliers are below Q1 - 1.5 * IQR or above Q3 + 1.5 * IQR.

   Example:

   .. math::

      Lower Bound = Q1 - 1.5 \times IQR = 18.5 - 1.5 \times 48.5 = -53.25 \\
      Upper Bound = Q3 + 1.5 \times IQR = 67 + 1.5 \times 48.5 = 138.75

   Outliers are any values outside the range (-53.25, 138.75). There are no outliers in this dataset.

9. **Variance** (:math:`s^2`):
   
   .. math::

      s^2 = \frac{1}{n-1} \sum_{i=1}^{n} (x_i - \mu)^2

   Example:

   .. math::

      s^2 = \frac{(5 - 40.1)^2 + (6 - 40.1)^2 + ... + (80 - 40.1)^2}{19} = 706.95

**In general, we can calculate the Pth percentile by following these steps:**

1. **Find the Position**: 

   Use the following formula to determine the position in the sorted dataset:

   .. math::
      \text{Position} = \frac{P}{100} \times (n + 1)

   where:

   - \( P \) is the desired percentile (e.g., 25th percentile for Q1, 50th percentile for the median),

   - \( n \) is the number of data points in the dataset.

2. **Whole Number Position**: 

   - If the position is a whole number, use the corresponding data point at that position directly.

3. **Fractional Position**: 

   - If the position is a fraction (i.e., not a whole number), find the two adjacent data points in the dataset. 

   - Use the values at these adjacent positions and take their average to calculate the percentile.

**Example**:

To find the median (50th percentile) in a dataset with \( n = 8 \) data points, use the formula to find the position:

.. math::
   \text{Position} = \frac{50}{100} \times (8 + 1) = 4.5

Since 4.5 is a fraction, find the 4th and 5th data points in the sorted dataset and take their average for this textbook, the median is calculated as:

.. math::
   \text{Median} = \frac{x_4 + x_5}{2}

This method can be applied to any percentile by changing the value of \( P \). For example, to find the 25th percentile, use \( P = 25 \).

.. image:: /images/0401.png

.. image:: /images/0402.png

.. image:: /images/0403.png

.. image:: /images/0404.png


Week 03: Ch5.1 Bias and Variability, Ch1: Graphing and Numerical Summaries
==========================================================================

Section 5.1 Toward Statistical Inference SUMMARY
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- A number that describes a population is a **parameter**. A number that describes a sample, and is computed from the sample data, is a **statistic**.

- The purpose of sampling or experimentation is usually **statistical inference**: using sample statistics to make statements about unknown parameters.

- A statistic from a probability sample or a randomized experiment varies randomly from sample to sample. The **sampling distribution** of a statistic describes how the statistic varies in these repeated data productions. The sampling distribution answers the question "What would happen if we repeated the sample or experiment many times?" Formal statistical inference is based on the sampling distributions of statistics.

- **Simulation** can be used to imitate the production of many random samples. If we calculate the statistic for each of these samples, their distribution approximates the statistic’s sampling distribution.

- A statistic as an **estimator** of a parameter may suffer from **bias** or from large **variability**. Bias means that the center of the sampling distribution is not equal to the true value of the parameter. The variability of the statistic is described by the spread of its sampling distribution.

- The spread of a statistic is usually reported by giving a **margin of error** for conclusions based on sample results. As the sample size increases, the margin of error decreases.

- Properly chosen statistics from randomized data production designs have no bias resulting from the way the sample is selected or the way the experimental units are assigned to treatments. We can reduce the variability of the statistic by increasing the size of the sample.

- As long as the population is at least 20 times larger than the sample size n, the size of the population has little influence on the variability of a statistic.

Section 5.1 Exercises
^^^^^^^^^^^^^^^^^^^^^

5.1 to 5.4, 5.6, and 5.12

Section 1.1 Data SUMMARY
^^^^^^^^^^^^^^^^^^^^^^^^

- A data set contains information on a number of **cases**. Cases may be customers, companies, subjects in a study, units in an experiment, or other objects.

- For each case, the data give values for one or more **variables**. A variable describes some characteristic of a case, such as a person’s height, gender, or salary. Variables can have different **values** for different cases.

- A **label** is a special variable used to identify cases in a data set.

- Some variables are **categorical**, and others are **quantitative**. A categorical variable places each individual into a category, such as male or female. A quantitative variable has numerical values that measure some characteristic of each case, such as height in centimeters or annual salary in dollars.

- The **key characteristics** of a data set answer the questions Who? (What cases), What? (What variables), and Why? (What purpose)

- Converting a count to a **rate** is an example of **adjusting one variable to create another**.

Section 1.2 Displaying Distributions with Graphs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The distribution of a variable describes how the values of a variable vary from case to case. We can use graphic and numerical descriptions for a distribution. 

**Exploratory data analysis:** the examination of using statistical tools and ideas help us examine data to **describe their main features**. Our focus for this examination is on careful description of the values of the variables in our data set. In many applications, our real interest is in using our descriptions to **predict**. We use the term **predictive analytics** to describe data used in this way.

- Demo: Movie Rating, Categorical

- Demo: Stemplot, Example 1.10

- **Demo: Histogram, Example 1.13**

We can make a histogram first

.. image:: /images/IQ_histogram.png

Then, we can overlay the density curve on the histogram. For the difference between a histogram and a density plot, you can refer to the following resource: `<https://online.stat.psu.edu/stat414/book/export/html/640>`_.

For a density curve, it is always above zero, and the total area under the curve is normalized to one. For each interval, such as 95 to 105, the area is equal to the area of the bar for that interval divided by the total area of all bars.

.. image:: /images/0406.png

.. image:: /images/IQ_density.png

Then, we can analyze the shape of the density. Like a bell shape? The center, mean and median.

.. image:: /images/IQ_mm.png

The blue vertical dashed line indicates the mean, while the green line represents the median. 

Then, we check the tails.

Left tail in semi-transparent blue.

.. image:: /images/IQ_left.png

Right tail in semi-transparent red.

.. image:: /images/IQ_leftright.png


- Demo: Mode, Skewness, and Time Plot

The two graphs below illustrate the different types of skewness. The solid-colored data points are outliers that are distant from the center of the distribution.

.. image:: /images/skewleft.png

.. image:: /images/skewright.png


Special Topic: Current Population Survey (CPS) sampling process
===============================================================

The CPS uses a multistage sampling design to select households across the United States. This process ensures that the survey is representative of the entire population while also being efficient and cost-effective. Below is a step-by-step breakdown of how the sampling works, along with hypothetical numbers to illustrate each stage.

Stage 1: Selection of Primary Sampling Units (PSUs)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**What are PSUs?**

Primary Sampling Units (PSUs) are large geographic areas such as metropolitan areas, counties, or groups of adjacent counties. The U.S. is divided into 2007 PSUs that cover the entire country.

### Step 1: Automatically Include Largest PSUs

- **Automatic Inclusion:** The first step involves automatically selecting the 428 PSUs with the largest populations. These PSUs are selected because they account for a significant portion of the U.S. population and are critical for ensuring that the sample is representative of the country’s population distribution.
  
  **Example:**

  - **Top 428 PSUs:** These might include large metropolitan areas like New York City, Los Angeles, and Chicago, along with other densely populated areas across the country.

### Step 2: Stratify and Sample the Remaining PSUs

**Stratification Process:**

- **Remaining PSUs:** After selecting the 428 largest PSUs, 1579 PSUs remain.
- **Stratification:** These 1579 PSUs are grouped into strata. Stratification is done based on various characteristics, ensuring that the sample captures the diversity of the remaining PSUs. Typical stratification criteria might include:

  - **Geographic location:** (e.g., Northeast, Midwest, South, West)
  - **Urban vs. rural:** (e.g., urban areas, suburban areas, rural areas)
  - **Socio-economic characteristics:** (e.g., income levels, education levels)
  - **Population density:** (e.g., high-density vs. low-density areas)

**Example of Stratification:**

- **Suppose the 1579 PSUs are divided into 5 strata based on geographic location:**

  - Stratum 1: Northeast (300 PSUs)
  - Stratum 2: Midwest (400 PSUs)
  - Stratum 3: South (500 PSUs)
  - Stratum 4: West (279 PSUs)
  - Stratum 5: Rural areas across all regions (100 PSUs)

**Sampling within Each Stratum:**

- Within each stratum, a proportional number of PSUs are randomly selected to ensure that each region is adequately represented in the final sample.

**Example of Selecting 326 PSUs:**

- **From the 5 strata:**

  - Stratum 1 (Northeast): ``300/1579 * 326 ≈ 62`` PSUs selected
  - Stratum 2 (Midwest): ``400/1579 * 326 ≈ 83`` PSUs selected
  - Stratum 3 (South): ``500/1579 * 326 ≈ 103`` PSUs selected
  - Stratum 4 (West): ``279/1579 * 326 ≈ 58`` PSUs selected
  - Stratum 5 (Rural areas): ``100/1579 * 326 ≈ 20`` PSUs selected

- **Total PSUs selected:** ``62 + 83 + 103 + 58 + 20 = 326 PSUs``

**Final Selection:**

- **Total PSUs:** The 428 largest PSUs + 326 selected from the remaining PSUs = **754 PSUs selected** for the CPS.

Stage 2: Selection of Blocks within Each PSU
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**What are Blocks?**

Blocks are smaller geographical areas within each PSU, such as city blocks in urban areas or defined rural areas. Blocks are used to further refine the sampling process within each PSU.

### Step 1: Divide Each PSU into Blocks

- **Division Process:** Each selected PSU is divided into blocks. The number of blocks within each PSU depends on its size and population density.
  
  **Example:**

  - **Urban PSU:** An urban PSU might be divided into 200 blocks.
  - **Rural PSU:** A rural PSU might be divided into 50 blocks.

### Step 2: Stratify and Sample the Blocks

**Stratification Process:**

- **Stratify by Characteristics:** Blocks within each PSU are stratified based on characteristics like:

  - **Ethnic composition:** (e.g., blocks with a high proportion of a certain ethnic group)
  - **Socio-economic status:** (e.g., income levels, housing values)
  - **Housing type:** (e.g., single-family homes, apartments)

**Example of Block Stratification:**

- Suppose an urban PSU is divided into 200 blocks and stratified by income levels into three strata:

  - Stratum 1: High-income blocks (50 blocks)
  - Stratum 2: Middle-income blocks (100 blocks)
  - Stratum 3: Low-income blocks (50 blocks)

**Sampling within Each Stratum:**

- A random sample of blocks is selected from each stratum. The number of blocks selected depends on the size of the stratum.

**Example of Selecting Blocks:**

- **From the urban PSU with 200 blocks:**

  - Stratum 1 (High-income): 20% of 50 blocks = **10 blocks selected**
  - Stratum 2 (Middle-income): 20% of 100 blocks = **20 blocks selected**
  - Stratum 3 (Low-income): 20% of 50 blocks = **10 blocks selected**
  
  - **Total blocks selected from this PSU:** ``10 + 20 + 10 = 40 blocks selected``

- **For all 754 PSUs:** 

  - Suppose each PSU selects an average of 10% of its blocks.
  - If each PSU has 100 blocks on average, **Total blocks selected:** ``754 PSUs * 10 blocks = 7,540 blocks``

Stage 3: Selection of Housing Units within Blocks
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**What are Clusters?**

Within each selected block, housing units are grouped into clusters of four nearby units. Each cluster is a small group of housing units that are geographically close, making it easier for interviewers to visit.

### Step 1: Sort Housing Units into Clusters

**Sorting Process:**

- **List and Sort:** All housing units within each selected block are listed and sorted based on proximity. This could mean sorting by address, physical location, or other geographic indicators.
  
  **Example:**

  - In a block with 100 housing units, the units are sorted and grouped into 25 clusters of 4 units each.

### Step 2: Sample Clusters within Blocks

**Sampling Process:**

- **Probability Sampling:** A random sample of clusters is selected from each block. The selection might be done using **Simple Random Sampling (SRS)** or **Probability Proportional to Size (PPS)**.
  
  **Example of Cluster Sampling:**

  - If 20% of clusters are selected from each block, and each block has 25 clusters:

    - **Clusters selected per block:** ``25 * 20% = 5 clusters selected``

- **For all 7,540 blocks:**

  - **Total clusters selected:** ``7,540 blocks * 5 clusters = 37,700 clusters``

### Step 3: Final Selection of Housing Units

- **Total Housing Units:** Each cluster contains 4 housing units.

  - **Total housing units selected:** ``37,700 clusters * 4 housing units per cluster = 150,800 housing units selected``

Summary of the CPS Sampling Process
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. **Stage 1: PSU Selection**
   - **754 PSUs** are selected from the total of 2007 PSUs.

2. **Stage 2: Block Selection**
   - From these 754 PSUs, **7,540 blocks** are selected.

3. **Stage 3: Cluster and Housing Unit Selection**
   - Within these blocks, **37,700 clusters** (each containing 4 housing units) are selected.
   - **Final Sample:** Approximately **150,800 households** are included in the CPS.


Lecture 03 Ch3 Producing Data 08/25-08/31/2024
==============================================

We're building our terminology vocabulary so we can explore more interesting topics later on. Some of the definitions and concepts are straightforward, but others might be a bit challenging if you're encountering them for the first time. I suggest reading the examples in the textbook (Yes! I finally got the textbook). Once you have the context, the concepts become easier to understand. In class, I'll focus on explaining the key parts of these definitions and concepts. Most importantly, I'll do my best to connect them, so you can grasp the overall logic and see the big picture. This will help you remember the concepts more easily and understand why they exist. I believe this approach is crucial to the learning process.

Summary of Ch3.1 Sources of Data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Confounding**, You will hear this often—it is probably one of the biggest challenges we face when trying to establish causality. For example, consider the smoking and lung cancer example, or the placebo effect in medical experiments. The reason we seek to establish causality is that we often want to understand the response of a variable **Y** when we apply a treatment or intervention to an explanatory variable **X**.

In observational studies, advanced statistical techniques are typically required to address confounding variables. In experimental studies, careful design can help reduce the impact of confounding. In this chapter, we will primarily focus on experimental studies.

.. admonition:: Remember!
  
   **Confounding** occurs when an explanatory variable is related to one or more other variables that have an influence on the response variable. When this happens, we sometimes attribute a relationship to an explanatory variable when the effect is fully or partly due to the confounding variables.

**Textbook justification for studying experiments**

An observational study, even one based on a carefully chosen sample, is a poor way to determine what will happen if we change something. The best way to see the effects of a change is to do an intervention—where we actually impose the change. When our goal is to understand cause and effect, experiments are the only source of fully convincing data.

.. admonition:: Remember!

   In an **observational study**, we observe individuals and measure variables of interest but do not attempt to influence the responses.

   In an **experiment**, we deliberately impose some condition on individuals, and we observe their responses. The condition imposed is called a treatment or an **intervention**.

**Section 3.1 SUMMARY**

- **Anecdotal data** come from stories or reports about cases that do not necessarily represent a larger group of cases.

- **Available data** are data that were produced for some other purpose but that may help answer a question of interest.

- A **sample survey** collects data from a **sample** of cases that represent some larger **population** of cases.

- A **census** collects data from all cases in the population of interest.

- In an **observational study**, we observe individuals but we do not attempt to influence their responses.

- In an **experiment**, a treatment or an intervention is imposed, and the responses are recorded.

Summary of Ch3.2 Design of Experiments
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

One of the challenges in dealing with confounding is that the confounding variable, or confounder, is often hidden or lurking. For example, in the 1950s, many studies attempted to establish a causal relationship between smoking and lung cancer—a conclusion that was obviously bad news for tobacco companies and the entire industry. The tobacco industry argued that a genetic factor might influence both smoking behavior and the development of lung cancer, and that this genetic factor—a hidden variable—could not be measured with the technology available in the 1950s.

The best way to avoid confounding is to do a **comparative experiment** according to the textbook.

In medical settings, it is standard practice to randomly assign patients either to one or more **treatment groups** or a **control group**. The effects of a treatment are evaluated by making a **comparison** with the control group. For a comparison to be valid, the conditions experienced by subjects in each **treatment group** and the control group should be identical except that the treatment groups receive the product or products that are being evaluated.

**Purpose of an experiment, explanatory and response variable:**

Because the purpose of an experiment is to reveal the response of one variable to changes in one or more other variables, the distinction between explanatory and response variables is important. The explanatory variables in an experiment are often called **factors**. Many experiments study the joint effects of several factors. In such an experiment, each **treatment** is formed by combining a specific value (often called a **level**) of each of the factors.

If groups assigned to treatments are quite different in a comparative experiment, we should be concerned that our experiment will be **bias**. That's why **Randomization** is essential to ensure that the groups are similar. **Matching** can be helpful, but often there are too many lurking varibles. Therefore, randomized comparative experiments are crucial. For more details, refer to Figure 3.3 and the smartphone example 3.18 in the textbook.

.. admonition:: Remember!

   When all experimental units are allocated at random among all treatments, as in Examples 3.20 (page 168) and 3.21, the experimental design is known as a **completely randomized design**. Completely randomized designs can compare any number of treatments. The treatments can be formed by levels of a single factor or by more than one factor.

.. admonition:: Principles of experimental design

   The basic principles of statistical design of experiments are

   1. **Compare** two or more treatments. This will control the effects of lurking variables on the response.

   2. **Randomize**: use chance to assign experimental units to treatments.

   3. **Repeat** each treatment on many units to reduce chance variation in the results.

**Other Experiment Designs:**

**Matched Pairs Designs**

Completely randomized designs are the simplest statistical designs for experiments. They illustrate clearly the principles of control, randomization, and **repetition**. However, completely randomized designs are often inferior to more elaborate statistical designs. In particular, matching the subjects in various ways can produce more precise results than simple randomization.

The simplest use of matching is a **matched pairs design**, which compares just two treatments. The subjects are matched in pairs. For example, an experiment to compare two advertisements for the same product might use pairs of subjects with the same age, sex, and income. The idea is that matched subjects are more similar than unmatched subjects so that comparing responses within a number of pairs is more efficient than comparing the responses of groups of randomly assigned subjects. Randomization remains important: which one of a matched pair sees the first ad is decided at random. One common variation of the matched pairs design imposes both treatments on the same subjects so that each subject serves as his or her own control.

**Block Designs**

Block designs extend the use of "similar subjects" from pairs to larger groups. See Figure 3.6 and the cancer example 3.26 in the textbook.

A **block** is a group of experimental units or subjects that are known before the experiment to be similar in some way that is expected to affect the response to the treatments. In a **block design**, the random assignment of units to treatments is carried out separately within each block.

**Section 3.2 SUMMARY**

- In an experiment, one or more **treatments** are imposed on the **experimental units** or **subjects**. Each treatment is a combination of **levels** of the explanatory variables, which we call **factors**. **Outcomes** are the measured variables that are used to compare the treatments.

- The **design** of an experiment refers to the choice of treatments and the manner in which the experimental units or subjects are assigned to the treatments.

- The basic principles of statistical design of experiments are **comparison**, **randomization**, and **repetition**.

- The simplest form of control is **comparison**. Experiments should compare two or more treatments in order to prevent **confounding** the effect of a treatment with other influences, such as lurking variables.

- **Randomization** uses chance (Table B at the back of the textbook or software) to assign subjects to the treatments. Randomization creates treatment groups that are similar (except for chance variation) before the treatments are applied. Randomization and comparison together prevent **bias**, or systematic favoritism, in experiments.

- You can carry out randomization by giving numerical labels to the experimental units and using software or a **table of random digits** to choose treatment groups.

- **Repetition** of the treatments on many units reduces the role of chance variation and makes the experiment more sensitive to differences among the treatments.

- Good experiments require attention to detail as well as good statistical design. Many behavioral and medical experiments are **double-blind**. Lack of realism in an experiment can prevent us from generalizing its results.

- **Matched pairs** are used to compare two treatments. In some matched pairs designs, each subject receives both treatments in a random order. This is called a **cross-over experiment**. In others, the subjects are matched in pairs as closely as possible, and one subject in each pair receives each treatment.

- In addition to comparison, a second form of control is to restrict randomization by forming **blocks** of experimental units that are similar in some way that is important to the response. Randomization is then carried out separately within each block.

Summary of Ch3.3 Sampling Design
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The sample design refers to the method used to choose the sample from the population. The entire group of individuals that we want information about is called the **population**. A **sample** is a part of the population that we actually examine in order to gather information. A **parameter** is a number that describes the population, the information we want to know. Because in practice, we do not know the parameter's value. A **statistic** is a number that describes a sample. The value of a statistic is known when we have taken a sample, but it can change from sample to sample. We use a statistic to estimate an unknown parameter. The purpose of sampling or experimentation is usually **statistical inference:** using sample statistics to make statements about unknown parameters.

**Voluntary response sample**

A **voluntary response sample** consists of people who choose themselves by responding to a general appeal. Voluntary response samples are frequently biased because people with strong opinions, especially negative opinions, are most likely to respond.

**Simple random sample**

A **simple random sample (SRS)** of size n consists of n individuals from the population chosen in such a way that every set of n individuals has an equal chance to be the sample actually selected.

Each treatment group in a **completely randomized experimental design** (When all experimental units are allocated at random among all treatments.) is an SRS drawn from the available experimental units. We select an SRS by labeling all the individuals in the population and using software or a table of random digits to select a sample of the desired size, just as in experimental randomization. **Notice that an SRS not only gives every possible sample an equal chance to be chosen but also gives each individual an equal chance to be chosen.** There are other random sampling designs that give each individual, but not each sample, an equal chance. One such design, systematic random sampling, is described in Exercise 3.40 (page 191).

Please refer to the textbook for guidance on how to perform a Simple Random Sample (SRS) using software or random digits.

Often, the problems we are studying require more complex sampling designs.

**More complex sampling designs**

A **probability sample** is a sample chosen by chance. We must know what samples are possible and what chance, or probability, each possible sample has.

Some probability sampling designs (such as an SRS) give each member of the population an equal chance to be selected. This may not be true in more elaborate sampling designs. In every case, however, the use of chance to select the sample is the essential principle of statistical sampling.

Designs for sampling from large populations spread out over a wide area are usually more complex than an SRS. For example, it is common to sample important groups within the population separately and then combine these samples. This is the idea of a **stratified sample**.

**Stratified random sample**

To select a **stratified random sample**, first divide the population into groups of similar individuals, called **strata**. Then choose a separate SRS in each stratum and combine these SRSs to form the full sample.

Choose the strata based on facts known before the sample is taken. For example, a population of election districts might be divided into urban, suburban, and rural strata.

**Multistage random samples**

Another common means of restricting random selection is to choose the sample in stages. This type of design is called a **multistage design**. This type of design is widely used in national samples of households or people. For example, data on employment and unemployment are gathered by the government’s Current Population Survey, which conducts interviews in about 60,000 households each month. The cost of sending interviewers to the widely scattered households in an SRS would be too high. Moreover, the government wants data broken down by states and large cities.

**EXAMPLE 3.38 The Current Population Survey.**

The Current Population Survey uses a multistage design. The final sample consists of groups of nearby households, called **clusters**, that an interviewer can easily visit. Most opinion polls and other national samples are also multistage, though interviewing in most national samples today is done by telephone rather than in person, eliminating the economic need for clustering. The Current Population Survey sampling design is roughly as follows:

**Stage 1.** Divide the United States into 2007 geographical areas called primary sampling units, or PSUs. PSUs do not cross state lines. Select a sample of 754 PSUs. This sample includes the 428 PSUs with the largest population and a stratified sample of 326 of the others.

**Stage 2.** Divide each PSU selected into smaller areas called blocks. Stratify the blocks using ethnic and other information and take a stratified sample of the blocks in each PSU.

**Stage 3.** Sort the housing units in each block into clusters of four nearby units. Interview the households in a probability sample of these clusters.

Analysis of data from sampling designs more complex than an SRS takes us beyond basic statistics. But the SRS is the building block of more elaborate designs, and analysis of other designs differs more in complexity of detail than in fundamental concepts.

**Cautions about sample surveys**

.. admonition:: Remember!

   **Undercoverage** occurs when some groups in the population are left out of the process of choosing the sample.

   **Nonresponse** occurs when an individual chosen for a sample can't be contacted or does not cooperate.

**Section 3.3 SUMMARY**

- A sample survey selects a **sample** from the **population** of all individuals about which we desire information. We base conclusions about the population on data about the sample.

- The **sample design** refers to the method used to select the sample from the population. **Probability sample designs** use impersonal chance to select a sample.

- The basic probability sample is a **simple random sample (SRS)**. An SRS gives every possible sample of a given size the same chance to be chosen.

- Choose an SRS using software. This can also be done using a **table of random digits** to select the sample.

- To choose a **stratified random sample**, divide the population into **strata**, groups of individuals that are similar in some way that is important to the response. Then choose a separate SRS from each stratum and combine them to form the full sample.

- **Multistage samples** select successively smaller groups within the population in stages, resulting in a sample consisting of clusters of individuals. Each stage may employ an SRS, a stratified sample, or another type of sample.

- Failure to use probability sampling often results in **bias**, or systematic errors in the way the sample represents the population.

- **Voluntary response samples**, in which the respondents choose themselves, are particularly prone to large bias.

- In human populations, even probability samples can suffer from bias due to **undercoverage** or **nonresponse**, from **response bias** due to the behavior of the interviewer or the respondent, or from misleading results due to **poorly worded questions**.

Summary of Ch3.4 Ethics
^^^^^^^^^^^^^^^^^^^^^^^

The production and use of data, like all other human endeavors, raise ethical quesitons. The most complex issues of data ethics arise when we collect data from people. For example, there are many articles that discuss the complex issues raised by twin studies.

The ethical difficulties are more severe for experiments that impose some treatment on people than for sample surveys that simply gather information. Trials of new medical treatments, for example, can do harm as well as good to their subjects.


**Basic data ethics**

The organization that carries out a study must have an **institutional review board** that reviews all planned studies in advance in order to protect the subjects from possible harm.

All individuals who are subjects in a study must give their **informed consent** before data are collected.

All individual data must be kept confidential. Only statistical summaries for groups of subjects may be made public.

**Section 3.4 SUMMARY**

- Approval of an **institutional review board** is required for studies that involve humans or animals as subjects.

- Human subjects must give **informed consent** if they are to participate in experiments.

- Data on human subjects must be kept **confidential**.

- Clinical trials should be evaluated from an ethics standpoint.

Ch2.7 The Question of Causation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. image:: /images/0301.png

**common response:** the chocolate consumption and Nobel Prize example.
**confounding:** the smoking and lung caner example. 

**Explaining Association**

Many observed associations are at least partly explained by **lurking variables**. Both **common response** and **confounding** involve the influence of a lurking variable (or variables) z on the response variable y. The distinction between these two types of relationships is less important than the common element: the influence of lurking variables. The most important lesson of these examples is one we have already emphasized: **even a very strong association between two variables is not by itself good evidence that there is a cause-and-effect link between the variables.**

Figure 2.34(c) illustrates **confounding**. Both the explanatory variable x and the lurking variable z may influence the response variable y. Because x is confounded with z, we cannot distinguish the influence of x from the influence of z. We cannot say how strong the direct effect of x on y is. In fact, it can be hard to say if x influences y at all. **When many uncontrolled variables are related to a response variable, you should always ask whether or not confounding of several variables prevents you from drawing conclusions about causation.**

**Establishing Causation**

How can a direct causal link between x and y be established? The best method—indeed, the only fully compelling method—of establishing causation is to conduct a carefully designed **experiment** in which the effects of possible lurking variables are controlled. "Chapter 3" explains how to design convincing experiments.

**Section 2.7 Summary**

- Some observed associations between two variables are due to a **cause-and-effect** relationship between these variables, but others are explained by **lurking variables**.

- The effect of lurking variables can operate through **common response** if changes in both the explanatory and the response variables are caused by changes in lurking variables. **Confounding** of two variables (either explanatory or lurking variables or both) means that we cannot distinguish their effects on the response variable.

- Establishing that an association is due to causation is best accomplished by conducting an **experiment** that changes the explanatory variable while controlling other influences on the response.

- In the absence of experimental evidence, be cautious in accepting claims of causation. Good evidence of causation (1) requires a strong association, (2) appears consistently in many studies, (3) has higher levels of the explanatory variable associated with stronger responses, (4) requires that alleged cause precede the effect in time, and (5) must be plausible.

Ch5.1 Toward Statistical Inference
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Key Terms Related to Sampling Distribution**

1. **Population:** The entire set of individuals or elements that we are interested in studying. A population has parameters like the true mean (:math:`\mu`) and standard deviation (:math:`\sigma`). 

   *Example*: The average height of all Purdue students.

2. **Sample:** A subset of the population selected for measurement. The sample is used to make inferences about the population. 

   *Example*: We select 100 students to form a sample.

3. **Statistic:** A numerical value calculated from a sample. It is used to estimate a population parameter. 
   
   *Example*: The sample mean calculated for each sample is a statistic.

4. **Estimator:** A rule or formula used to calculate a statistic that estimates a population parameter. 

   *Formula*: For the sample mean, the estimator is:

      :math:`\hat{\mu} = \frac{1}{n} \sum_{i=1}^{n} X_i`

         where (:math:`X_i`) are the sample values and (:math:`n`) is the sample size.

5. **Estimate:** The specific value obtained by applying the estimator to a particular sample. It is a realization of the estimator.

6. **Sampling Distribution:** The probability distribution of a statistic obtained from a large number of samples drawn from a specific population. It shows how the statistic varies from sample to sample. 

   *Example*: The distribution of the `sample_means` represents the sampling distribution of the sample mean.

7. **Unbiased Estimator:** An estimator whose expected value (mean of its sampling distribution) is equal to the true value of the population parameter it estimates. 

   *Example*: The sample mean is an unbiased estimator of the population mean.

8. **Biased Estimator:** An estimator whose expected value is not equal to the true value of the population parameter it estimates. This introduces a systematic error (bias) in the estimates.

9. **Bias:** The difference between the expected value of an estimator and the true value of the population parameter. Bias measures the accuracy of an estimator. 

   *Formula*: Bias of an estimator (:math:`\hat{\theta}`) for a parameter (:math:`\theta`) is given by:

      :math:`\text{Bias}(\hat{\theta}) = E(\hat{\theta}) - \theta`
     
10. **Variance of the Sampling Distribution:** The spread of the sampling distribution, indicating how much the statistic varies from one sample to another. Lower variance means more precise estimates. 

   *Formula*: The variance of the sampling distribution of the sample mean (standard error squared) is given by:

      :math:`\text{Var}(\hat{\mu}) = \frac{\sigma^2}{n}`

         where (:math:`\sigma^2`) is the population variance and (:math:`n`) is the sample size.

11. **Standard Error:** The standard deviation of the sampling distribution. It measures the precision of the estimator and how much the sample mean is expected to vary from sample to sample. 

   *Formula*: The standard error of the sample mean is:

      :math:`\text{SE}(\hat{\mu}) = \frac{\sigma}{\sqrt{n}}`

         *Note*: The standard error decreases as the sample size increases.

**What is a Sampling Distribution?**

A sampling distribution is the probability distribution of a given statistic based on a large number of samples drawn from a specific population. In simpler terms, if you were to repeatedly take random samples from a population and calculate a statistic (like the mean, median, or variance) for each sample, the distribution of those calculated statistics would form the sampling distribution.

For example, if you repeatedly take random samples of 30 individuals from a population and calculate the sample mean for each sample, the distribution of those sample means is the sampling distribution of the mean.

**Why Do We Care About Its Mean and Variance?**

*Mean of the Sampling Distribution:*
The mean of the sampling distribution (often called the expected value) is important because it tells us about the accuracy of our estimator. If the mean of the sampling distribution is equal to the true population parameter, then the estimator is said to be unbiased. This means, on average, the estimator provides the correct value, making it a reliable tool for making inferences about the population.

For example, if the mean of the sampling distribution of the sample mean is equal to the population mean, then the sample mean is an unbiased estimator of the population mean.

*Variance of the Sampling Distribution:*
The variance (or spread) of the sampling distribution indicates the variability of the estimator. It tells us how much the statistic (e.g., sample mean) will fluctuate from one sample to another. A lower variance means that the estimator is more consistent and reliable because the estimates are closely clustered around the mean of the sampling distribution.

Variance is crucial because it directly affects the standard error, which measures the precision of the estimator. A smaller standard error indicates that our sample statistic is likely to be close to the true population parameter, which is desirable in statistical inference.

The variance also helps us understand the trade-off between accuracy and precision. While the mean of the sampling distribution indicates accuracy (bias), the variance indicates precision (how much the estimates vary).

.. image:: /images/0302.png

**Example Two: Normal Distribution with mean = 50, standard deviation = 10**

The true population consists of 10,000 units. For the large sample experiment, we draw 100 units at a time to form each sample. For the small sample experiment, we draw 10 units per sample. We repeat this process 100 times, resulting in 100 large samples and 100 small samples. We then calculate the sample means for each sample to create sampling distributions for both experiments. As shown in the graph, the sampling distribution for the small sample is much more dispersed than that of the large sample, indicating greater variability.

.. image:: /images/0303.png












Lecture 02  Producing Data 08/18-08/24/2024
===========================================

Sources of Data
^^^^^^^^^^^^^^^

If we aim to study something, our objective is often to draw conclusions or uncover **causal relationships**. However, it's important to be cautious about relying solely on personal experience or hearsay when forming these conclusions.

**Anecdotal data** represent individual cases that often come to our attention because they are striking in some way. We tend to remember these cases because they are unusual. **The fact that they are unusual means that they may not be representative of any larger group of cases.**

We can use **available data**, data that were produced in the past for some other purpose but that may help answer a present question inexpensively. Alternatively, we can intentionally generate new data specifically to answer a particular question. The first approach typically results in observational studies, while the second leads to experimental studies.

Both approches have their own challenges.

**Sample Surveys**, researchers typically collect data without influencing the outcomes, making their work a form of observational study.. In a sample survey, a **sample** of individuals is selected from a larger **population** of individuals. One can study a small part of the population in order to gain information about the population as a whole. Conclusions drawn from a sample are valid only when the sample is drawn in a **well-defined way**.

When our goal is to understand cause and effect (causality), experiments are the only source of fully convincing data. The invention of randomized experiments is a stroke of genius; even today, they remain the gold standard for large pharmaceutical companies to test the effectiveness of their new drugs. The distinction between an observational study and an experiment is one of the most important in statistics.

.. admonition:: Remember!

   An observational study observes individuals and measures variables of interest but does not attempt to influence the responses. The purpose is to describe some group or situation.

   An experiment deliberately imposes some treatment on individuals to measure their responses. The purpose is to study whether the treatment causes a change in the response.

**Confounding:** Observational studies of the effect of one variable on another often fail to establish causality because of confounding between the explanatory variable and one or more lurking/hidden variables. Finding the confounder is a million dollar question. Sometimes, people really do want to hide this hidden variable. The widely recognized phrase "Correlation is not causation."

.. image:: /images/0201.png

There's an odd connection between eating more chocolate and winning the Nobel Prize.

.. image:: /images/0202.png

Well-designed experiments take steps to avoid confounding. The key is randomize.

Design of Experiments
^^^^^^^^^^^^^^^^^^^^^

An experiment is a study in which we actually do something (a treatment) to people, animals, or objects (the experimental units) to observe the response. 

* An **experimental unit** is the smallest entity to which a treatment is applied. When the units are human beings, they are often called **subjects**.

* The explanatory variables in an experiment are often called **factors**.

* A specific condition applied to the individuals in an experiment is called a **treatment**. If an experiment has several explanatory variables, a treatment is a combination of specific values of these variables. 

* **Outcomes** are the measured variables that are used to compare the treatments.

To clearly observe and measure effects, we need well-designed comparative experiments. Effective design is as crucial in experiments as it is in sampling, which often involves assigning subjects to two or more groups. Typically, these include a **control group** and a **treatment group**. The treatment group receives the treatment/intervention being studied, while the control group receives a placebo. The **placebo effect** occurs when people respond favorably to personal attention or to any treatment that they hope will help them. A study is **biased** if it systematically favors certain outcomes over others. 

**Bias** in sampling is the tendency for samples to differ from the corresponding population in some systematic way. Bias can result from the way in which the sample is selected or from the way in which information is obtained once the sample has been chosen. The most common types of bias encountered in sampling situations are **selection bias, measurement or response bias, and nonresponse bias**.

The Need for Randomization: Comparison alone is not enough. If the treatments are given to groups that differ greatly, bias will result. The solution to the problem of bias is random assignment. Just like sampling surveys, we need to choose our survey participants randomly. 

.. admonition:: Remember!
   
   In an experiment, **random assignment** means that experimental units are assigned to treatments at random—that is, using some sort of chance process. 

.. image:: /images/0203.png

How to Randomize: One way to randomize an experiment is to rely on random digits to make choices in a neutral way. We can use a table of random digits or the random sampling function provided by most statistical software. Roll a dice?

**Principles of Experimental Design:**

* **Control** for lurking variables that might affect the response, most simply by comparing two or more treatments. 

* **Randomize:** Use chance to assign experimental units to treatments.

* **Replication:** Use enough experimental units in each group to reduce chance variation in the results.

In a **double-blind experiment**, neither the subjects nor those with whom they interact know which treatment a subject received.

The most serious **potential weakness** of experiments is **lack of realism**. That is, the subjects or treatments or setting of an experiment might not realistically duplicate the conditions we really want to study.

The experimental conditions often do not accurately reflect real-world situations. Simulation, we know it's just a simulation. 

Nonetheless, the random comparative experiment, because of its ability to give convincing evidence for causation, is one of the most important ideas in statistics.

**Blocked Designs**: Completely randomized designs are the simplest statistical designs for experiments. But, as with sampling, there are times when the simplest method does not yield the most precise results.

* A **block** is a group of experimental units that are known, before the experiment, to be similar in some way that is expected to affect the response to the treatments. Blocking by certain variables, such as age, sex.

* In a **block design**, the random assignment of experimental units to treatments is carried out separately within each block. 

Form blocks based on the most important unavoidable sources of variability (lurking variables) among the experimental units. Randomization will average out the effects of the remaining lurking variables and allow an unbiased comparison of the treatments. What we lose here?

**Control what you can, block what you cannot control (that is, form blocks), and randomize to create comparable groups.** 

Population and Sample
^^^^^^^^^^^^^^^^^^^^^

The distinction between population and sample is basic to statistics. To make sense of any sample result, you must know what population the sample represents.  In a statistical study, the **population** is the entire group of individuals about which we want information. A **sample** is the part of the population from which we actually collect information. We use information from a sample to draw conclusions about the entire population.

.. image:: /images/0204.png



Lecture 01 08/18-08/24/2024
---------------------------
Things always tend to get a bit chaotic at the beginning. Just this Monday, I was assigned a new office, and after a deep cleaning and I was ready to set up the monitor, I was informed that I had been assigned to the wrong office and needed to move again. Life has a way of throwing us curveballs, but that unpredictability is also what makes it interesting—it's full of uncertainties and randomness.

As we embark on this introductory statistics course, STAT 301: Elementary Statistical Methods, you may feel overwhelmed by the volume of material. With such a large class and the introductory nature of the course, it's understandable. You might find yourself navigating different tools and technologies—learning SPSS, while tackling MATLAB, or diving into Python in other classes. It can feel like there isn’t enough time to keep up.

But instead of getting discouraged, embrace the challenge. Often, feeling overwhelmed is a sign that you’re pushing your boundaries and growing. Life is full of challenges, and when you look back, you'll be amazed at how much you've overcome and how much stronger you've become. Remember, your instructors and TAs are here to support you every step of the way.

Instructor and TAs
^^^^^^^^^^^^^^^^^^
Your instructor and TAs are here to support you throughout the entire semester. You'll meet your instructor during lectures and your TAs during lab sessions, typically held on Fridays. They are your first points of contact if you have any questions about course materials. Remember, no question is a stupid question, and we understand that students come from diverse backgrounds. So, don't hesitate to reach out to us in person or via email. As for me, you can email me anytime. However, here are some tips when contacting us for help:

* Before reaching out, spend some time formulating your issue. Clearly show us where you're encountering problems and what specifically you're struggling with.
* We cannot do the work for you; it’s essential that you put in the effort first. Don’t bring a question without having spent time pondering it or studying the relevant materials. This approach is more effective.
* The help room and office hours are held at MATH 206/211. From my understanding, there will be someone available for this course every weekday. The great thing is, you can ask anyone there for assistance. Just drop by the office hours or meet us online using WebEx, Zoom, or Teams!
* Email is best suited for answering short questions. If your question is more complex, especially if it involves using a program or your laptop, please visit the help room or schedule an in-person meeting.
* In the syllabus, you will find contact information for all the instructors and TAs. Be sure to note down the contact details for the instructor and TA assigned to your section.
* Note: A Cengage (WebAssign) representative will be available in person for assistance in MATH 431 every Monday and Tuesday from 10 AM to 3:30 PM.


Some Important Notes
^^^^^^^^^^^^^^^^^^^^
* There are several types of assignments in this course: Homework, Attendance (or Quizzes if you are in an online section), Labs, Peer Review Written Assignment (PRWA), Data Science Project, and Two Midterm Exams. With so many due dates, it's crucial to check them regularly. Each week, be aware of what assignments need to be completed. It is solely your responsibility to submit your work on time. The instructor and TAs cannot make exceptions for late submissions. This is a large class with over a thousand students, and we must be fair to everyone.
* Every point counts, and the **Number #1 Reason students fail this course: Not completing assignments or submitting them late**. Start your assignments early—don’t wait until the last minute.
* You are responsible for verifying each submission. If there is an error, we CANNOT award points. **Please make sure you have uploaded the correct document**.
* Review each type of assignment in the syllabus and ensure you understand your responsibilities for each. For group assignments, your attendance and participation matter. These assignments typically have multiple checkpoints and several deadlines. Mark them on your calendar.
* Don’t wait until the last minute to familiarize yourself with the technologies needed to complete your assignments. Many assignments will be conducted online. For example, the two exams will be proctored using Respondus LockDown Browser. Make sure you are comfortable using the browser before the exam date, especially if you plan to use your own laptop. Purdue usually provides dedicated webpages with instructions for using such software. For example, information on the LockDown Browser can be accessed at `link01`_. Simply search Google for "Purdue" plus the software name, or look for tutorials on YouTube before you need to use them.
* **Your grade will be calculated strictly from your official scores on BrightSpace**. There may be opportunities for extra credit in the homework, but do not ask for additional extra credit at the end of the semester to reach a grade cutoff. With over :math:`1,000` students enrolled in this course each semester, everyone has unique circumstances. Therefore, grade cutoffs are strictly enforced to ensure fairness for all students. Track your progress diligently!
* Install SPSS on your computer as soon as possible via the Purdue Community Hub, and try to familiarize yourself with it. Lab activities and some homework assignments will require SPSS. If you have trouble with SPSS, visit the help room to get the assistance you need.


.. _link01: https://www.purdue.edu/innovativelearning/tools-resources/instructional-technology/respondus-browser/

Assignments
^^^^^^^^^^^

Late assignments will be subject to penalties unless accompanied by valid documentation (physical letter or email) from an authorized source (e.g., doctors, university officials).

I’d like to emphasize two points regarding this. First, many students mistakenly believe that instructors have the authority to change grades at their discretion. The reality is that we are primarily rule enforcers, and grading is likely the area where we have the least flexibility. Moreover, even small mistakes can quickly accumulate, leading to severe consequences in the real world. Consider watching documentaries or movies like those on Enron or "The Big Short" about the financial crisis. This is why the University and society expect us to strictly enforce these rules. Second, you will find later in life that the cost of making mistakes, like submitting an assignment late, is much lower in school than in the real world, where the stakes are much higher. As your instructor, I hope you learn this important lesson and understand the value of accountability.

* **Attendance:** Your TA will check your attendance during the Friday lab sessions. This accounts for 5% of your total final grade.
* **Homework:** There are 23 homework assignments, with the lowest 2 scores dropped. Homework is completed on WebAssign, so please ensure you register for it. Multiple assignments may be due in a single week—check the due dates regularly. For details on penalties and extra credit, please refer to the syllabus. Homework counts for 15% of your total grade.
* **Labs:** There are 7 lab assignments, with the lowest 1 score dropped. Labs are conducted on BrightSpace or WebAssign. Please refer to the syllabus for penalty details. Labs constitute 20% of your total grade.
* **Peer Reviewed Written Assignment (PRWA):** The PRWA will be completed online using a software package (Circuit) within BrightSpace. This involves two parts of written assignments, so please check the corresponding open and due dates, and ensure you submit the required assignments. PRWA counts for 10% of your total grade.
* **Midterm Exams:** There are 2 midterm exams, each lasting 45 minutes. The exams will take place on Fridays during the designated lab time. If you are using a personal computer, please ensure the necessary software is installed in advance. Midterms account for 30% of your total grade.
* **Data Project:** This project includes multiple checkpoints—please refer to the schedule for the corresponding due dates. Your attendance and participation are crucial. The Data Project makes up 20% of your total grade.


How to Get SPSS from Purdue Community Hub
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Below are the steps to download and install SPSS from the Purdue Community Hub on your personal computer. I’m using a Mac for this demonstration, but the process should be similar if you're using a Windows PC, with the main difference being the installation process, where you'll need to follow the Windows installation wizard. If you're not particularly tech-savvy, I recommend simply following the wizard and choosing the default folders and settings. If you encounter any issues, don't hesitate to seek help from your TAs or instructor. Additionally, you can find helpful videos on YouTube that explain how to install and activate SPSS.

**Step 1:** Visit the Purdue Community Hub website and click the "Login" button located on the right side of the page.

.. image:: /images/spss01.png

**Step 2:** Log in using your Purdue Career Account credentials.

.. image:: /images/spss02.png

**Step 3:** Once you’ve successfully logged in, you’ll be directed to the store homepage. Scroll down and locate the "Statistical Software" tile.

.. image:: /images/spss03.png

**Step 4:** Click on "Statistical Software" tile.

.. image:: /images/spss04.png

**Step 5:** You will see available softwares. Scroll down to find 'SPSS Standard for Personally Owned Computers,' then click on it.

.. image:: /images/spss05.png

**Step 6:** Select the appropriate version based on your computer, then click 'Add to Cart.' It’s free!

.. image:: /images/spss06.png

**Step 7:** Click 'Check Out' to proceed.

.. image:: /images/spss07.png

**Step 8:** Check 'I Accept,' and then click 'Next.' After all, it's free—what else can you do?

.. image:: /images/spss08.png

**Step 9:** Click 'Next.' We're almost done!

.. image:: /images/spss09.png

**Step 10:** Click 'Place Order' to complete the process.

.. image:: /images/spss10.png

**Step 11:** **COPY the serial number somewhere safe**, before clicking the download button. You'll need it to activate the software when prompted.

.. admonition:: Remember!

   Copy the serial number to a safe place so you can easily retrieve it later when you activate SPSS.


.. image:: /images/spss11.png

**Step 12:** A new page will pop up, and you can wait for the download to finish. Since it’s a large file, please be patient, especially if your internet connection is slow.

.. image:: /images/spss12.png





.. Seite's place, at least in a working enrionment in the future, you need to talk to someone who using statitcs in a compnay enrivorment, it's better for you to understand theri langeage. 



.. toctree::
   :maxdepth: 2
   :caption: Contents:

