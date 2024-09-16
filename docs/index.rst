.. STAT 301 documentation master file, created by
   sphinx-quickstart on Sat Aug 17 02:06:35 2024.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

STAT 301 @Purdue
======================
Welcome to the STAT 301 resource site, designed to provide supplementary materials for Purdue University students. As I am new to teaching this course, I will be adding more materials as the semester progresses. Please note that the content here may contain errors or mistakes; if you spot any, I encourage you to contact me.

The views expressed in this document are my own and do not necessarily reflect those of other instructors for this class. STAT 301 is a university-wide undergraduate course that serves a large and diverse student body. If you have any concerns about the materials presented here, please don't hesitate to reach out.

My primary goal with this resource is to support your learning in STAT 301, and to inspire you to explore statistics further. I hope that what you learn in this class will be valuable to you in the future, and that five or ten years from now, you'll still remember something useful from this experience.


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

