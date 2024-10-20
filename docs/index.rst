.. STAT 301 documentation master file, created by
   sphinx-quickstart on Sat Aug 17 02:06:35 2024.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

STAT 301 @Purdue
======================
Welcome to the STAT 301 resource site, designed to provide supplementary materials for Purdue University students. As I am new to teaching this course, I will be adding more materials as the semester progresses. Please note that the content here may contain errors or mistakes; if you spot any, I encourage you to contact me.

The views expressed in this document are my own and do not necessarily reflect those of other instructors for this class. STAT 301 is a university-wide undergraduate course that serves a large and diverse student body. If you have any concerns about the materials presented here, please don't hesitate to reach out.

My primary goal with this resource is to support your learning in STAT 301, and to inspire you to explore statistics further. I hope that what you learn in this class will be valuable to you in the future, and that five or ten years from now, you'll still remember something useful from this experience.

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

In a linear regression model with two predictors (without interaction), the relationship between the predictors and the response \(Y\) is:

.. math::  
   Y = \beta_0 + \beta_1 \cdot X_1 + \beta_2 \cdot X_2 + \epsilon

- \( \beta_1 \): Measures the effect of \( X_1 \) on \( Y \) when \( X_2 \) is held constant.  
- \( \beta_2 \): Measures the effect of \( X_2 \) on \( Y \) when \( X_1 \) is held constant.

This model assumes that the effect of \( X_1 \) on \( Y \) is the same no matter the value of \( X_2 \), and vice versa. However, if the impact of \( X_1 \) on \( Y \) changes depending on the value of \( X_2 \), there is an **interaction effect**.

To capture this dependency, we introduce a product term \( X_1 \times X_2 \). The full model with interaction becomes:

.. math::  
   Y = \beta_0 + \beta_1 \cdot X_1 + \beta_2 \cdot X_2 + \beta_3 \cdot (X_1 \times X_2) + \epsilon

- **Without interaction** (\( \beta_3 = 0 \)):  
  - The effect of \( X_1 \) on \( Y \) is fixed at \( \beta_1 \), regardless of the value of \( X_2 \).  
  - Similarly, the effect of \( X_2 \) on \( Y \) is \( \beta_2 \), no matter the value of \( X_1 \).

- **With interaction** (\( \beta_3 \neq 0 \)):  
  - The effect of \( X_1 \) on \( Y \) changes depending on the value of \( X_2 \).  
  - Similarly, the effect of \( X_2 \) on \( Y \) depends on the value of \( X_1 \).

The interaction term \( X_1 \times X_2 \) allows us to model this dependency between the two predictors.

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

1. **\(\bar{x}_{ij}\)** – Mean for the group at **level \(i\) of Factor A** and **level \(j\) of Factor B**.  
   - Represents the **observed group mean** for the specific combination of two factor levels.

2. **\(\bar{x}_{i\cdot}\)** – Marginal mean for **level \(i\) of Factor A**, averaged across all levels of Factor B.  
   - Represents the **main effect of Factor A**, assuming no interaction with Factor B.

3. **\(\bar{x}_{\cdot j}\)** – Marginal mean for **level \(j\) of Factor B**, averaged across all levels of Factor A.  
   - Represents the **main effect of Factor B**, assuming no interaction with Factor A.

4. **\(\bar{x}_{..}\)** – Grand mean of all observations in the dataset.  
   - Used to adjust for the subtraction of marginal means.

### How the Formula Captures Interaction Effect  

The expression inside the parentheses:

.. math::

   \left( \bar{x}_{ij} - \bar{x}_{i\cdot} - \bar{x}_{\cdot j} + \bar{x}_{..} \right)

captures the **additional variability** that cannot be explained by the main effects of Factor A and Factor B alone.

1. **Subtract \(\bar{x}_{i\cdot}\)**:  
   - Removes the portion of the group mean \(\bar{x}_{ij}\) explained by Factor A.

2. **Subtract \(\bar{x}_{\cdot j}\)**:  
   - Removes the portion of the group mean \(\bar{x}_{ij}\) explained by Factor B.

3. **Add \(\bar{x}_{..}\)**:  
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

The pooled sample variance \(s_p^2\) is given by:

.. math::

   s_p^2 = \frac{\sum (n_{ij} - 1) s_{ij}^2}{\sum (n_{ij} - 1)}

We will show that this formula is equivalent to:

.. math::

   s_p^2 = \frac{SSE}{DFE}

where **SSE** is the Sum of Squares for Residuals, and **DFE** is the Degrees of Freedom for Error.

### Step 1: Define the Terms  

1. **Sample Variance for Group \( (i, j) \)**:

   .. math::

      s_{ij}^2 = \frac{1}{n_{ij} - 1} \sum_{k=1}^{n_{ij}} \left( x_{ijk} - \bar{x}_{ij} \right)^2

   where:

   - \(x_{ijk}\) is the \(k\)-th observation in the group \( (i, j) \).  
   - \( \bar{x}_{ij} \) is the mean of the group \( (i, j) \).  
   - \(n_{ij}\) is the number of observations in group \( (i, j) \).

2. **Sum of Squares for Group \( (i, j) \)**:

   .. math::

      SS_{ij} = \sum_{k=1}^{n_{ij}} \left( x_{ijk} - \bar{x}_{ij} \right)^2

3. **Degrees of Freedom for Group \( (i, j) \)**:

   .. math::

      DF_{ij} = n_{ij} - 1

### Step 2: Rewrite the Pooled Variance Formula  

Substitute the formula for \( s_{ij}^2 \) into the pooled variance equation:

.. math::

   s_p^2 = \frac{\sum (n_{ij} - 1) \cdot \frac{1}{n_{ij} - 1} \sum_{k=1}^{n_{ij}} \left( x_{ijk} - \bar{x}_{ij} \right)^2}{\sum (n_{ij} - 1)}

The \( (n_{ij} - 1) \) terms cancel out:

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

This completes the proof. The pooled variance \( s_p^2 \) is simply the **mean squared error (MSE)**, which is the residual sum of squares (SSE) divided by the degrees of freedom for error (DFE).

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
----------------------------

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
---------------------------

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
----------------------------------------------------------------

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
---------------------------------------------------------

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
------------------------------------------------------

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
----------------------------------------------------

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

9. **Variance (s^2)**:
   
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
   - \( P \) is the desired percentile (e.g., 25th percentile for Q1, 50th percentile for the median), \
   - \( n \) is the number of data points in the dataset.

2. **Whole Number Position**: 
   - If the position is a whole number, use the corresponding data point at that position directly.

3. **Fractional Position**: 
   - If the position is a fraction (i.e., not a whole number), find the two adjacent data points in the dataset. \
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
--------------------------------------------------------------------------

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
---------------------------------------------------------------

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
----------------------------------------------

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
-------------------------------------------

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

