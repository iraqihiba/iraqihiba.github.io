- 
- Date de début:
    - [April 4th, 2023](../Daily Document/April 4th, 2023.md) 
    - Objectif:
    - Données:
    - Démarche:
        - Describe the methods used to collect and analyze data
        - Explain the data analysis techniques used, including any statistical tests or models
        - Justify the selection of methods and techniques used in the project
        - Provide links to any tools or software used in the project
    - Résultats:
        - Present the findings of the data analysis in a clear and concise manner
        - Use visual aids such as graphs and tables to enhance the presentation of the results
        - Discuss the significance of the results in relation to the project objectives
        - Provide links to any data used in the project
- Step by step:
    - Project planning
        - Define the research question and objectives
            - The effect of smiling on leniency
            - Does smiling really increase leniency? 
            - Are different types of smiles differentially effective?
            - N9adou a way to detect the type of smile ou mba3d la clémence t9add 7assab dak smile li darat. En prenant one smile comme reference bach man7agrouch chi wa7ad ou man advantagewch chi wa7ad wakha les infos de crime houma hadouk
        - Identify data sources and collection methods
            - ![](local://C:/Users/Hiba Iraqi/remnote/remnote-614648b15118b8003413db97/files/D1AgP4rb1m7NQs7p-692PJaRs4ThizAr6Vh8lP1VAY3s8_oTycOG9H2TJM76a-VRVidEJiDG4386-nW6jh1cLyN352SqhSd66ZXOCnoMKcK4g2cDHMUhrq6PCUHkKyAG.png) ![](local://C:/Users/Hiba Iraqi/remnote/remnote-614648b15118b8003413db97/files/atkoPrd85WZ411DcrtUpQIVLbrdWalkGp4WMvnpdVPcUz5yM_-S0WmIaL1B-WF7g8IEhCirh-NVPtiHBLCldGe9KxBKAMQ42RkjU5HCZmmbTKRwZ32DEPKnIYjkBQixe.png) ![](local://C:/Users/Hiba Iraqi/remnote/remnote-614648b15118b8003413db97/files/IVZ6r1aRGhSUNWXUL2JxzxWtdDfnvhNRrzT5GSRgC4415p_SZZbH3Bs9O-Zhg0ZDtF0So59eGXdBi5_LBMwD2cv37hS__ywVqi9O8kA9T86pdJXij8nn8DLp5wF-ra2S.png) ![](local://C:/Users/Hiba Iraqi/remnote/remnote-614648b15118b8003413db97/files/YvQUL7pu6mNy6BFVonfvO4nQCyKzMYMwnvZ4znoEYg7m7LIPN17Czg7yyXZYx8Rd1O-V5FSZWP9qfLsZmiceBrqQrrrEstr1M4bsRRUw9rXbHy6AWQQdB7QHtwl9jgH6.png) 
            - ![](local://C:/Users/Hiba Iraqi/remnote/remnote-614648b15118b8003413db97/files/DA48vy4v4DA88uTHpq6liVK5rDVzIX-SijOhlbEjPlwexkPR_Ov_kCVXwgT5uVfh3hmmZrmZ6dK2QAyt1d2d21qy3nfu-vi733IM9A-uZ-f0eA7BFkaWCzZx74OQoeGx.png) 
            - 03:37 [April 4th, 2023](../Daily Document/April 4th, 2023.md) 
        - Determine the analysis techniques to be used
            - ANOVA
            - Descriptive Statistics:
                - Box Plot
                - Barplot
                - Scatter plot
                - Heat map
            - Inferential Statistics:
                - A contrast is used to test the hypothesis that the mean of the three smile conditions is different from the mean of the neutral condition
                - t squared
                - Dunnetts' Test
            - [April 4th, 2023](../Daily Document/April 4th, 2023.md) 18:34 
    - Data Collection
        - Collect and clean the data
            - From the online statbook website as text in lines emotion scale separated by a whitespace
        - Ensure data quality and integrity
            - The Publication author Marianne LaFrance is experienced in faces and has conducted multiple studies since and the paper is citated a lot. I tried to get the data from the origin but it isn't avaible in most websites used for that matter or on the publication page.
        - Prepare the data for analysis
            - From copying the observations from TOSB, I constructed a text file where each line was in shape of a tuple of observations. I then converted the data into a dataframe object and used pandas and openpyxl libraries to stuff it into an excel file. In the raw data, the author doen't use the ',' but rather '.' for decimal values which was a bother to convert into integer values. I didn't do it in python, but in Excel with the help of chatgpt. This is what it adviced me to do for future reference:
    - Data Analysis
        - Apply statistical methods and techniques to the data
            - BY SOFTWARE USED:
                - STATA Beginning: [April 5th, 2023](../Daily Document/April 5th, 2023.md)  15:00
                    - ANOVA
                    - Descriptive Statistics:
                        - Code:
                            - import excel "C:\Users\Hiba Iraqi\Desktop\Project\data.xlsx", sheet("Sheet1") firstrow
graph box Scale, over(Smile) title("Box Plot of the values of leniency for each type of smile")
graph bar (count), over (Smile) title("Frequency of each smile in the dataset")
graph bar (count), over(Scale) title("Bar_Plot Distribution of leniency ratings")
graph bar (mean) Scale, over (Smile) title("Means of leniency according to the type of smile")
ssc install vioplot, replace
vioplot Scale, over (Smile) title("Violin Plot of Leniency Ratings By Type of Smile")

                        - Box Plot
                        - Barplot
                        - Violin Plot
                        - Heat map
                    - Inferential Statistics:
                        - A contrast is used to test the hypothesis that the mean of the three smile conditions is different from the mean of the neutral condition
                        - t squared
                        - Dunnetts' Test
                - PYTHON
                    - Data formatting:
                    - import pandas as pd
f=open("C:/Users/Hiba Iraqi/Desktop/Project/Defining the research question and objectives/Sourires et clémence.txt",'r')
A=f.readlines()
#print(A)
alist = [line.rstrip() for line in open('C:/Users/Hiba Iraqi/Desktop/Project/Defining the research question and objectives/Sourires et clémence.txt')]
#print(alist)
w=[]
for i in alist:
    w+=i.split()
#print(w)
data=[]
for j in range(0,len(w),2):
    data.append((w[j],w[j+1]))
print(data)
#data+=tuple([1.2])
#print(data)
with open("C:/Users/Hiba Iraqi/Desktop/Project/Defining the research question and objectives/output.txt", 'w') as file:
    # Write each tuple to file as a string
    for tpl in data:
        file.write(str(tpl)+'\n')
print("Done")
df=pd.DataFrame(data,columns=['Smile','Scale'])
df.to_excel("C:/Users/Hiba Iraqi/Desktop/Project/data.xlsx",index=False)
print("Double done, go check")
print(df)

                - R
                    - Robust ANOVA (Scale doesn't follow a normal distribution)
                    - library(readxl)
#Warning message:
data <- read_excel("C:/Users/Hiba Iraqi/Desktop/Project/data.xlsx")
View(data)
attach(data)
boxplot(Scale~Smile)
# This error shows up: 
#Error in plot.new() : figure margins too large
# 7assab l 7aj chat-gpt and it works :
#Adjust the margins: You can also try reducing the 
#size of the margins around the plot using the par() function
par(mar = c(5, 4, 4, 2) + 0.1) # adjust the margins as needed
boxplot(Scale~Smile, data = data)
detach(data)
summary(aov(Scale~Smile, data=data))
pairwise.t.test(data$Scale, data$Smile, p.adjust.method = "bonferroni") 
attach(data)
# Blach Kruskal test ki comparer l medians
kruskal.test(Scale~Smile)
detach(data)
library(WRS2)
# Robust ANOVA: not enough significance
t1waybt(Scale ~ Smile, data = data, nboot = 5000)
# Robust post hoc test shows that the difference between felt and neutral is significant
mcppb20(Scale ~ Smile, data = data, nboot = 5000)

        - Interpret the results and draw conclusions
            - Only the means of the "neutral" category and the "false" category differ substantially
            - Displaying an image of a false-smiling person really does increase significantly the leniency accorded to them compared to a display of a neutral expression. 
            - It begs the question of the soundness of judgement when presented with a photo of the person being judged, and could spring interest in methods accounting for this gap at assisting the judges of moral conduct.
            - We have to take into account the sample from which we derived these conclusions, possible academic misconduct was what was judged, and only introductory psychology students participated as part of a course requirement
            - Judges may be on the lookout for impression management strategies, and a smile originally designed to subtly flatter may "boomerang" and result in even harsher punishment.
            - Each smile is operationally defined in terms of objective FACS codes. (Ekman &Friesen)
            - Only a picture was shown, not the actual person smiling en chair et en os.
            - 
            - Train of thoughts/analysis:
                - 08:25 [April 9th, 2023](../Daily Document/April 9th, 2023.md) 
                - With the help of descriptive statistics, we can see the difference in the distribution of probabilities for each category with the use of a violin plot. (A more sophisticated version of a boxplot), the approximated normality of each sub-category.
                - With the use of a boxplot for each category, we can kind of guess the difference between the means of each category for the variable Scale, notably for the "false" subset, compared to the "neutral" one.
                - We decide to use inferential statistics to test the hypothesis of the similarity of the means. 
                - The hypothesis that the quantitative variable Scale follows a normal distribution can be dismissed with a 95% confidence level.
                - Each category has similar standard deviations. We use Bartlett's test for equal variances. A p-value of  0.56, indicating that the assumption of equal variances across the groups is met. 
                - The observations are all independant from each other. The data is based on a study that mobilized data from 136 different students.
                - Just an observation: (Re-formulate using p-values). However, we fail to refute the hypothesis that the scale of each category of smile follows a normal distribution within a 85% confidence level.
                - Each group has 34 observations each. (How to judge if enough of a sample size?)
                - The dependent variable, Scale, is continuous and the independent variable Smile  is categorical with three or more levels. 
                - All the conditions for a one-way ANOVA are verified other than the normality of the distribution. We later on can do a robust one-way ANOVA on R, seeing that the overall distribution is not normal. (Trimmed means)
                - The null hypothesis for the ANOVA is that there is no difference in the mean value of the "Smile" variable across the four groups, while the alternative hypothesis is that at least one of the groups differs significantly from the others. 
                - For now, we use an regular one-way ANOVA, "The Bartlett's test fails to prove that the variances are different."  The output indicates that there is a significant difference in the means  of the "Smile" variable across the four groups, with a p-value of  0.0182. This means that we can reject the null hypothesis and conclude  that there is evidence of a significant difference in mean "Smile"  scores among the four groups.  
                - T-testing between the different categories shows a difference:
                    - This indicates that there is a statistically significant difference in  the mean values of "Scale" between the two groups at the 0.05  significance level.  
                - Using R for advanced analysis:
                    - Pairwise comparisons using t tests gives a p-value of 0.011 for neutral-false. Otherwise, all other p-values are greater than 0.05. (P-value adjustment method: bonferroni)
                        - Using the Bonferroni correction ensures that the overall probability of  making a Type I error does not exceed the desired level, but it comes at  the cost of reduced statistical power. That is, the Bonferroni  correction makes it more difficult to reject the null hypothesis, even  when it is true.  
                        - We use the Bonferroni correction to adjust the p-values of pairwise  comparisons when conducting multiple t-tests. The Bonferroni correction  is a method of controlling the family-wise error rate (FWER) by  adjusting the alpha level of each individual test.  
                    - Using the Robust One-Way ANOVA  
                        - Bootstrap version of the heteroscedastic one-way ANOVA for trimmed means   
                        - Test the hypothesis of equal trimmed means using a percentile t bootstrap method  
                        - Put another way, groups probably differ when null hypotheses are rejected with standard methods, but in many situations, standard methods are the least likely to find a difference, and they offer a poor summary of how groups differ and the magnitude of the difference.  (Bal7a9 we found chi 7aja b l one-way ANOVA l3adiya but none b lakhra)
                        - Reference: [Introduction to Robust Estimation and Hypothesis Testing - 3rd Edition](https://www.elsevier.com/books/introduction-to-robust-estimation-and-hypothesis-testing/wilcox/978-0-12-386983-8)
                    - Robust post hoc test shows that only the difference between felt and neutral is significant
                    - 13:19 [April 9th, 2023](../Daily Document/April 9th, 2023.md) 
        - Meaningfulness of the results
    - Report writing
        - Develop an outline and structure for the report
        - Write the report, including the introduction, objectifs données démarche (methodology), results, discussion and conclusion sections
        - Edit and proofread the report to ensure clarity and coherence
    - Review and presentation
        - Review and finalize the report
        - Prepare a presentation for the key findings and recommendations
        - Present the report and answer any questions or feedback from bnadam li isswal 3la l project 
