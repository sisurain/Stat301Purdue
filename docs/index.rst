.. STAT 301 documentation master file, created by
   sphinx-quickstart on Sat Aug 17 02:06:35 2024.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

STAT 301 @Purdue
======================
Welcome to the STAT 301 resource site, designed to provide supplementary materials for Purdue University students. As I am new to teaching this course, I will be adding more materials as the semester progresses. Please note that the content here may contain errors or mistakes; if you spot any, I encourage you to contact me.

The views expressed in this document are my own and do not necessarily reflect those of other instructors for this class. STAT 301 is a university-wide undergraduate course that serves a large and diverse student body. If you have any concerns about the materials presented here, please don't hesitate to reach out.

My primary goal with this resource is to support your learning in STAT 301, and to inspire you to explore statistics further. I hope that what you learn in this class will be valuable to you in the future, and that five or ten years from now, you'll still remember something useful from this experience.

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

.. image:: /images/0201.png

Well-designed experiments take steps to avoid confounding. The key is randomize.

Design of Experiments
^^^^^^^^^^^^^^^^^^^^^

An experiment is a study in which we actually do something (a treatment) to people, animals, or objects (the experimental units) to observe the response. 

* An **experimental unit** is the smallest entity to which a treatment is applied. When the units are human beings, they are often called **subjects**.

* The explanatory variables in an experiment are often called **factors**.

* A specific condition applied to the individuals in an experiment is called a **treatment**. If an experiment has several explanatory variables, a treatment is a combination of specific values of these variables. 

* **Outcomes** are the measured variables that are used to compare the treatments.

To clearly observe and measure effects, we need well-designed comparative experiments. Effective design is as crucial in experiments as it is in sampling, which often involves assigning subjects to two or more groups. Typically, these include a **control group** and a **treatment group**. The treatment group receives the treatment/intervention being studied, while the control group receives a placebo. The **placebo effect** occurs when people respond favorably to personal attention or to any treatment that they hope will help them. A study is **biased** if it systematically favors certain outcomes over others. 

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

* A *block* is a group of experimental units that are known, before the experiment, to be similar in some way that is expected to affect the response to the treatments. Blocking by certain variables, such as age, sex.

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

