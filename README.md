# First UCI Bootcamp Project
## Members
* Gurcharan Singh
* Abhishek Bhatt
* Steven Ortiz
* Peter Lai

# Large Datasets
* globalterrorismdb_0718dist.csv
* gtd_0717.csv

=> https://drive.google.com/open?id=1E3SeAIPrLpAnRixN3oEM6VmIDJGuQ9fT

# Our Design on addressing the question – Does Terrorism work?

* Our scope is to showcase the impact of the terrorist attacks on the country’s GDP growth, because GDP is the direct indicator and measure of a country’s economy and how well it is doing. 
* Our analysis are limited to 8 regions of the world by selecting 12 countries as representative of those regions to study in the period of a decade (2008-2018)
* Would a country’s GDP growth rate (%) and Currency (exchange rate based on US dollars) be affected in certain years that the terrorist attacks have thrive? Would the GDP improve or decline? Would currency strengthen or weaken? 
* Is the number of terrorist attacks each year going to affect each years GDP and Currency exchange rate, and if there is correlation between the three.

# Hypothesis
Over the course of 10 years, if the number of attacks in a country increases from one year to the next, then it will have a negative effect on that year’s GDP growth rate. If the number of attacks in a country decrease from one year to the next, it will have a positive effect on that year’s GDP growth rate. 
(We are not including Currency, only GDP)
# Null Hypothesis
The GDP growth rate of each year is not affected by the number of attacks that occur in that country. (Our data, should show, terrorist attack will have affect on GDP).

# Countries and Regions for Analysis
* Asia: Philippines, China, Pakistan, Georgia
* Europe: United Kingdom, Ukraine
* Africa: Somalia
* Middle East: Iraq
* North America: United States
* Central America: Honduras
* South America: Colombia
* Oceania: Australia


# Data Cleaning Process
1. We got terrorism data from Global Terrorism Data, GDP data from The World Bank, Currency data from Foreign exchange rates API. Raw data are  Downloaded and cleaned as per our requirement and hypothesis.
2. Our main thoughts were to get insights if terrorist attacks have any relation to country's GDP, but in fact there isn't any.
3. GTD dataset was huge to manage and clean to the required output.
4. Insights are in Jupyter Notebook
5. Analysis again someone need to say from the notebook and plots. Exploring the GTD and GDP data, merging on year and country, so that we can understand if there is any relationship between attacks happened and GDP over the period on 10 years from 2008 to 2017

# Conclusion ([Analysis](Analysis/GTD_GDP_Analysis.md))
* Terrorism can be successful in causing turmoil in specific region of the world (such as Iraq), but when it comes to accomplishing broader strategic goals, such as hurting a country’s economic climate or citizen morale, the data shows no correlation between Number of Attacks and GDP % change or Currency % change. 
* Terrorism seems to not able to deter Import/Export part of the GDP equation, at least our data did not show a direct impact. 
* Possible reason could be nation-states are too militarily and economically strong to be affected by terrorists, and the government structure are in place to sustain those attack (Pakistan or United States). 
* Give it up for the counter terrorism intel!!







