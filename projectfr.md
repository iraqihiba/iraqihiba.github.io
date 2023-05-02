# Évaluation statistique de l'impact du type de sourire accompagnant le dossier d'un fraudeur sur le degré de clémence qu'on lui accorde 
*Utilisation de Pandas, Stata et R*
## Defining the research questions and objectives:
Le sourire augmente-t-il vraiment la clémence accordée ?

Les différents types de sourires ont-ils une efficacité différente ?
## Identification des sources de données et des méthodes de collecte:
[Why Smiles Generate Leniency](https://journals.sagepub.com/doi/10.1177/0146167295213002)

136 étudiants ont joué le rôle d'un membre d'un comité disciplinaire d'un établissement d'enseignement supérieur chargé d'examiner un éventuel cas de mauvaise conduite (triche).

On a montré à une même proportion de la population le dossier de l'accusé accompagné soit d'une photo d'un sourire misérable, neutre, faux ou ressenti.

## Détermination des techniques d'analyse à utiliser, y compris les éventuels tests statistiques :

### Statistiques descriptives: 
Boîte à moustaches ~ Graphique à barres ~ Diagramme en violon

### Tests d'hypothèse : 
Analyse de variance unidirectionnelle ~ Tests Post-hoc 

~Il y a encore des choses à ajouter~

*La raison pour laquelle ils ont été utilisés en particulier est expliquée un plus loin.*
## Collecte des données Nettoyage Qualité Préparation de l'analyse :
### Collecte et nettoyage des données :
Initialement stockées sous forme de lignes de texte
### S'assurer de la qualité et de l'intégrité des données :
Marianne LaFrance est expérimentée dans l'analyse des visages (manuel FACS). L'impact de l'étude est de 4560.
### Préparation des données pour l'analyse :
Conversion du fichier texte en fichier Excel avec les types appropriés pour le traitement ultérieur des données à l'aide de Python et de la bibliothèque Pandas + modification du type d'une colonne directement dans Excel
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
			
## Analyse des données
### Statistiques descriptives à l'aide de Stata
On peut deviner la **différence** entre les **moyennes** de chaque catégorie pour la variable Scale (Échelle de clémence : une valeur élevée signifie la plus grande clémence à l'égard du tricheur.), notamment pour le sous-ensemble **"faux"** **comparé à** celui **"neutre"**.

![BoxPlot](https://i.imgur.com/8BjwqVI.png) 

Les observations sont toutes **indépendantes** les unes des autres. Les données sont basées sur une étude qui a mobilisé les données de **136** étudiants différents. Chaque groupe a **34** observations **chacun**.
![Frequency_Subset](https://i.imgur.com/hEQLQ57.png)

**Scale**, apparemment **ne suit pas** la  **loi normale**

![Distribution](https://i.imgur.com/VHdc6aE.png)

Nous pouvons voir la **différence** dans la **distribution** des probabilités pour chaque catégorie à l'aide d'un **diagramme de Violon**. 

![Violin Plot](https://i.imgur.com/ZCQAFtv.png)

Nous décidons d'utiliser les statistiques **inférentielles** pour tester l'**hypothèse** de **similarité** des **moyennes**.
### Tests d'hypothèse avec  Stata et R
### Stata 
L'hypothèse selon laquelle la variable quantitative Échelle suit une distribution normale peut être rejetée avec un niveau de confiance de 95 %, à l'aide d'un test W de Shapiro-Wilk et d'un test de Skewness et de Kurtosis, comme indiqué ci-dessous :

![Skewness and Kurtosis](https://i.imgur.com/UTjm5GU.png)

![Shapiro-Wilk test](https://i.imgur.com/fkWnpoX.png)

Chaque catégorie a des **écarts types similaires**. Nous utilisons le **test de Bartlett** pour vérifier l'égalité des variances. La valeur p est de 0.56, ce qui indique que l'hypothèse d'égalité des variances entre les groupes n'est pas à rejeter. 

![Barlett's test](https://i.imgur.com/RB05khg.png)

La variable dépendante Scale, est continue et la variable indépendante, le sourire, est nominale avec trois niveaux ou plus. 

Toutes les conditions d'une ANOVA unidirectionnelle sont vérifiées, à l'exception de la normalité de la distribution. Nous pourrons par la suite effectuer une ANOVA robuste unidirectionnelle sur R, en constatant que la distribution globale n'est pas normale. (Moyennes ajustées)

L'hypothèse nulle de l'ANOVA est qu'il n'y a pas de différence dans la valeur moyenne de la variable "sourire" entre les quatre groupes, tandis que l'hypothèse alternative est qu'au moins un des groupes diffère significativement des autres.

 

## Utilisation de R pour une analyse avancée :
Les comparaisons par paires à l'aide de tests t donnent une valeur p de 0,011 pour la combinaison neutre-faux.

Pour les autres paires, toutes les valeurs p sont supérieures à 0,05. (Méthode d'ajustement de la valeur p : bonferroni)
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

- L'utilisation de la correction de Bonferroni garantit que la probabilité globale de commettre une erreur de type I ne dépasse pas le niveau souhaité, mais au prix d'une réduction de la puissance statistique. En d'autres termes, la correction de Bonferroni rend plus difficile le rejet de l'hypothèse nulle, même si elle est vraie.  
- Nous utilisons la correction de Bonferroni pour ajuster les valeurs p des comparaisons par paires lors de tests t multiples. C'est une méthode qui permet de contrôler le taux d'erreur de la famille (FWER) en ajustant le niveau alpha de chaque test individuel.  
#### Utilisation de l'ANOVA robuste unidirectionnelle  
    Elle est robuste même lorsque l'hypothèse de normalité n'est pas vérifiée.
    
``` R
    library(WRS2)
    t1waybt(Scale ~ Smile, data = data, nboot = 5000)
```
![Robust one-way ANOVA](https://i.imgur.com/jv3bz6S.png)
- Version bootstrap de l'ANOVA hétéroscédastique à un facteur pour les moyennes ajustées   
- Teste l'hypothèse d'égalité des moyennes tronquées en utilisant une méthode bootstrap t percentile.  
- Référence: [Introduction to Robust Estimation and Hypothesis Testing-3rd Edition](https://www.elsevier.com/books/introduction-to-robust-estimation-and-hypothesis-testing/wilcox/978-0-12-386983-8)
#### Test post hoc robuste
Il montre que seule la différence entre les catégories ressenti et neutre est significative. 

(Le seul intervalle de confiance qui ne contient pas le zéro)
``` R
    mcppb20(Scale ~ Smile, data = data, nboot = 5000)
```
![Post-hoc Robust test](https://i.imgur.com/1ydRZ12.png)

## Interprétation des résultats et conclusions

### Seules les moyennes de la catégorie "neutre" et de la catégorie "faux" diffèrent sensiblement
L'affichage de l'image d'une personne au faux sourire augmente réellement et significativement l'indulgence à son égard par rapport à l'affichage d'une expression neutre. 

Cela soulève la question de la justesse du jugement lorsqu'on dispose d'une photo de la personne jugée, et pourrait susciter l'intérêt pour des méthodes qui tiennent compte de ce paramètre dans l'assistance aux juges de conduite morale.

#### Lacunes :
- Nous devons tenir compte de l'échantillon à partir duquel nous avons tiré ces conclusions, des tentatives de triche  académiques possibles ont été jugées, et les seuls participants étaient des étudiants en introduction à la psychologie qui ont fait cela dans le cadre d'un cours obligatoire.
- Les juges peuvent être à l'affût de stratégies de gestion de l'impression, et un sourire conçu à l'origine pour flatter subtilement peut "revenir en boomerang" et entraîner une punition encore plus sévère.
- Seule une photo a été montrée, et non la personne qui sourit *en chair et en os*.



    





    


