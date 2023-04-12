# Statistical Evaluation of The Contribution Of Smiling In Increasing Clemency 
*Using Pandas,Stata &R*
## Defining the research questions and objectives:
Does smiling really increase leniency?

Do different types of smiles differ in effectiveness?
## Identifying data sources and collection methods:
[Why Smiles Generate Leniency](https://journals.sagepub.com/doi/10.1177/0146167295213002)

136 students assumed the role of a member in a college disciplinary panel considering a possible case of academic misconduct.

An equal portion was shown the incriminating files, and arbitrarily a photo of either the miserable, neutral, fake or felt smile.

## Determining the analysis techniques to be used, including any statistical tests:

### Descriptive Statistics: 
Box Plot ~ Bar plot ~ Violin plot 

### Hypothesis-testing: 
One-way ANOVA ~ Post-hoc tests. ~There are still things to add~

*Why these in particular were used is talked about later on.*
## Data Collection Cleaning Quality Preparing for analysis:
### Collecting and cleaning the data:
Initially stored as lines of text
### Ensuring data quality and integrity:
Marianne LaFrance is experienced in face analysis (FACS manual), The Study's imapact is of 4560.
### Preparing the data for analysis:
Converting the text file into an excel file with the appropriate types for data processing later on  with the use of Python and the Pandas library + changing the type of a column directly in Excel
```python
			import pandas as pd
			f=open("C:/Users/Hiba Iraqi/Desktop/Project/Defining the research question and objectives/Sourires et clémence.txt",'r')
			A=f.readlines()
			alist = [line.rstrip() for line in open('C:/Users/Hiba Iraqi/Desktop/Project/Defining the research question and objectives/Sourires et clémence.txt')]
			w=[]
			for i in alist:
    				w+=i.split()
			data=[]
			for j in range(0,len(w),2):
    				data.append((w[j],w[j+1]))
			with open("C:/Users/Hiba Iraqi/Desktop/Project/Defining the research question and objectives/output.txt", 'w') as file:
    			# Write each tuple to file as a string
    			for tpl in data:
        			file.write(str(tpl)+'\n')
			df=pd.DataFrame(data,columns=['Smile','Scale'])
			df.to_excel("C:/Users/Hiba Iraqi/Desktop/Project/data.xlsx",index=False)
			print(df)
```
			
## Data Analysis
### Descriptive Statistics using Stata
We can kind of guess the **difference** between the **means** of each category for the variable Scale (Scale of leniency, a high value means the greatest clemency shown to the cheater) , notably for the **"false"** subset **compared** **to** the **"neutral"** one.
![BoxPlot](https://i.imgur.com/8BjwqVI.png) 

The observations are all **independent** from each other. The data is based on a study that mobilized data from **136** different students. Each group has **34** observations **each**.
![Frequency_Subset](https://i.imgur.com/hEQLQ57.png)

**Scale** is seemingly **not** **normally distributed**
![Distribution](https://i.imgur.com/VHdc6aE.png)

We can see the **difference** in the **distribution** of probabilities for each category with the use of a **violin plot**. 

![Violin Plot](https://i.imgur.com/ZCQAFtv.png)

We decide to use **inferential** statistics to test the **hypothesis** of the **similarity** of the **means**.
### Hypothesis Testing Mix Of Stata & R
### Stata 
The hypothesis that the quantitative variable Scale follows a normal distribution can be dismissed with a 95% confidence level. with the help of a Shapiro-Wilk W test and also  with a Skewness and Kurtosis test, as seen below:

![Skewness and Kurtosis](https://i.imgur.com/UTjm5GU.png)

![Shapiro-Wilk test](https://i.imgur.com/fkWnpoX.png)

Each category has **similar standard deviations**. We use **Bartlett's test** for equal variances. A p-value of  0.56, indicating that the assumption of equal variances across the groups is met. 

![Barlett's test](https://i.imgur.com/RB05khg.png)

The dependent variable, Scale, is continuous and the independent variable Smile  is categorical with three or more levels. 

All the conditions for a one-way ANOVA are verified other than the normality of the distribution. We later on can do a robust one-way ANOVA on R, seeing that the overall distribution is not normal. (Trimmed means)

The null hypothesis for the ANOVA is that there is no difference in the mean value of the "Smile" variable across the four groups, while the alternative hypothesis is that at least one of the groups differs significantly from the others.

T-testing between the different categories shows a difference : This indicates that there is a statistically significant difference in  the mean values of "Scale" between the two groups at the 0.05  significance level. 

## Using R for advanced analysis:
Pairwise comparisons using t tests gives a p-value of 0.011 for the combination of  neutral-false.

Otherwise, all other p-values are greater than 0.05. (P-value adjustment method: bonferroni)
``` R
    library(readxl)
    data <- read_excel("C:/Users/Hiba Iraqi/Desktop/Project/data.xlsx")
    attach(data)
    par(mar = c(5, 4, 4, 2) + 0.1)
    boxplot(Scale~Smile, data = data)
    detach(data)
    summary(aov(Scale~Smile, data=data))
    pairwise.t.test(data$Scale, data$Smile, p.adjust.method = "bonferroni") 
``` 
![Pairwise t-tests](https://i.imgur.com/UulhuEm.png)

- Using the Bonferroni correction ensures that the overall probability of  making a Type I error does not exceed the desired level, but it comes at  the cost of reduced statistical power. That is, the Bonferroni  correction makes it more difficult to reject the null hypothesis, even  when it is true.  
- We use the Bonferroni correction to adjust the p-values of pairwise  comparisons when conducting multiple t-tests. The Bonferroni correction  is a method of controlling the family-wise error rate (FWER) by  adjusting the alpha level of each individual test.  
#### Using the Robust One-Way ANOVA  
    It is robust even when normality isn't verified
    
``` R
    library(WRS2)
    t1waybt(Scale ~ Smile, data = data, nboot = 5000)
```
![Robust one-way ANOVA](https://i.imgur.com/jv3bz6S.png)
- Bootstrap version of the heteroscedastic one-way ANOVA for trimmed means   
- Tests the hypothesis of equal trimmed means using a percentile t bootstrap method  
- Reference: [Introduction to Robust Estimation and Hypothesis Testing-3rd Edition](https://www.elsevier.com/books/introduction-to-robust-estimation-and-hypothesis-testing/wilcox/978-0-12-386983-8)
#### Robust post hoc test
It shows that only the difference between felt and neutral is significant. 

(The only confidence interval that doesn't contain the zero)
``` R
    mcppb20(Scale ~ Smile, data = data, nboot = 5000)
```
![Post-hoc Robust test](https://i.imgur.com/1ydRZ12.png)

## Interpreting the results and drawing conclusions

### Only the means of the "neutral" category and the "false" category differ substantially
Displaying an image of a false-smiling person really does increase significantly the leniency accorded to them compared to the display of a neutral expression. 

It begs the question of the soundness of judgement when presented with a photo of the person being judged, and could spring interest in methods accounting for this gap at assisting the judges of moral conduct.

#### Shortcomings:
- We have to take into account the sample from which we derived these conclusions, possible academic misconduct was what was judged, and the only participants were  introductory psychology students who did as part of a course requirement.
- Judges may be on the lookout for impression management strategies, and a smile originally designed to subtly flatter may "boomerang" and result in even harsher punishment.
- Only a picture was shown, not the actual person smiling  *en chair et en os*.
