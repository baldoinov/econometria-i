# Statistics - A Full University Course on Data Science Basics

I've used [this](https://www.youtube.com/watch?v=xxpc-HPKN28&ab_channel=freeCodeCamp.org) video as reference. 


1. [Statistics - A Full University Course on Data Science Basics](#statistics-a-full-university-course-on-data-science-basics)
    1. [What is Statistics](#what-is-statistics)
    2. [Sampling](#sampling)
    3. [Experimental Design](#experimental-design)
    4. [Randomization](#randomization)
    5. [Frequency histogram, distribution and graphs](#frequency-histogram-distribution-and-graphs)
    6. [Measures of Central Tendency](#measures-of-central-tendency)
    7. [Measures of Variation](#measures-of-variation)


## What is Statistics

- Lecture Goals:
  - One example of a population parameter, and one example of a sample statistic.
  - Be able to classify a variable into quantitative or qualitative, and as nominal, ordinal, interval or ratio

- What is stats:
  - Stats is the study of how to collect, organize, analyze, and interpret numerical information and data 
  - Stats is both the science of uncertainty and technology of extracting information from data

- Individuals & Variables
  - Individuals are *people* or *objects* in a study.
    - Kidney dialysis patient
    - Baby born to a mother who smokes cigarettes
  - A variable is *characteristic* of the individual to be measured or observed.
    - Number of blood transfusions for that patient
    - Birth weight

- Parameter vs. Statistics
  - What is a population?
    - A population is a group of people or objects with a common theme.
    - When every member of that group is considered, it is a population.
    - Examples:
      - Theme: Nurses who work at Massachusetts General Hospital (MGH)
      - Population: Every single nurse who works into MGH
  - What is a sample?
    - A sample is a small portion of the population
    - It can be a representative sample, but it can also be a biased sample
  - Population Data → data from every individual in the population is available → Using entire population == census
  - Sample Data → data is only available from some individuals in population
  - Stats notation:
    - Capital **N** = Total population
    - Lower case **n** = Sample
  - ***Parameter***: is a measure that describes the entire population
    - Mean age of every American on medicare
  - ***Statistic*** is a measure that describes only a sample of a population
    - Mean age of Americans on Medicare estimated using the MBS

- Describing vs. Inferring
  - Descriptive statistics involve of organizing, picturing, and summarizing information from samples and populations
  - Inferential statistics involves methods of ***using information from a sample to draw conclusions regarding the population***.
  
- Four-level data classification:
  - Quantitative (Continuous): Numerical measurement of something → *"If I can make a mean out of it, it must be a quantitative variable"*
    - Interval: Difference between data values are meaningful ***and there is no true zero***
      - Time, for instance, cannot have a true zero
    - Ratio: Difference between data values are meaningful ***and there is a true zero***
      -  Systolic blood pressure has a true zero, if SBP is 0, you're dead.
  - Qualitative (Categorical): Refers to a characteristic of something.
    - Nominal: Applies to categories, labels or names, and cannot be ordered from smallest to largest, like eye color
    - Ordinal: Applies to data that can be arranged in order in categories, but the difference between data values cannot be determined or is meaningless


## Sampling

- Lecture goals:
  - Define sampling frame and sampling error
  - Give one example of how to do simple random sampling, and one example of how to do systematic sampling
  - Explain one reason to choose stratified sampling over other approaches
  - State two differences between cluster sampling and convenience sampling

- Sampling Definitions:
  - A sample is a part of a population. We often use it to infer from the sample to the population.
  - ***Sampling Frame***: a list of individuals from which a sample is actually selected. That is, the part of population from which you want to build a sample
    - Undercoverage: omitting population members from the sampling frame
  - ***Errors***:
    - ***Sampling error:*** the population mean will be different from your sample mean. This is a fact-of-life error. It can't be avoided. 
    - ***Non-sampling error***: this is an ***avoidable*** error. This comes with building a bad sampling frame, poor sample design, sloppy data etc.
  - ***Simulations***:
    - A numerical facsimile or representation of a real-world phenomenon
  - ***Simple Random Sampling (SRS)***:
    - A simple random sample of *n* measurements from a population is a subset of the population selected in such a manner that every sample of size *n* from the population has an equal chance of being selected.
    - Methods of SRS:
      - Number all the individuals in the population with a unique number and choose the number of individuals you want in your sample $n \choose k$
      - Generate a list of random numbers, assign these to the population and get the number of individuals you want in your sample. Here you can get the number in the order because you assigned them randomly 
    - ***Limits of SRS***:
      - You need a list, and you need a good list. If you don't have a good list, you risk undercoverage.
  - ***Stratified Sampling***:
    - First, our list of individuals is divided into groups, or strata (who share the same specific characteristic). This is a way to make it so that there are certain proportions of groups in the final sample.
    - After that, SRS takes place for each of the groups.
    - ***Limitations***:
      - Oversampling one group means your summary statistic is unbalanced
      - It is not possible to do without a list beforehand
      - It also is hard because you have to split the list into groups
  - ***Systematic Sampling***:
    - Can be done with or without a list!
    - ***How it's done:*** First, you arrange all individuals of the population in a particular order. Second, you pick a random individual as a start. Lastly, you pick the *kth* (every so many) member of the population in the sample.
    - Systematic Sampling ***CAN NOT*** be done when there is a pattern (periodicity) to the data (boy/girl/boy/girl)
  - ***Cluster Sampling***:
    - Cluster sampling it's the one you use when the problem is in a particular geographic location
    - ***Limitations***:
      - Sometimes, the people located in a cluster are all similar in a way that makes the problem hard to study. That is, it's hard to tell what is the independent cause of the problem we want to study. It's biased toward the type of people living in the area.
  - ***Convenience Sampling***:
    - Can be used under low risk circumstances
    - It's basically using results or data that are conveniently or readily obtained.
    - ***Limitations***:
      - There is a bias in every group.
      - Often miss important subpopulations (what stratified sampling addresses).
      - Results can be severely biased.
  - ***Multi-stage Sampling***:
    - Combination of sampling strategies layered in stages

- Conclusions:
  - Define sampling frame and sampling error:
    - Sampling frame it's the list of individuals from which the sample is actually selected. Sampling error it's the characteristic that the mean of your sample most certainly will be different from the mean of your population
  - Give one example of how to do simple random sampling, and one example of how to do systematic sampling:
    - One way of do an SRS it's by getting all unique individual records of a list and randomly selecting them to your sample. A systematic sample is done by arranging all individuals of a population in a particular order, choosing one of them randomly, and then choosing every *kth* individual.
  - Explain one reason to choose stratified sampling over other approaches
    - Stratified sampling should be used when you want to keep a certain representativeness in your study
  - State two differences between cluster sampling and convenience sampling
    - Cluster sampling is used when the problem we want to study is in a particular geographic location. Convenience sampling is used by using data conveniently available.

## Experimental Design

- Lecture goals:
  - State the steps of conducting a statistical study
  - Explain what a lurking variable is, and give an example
  - Define what a completely randomized experiment is.

- Basic guidelines for planning a statistical study:
  - State a hypothesis
    - Ex: Air pollution causes asthma in children who live in urban settings
  - Identify the individuals of interest
    - Ex: Children in urban settings
  - Specify the variable to measure
    - Ex: Air pollution and asthma
  - Determine if you'll use the entire population or a sample
    - Also choose the sampling method
  - Address ethical concerns before data collection
  - Collect the data
  - Use descriptive or inferential statistics to answer your hypothesis
  - Note any concerns about your data collection or analysis
    - Make recommendations for future studies  

- Experiment vs. Observational Study
  - Experiment: the purpose is to study the possible effect of a treatment or intervention on the variable measured
  - Observational: observations and measurements of individuals are taken. No treatment or intervention is assigned by the researcher.

- About replication:
  - Studies must be done rigorously enough to be ***replicated***
  - Replicating the results of observational studies and experiments is necessary for science to progress

- Avoiding bias in survey design:
  - Non-response and voluntary response: 
    - If many people refuse your survey, the people who do complete it are likely to have a biased opinion.
    - There may be a reason they do not complete your survey that has to do with how they feel about your survey topic.
  - Truthfulness of Response:
    - Respondents may lie on purpose
    - Respondents may lie inadvertently
  - Hidden bias:
    - Question wording may induce a certain response
    - Order of questions and other wording may induce a certain response
    - Scales of questions may not accurately measure responses
      - Do your feeling always fit on a scale of 1 to 5?
  - Interviewer influence:
    - Tell young female nursing students to ask elderly man about their sexual function doesn't seem the best way to get clean data
  - Vague wording:
    - Avoid vague terms used in a survey. The best way to do that is putting a number on it. "Have you waited more than x minutes?", not "Have you waited for a long time?"
    - If you must use vague terms, include grounding language. Set context.

- Lurking variable (variável de confusão):
  - A variable that is associated with a condition, but may not cause that condition
    - A lot of people who get involved in motorcycle accidents have tattoos, but tattoos don't cause motorcycle accidents.
    - Correlation ***it is not*** casualty. 



## Randomization

- Lecture subjects:
  - Steps in a completely randomized experiment
  - Placebo and placebo effect
  - Blocked randomization
  - Blinding

- Why randomize?
  - Helps prevent bias in selection member for each group.

## Frequency histogram, distribution and graphs

- Learning objectives:
  - Name two types of distributions and explain how they look
  - Define relative frequency and cumulative frequency
  - Describe a case in which a time-series graph would be appropriate
  - Describe the type of data plotted in a pie chart
  - Define class, upper class limit, and lower class limit

- Frequency histogram:
  - A frequency histogram is a specific type of bar chart made from data in a frequency table
  - The purpose of the chart is to **_reveal the distribution of the data_**.
  - Relative frequency is better for comparing two populations or two samples.
  - Are a special case of a bar graph that _**must**_ have:
    - Classes of a quantitative variable on the x-axis.
    - Frequency or relative frequency on the y-axis.

- Distributions:
  - It is the shape that is made if you draw a **line** along the edges of a histogram's bars.
  - The ones you should know:
    - Normal distribution
    - Uniform distribution
    - Skewed left/right distribution
      - If it's short on the left, it is skewed to the left.
    - Bimodal distribution
      - With two high points.

- Outliers:
  - Data values that are "very different" from other measurements in the dataset.

- Cumulative Frequency:
  - It's made by adding up all the classes before the class you are on
  - each cumulative frequency is equal to or higher than the last one.



- Time series graph:
  - Time in the x-axis
  - Time series data are made of measurements for the same variable for the same individual taken at intervals over a period of time.
  - They are useful to understand trends over time

- Bar Graph:
  - Can display qualitative or quantitative data
  - Length of bars represent variable's frequency or percentage of occurrence.
  - Histograms are a special case of a bar graph.
  - Problems with scale:
    - The scale you choose for the y-axis might influence how people see the data. A taller y-axis makes the differences between the categories look small, and a shorter y-axis makes the differences between the categories look way bigger than they really are.

- Pie charts: 
  - Used with counts of **mutually exclusive** frequencies

- Frequency Tables:
	- A table presenting how frequently a variable appears in our sample.
	- Classes of a frequency table:
		- ***Class***: an interval in the data
		- ***Class limit***: the lowest (*lower class limit*) and highest (*upper class limit*) value that can fit in a class
		- ***Class width***: how wide the class is. Is the upper class limit minus the lower class limit + 1. It says the number of elements inside that class.
		- ***Classes should be the same width***
		- Defining classes width with a formula:
			- Get the range of the sample ($maximum - minimum$)
			- Divide the result by the number of classes desired.
			- Increases this to the next integer.

- On All Graphs:
  - ***Always*** provide a title
  - Make the graph as clear as possible and don't let anything to be figured out.

- Conclusion:
  - The normal distribution looks like a bell and the uniform distribution is a straight line
  - Relative frequency is the observation of frequencies of a given class when compared to the whole population/sample. Cumulative frequency is the observation of the absolute frequency of each class added up by the absolute frequency of the previous classes.

## Measures of Central Tendency
- Learning Objectives:
	- Define trimmed mean and weighted average
- Measures of central tendency are concerned with knowing how much does the data have a tendency to go to the center
- They can only be asked about quantitative data
- Mode
	- The value that occurs most frequently.
	- It is possible to have no mode → when values are unique.
	- It is possible to have more than one mode.
	- The mode is not *resistant* or *stable*, that is, it changes very easily.
- Median
	- Is the center of the data.
	- You get the median by sorting the data and picking the number that is in the middle.
	- The median doesn't care much about the end of the data. Outliers don't bother it.
	- It *is resistant and stable*.

- Mean; Trimmed Mean & Weighted Average
	- Formula:
		- Sample: $\overline{X} = \frac{\sum{x}}{n}$
		- Population parameters: $\mu = \frac{\sum{x}}{N}$
	- Means are not resistant to outliers and not very stable.
	- One solutions to make the mean more *resistant* is to trim the data off each end so the outliers get cut off
		- How to make a 5% trimmed mean → Put the data in order → Remove 5% from the top and 5% from the bottom → Now take the mean out of the remaining data
	- When some values should count more towards the mean than others, you use a weighted average.
		- $\text{weighted mean} = \frac{\sum{xw}}{\sum{w}}$
		- $w$ is the weight of each observation of $x$

## Measures of Variation