# Impact des changements climatiques au Maroc, caractérisation temporelle de la température, pluviométrie et du décalage saisonnier
## Introduction
L'impact du changement climatique sur le secteur agricole entraîne des répercussions directes sur la sécurité alimentaire, l'économie agricole et la durabilité environnementale. L’amplitude de l’impact dépend tour à tour de l'exposition aux aléas climatiques, de la sensibilité des produits, terres et pratiques agricoles à ces changements ainsi que des capacités d’adaptation du secteur agricole. 

  L’exposition aux aléas climatiques est caractérisée à partir de l'évolution des séries temporelles de la température et des précipitations par région. Les régions connaissant une augmentation des températures et des variations importantes des précipitations sont plus exposées aux risques liés au climat, notamment les canicules, les inondations, les sécheresses et les tempêtes, qui peuvent avoir des effets dévastateurs sur les cultures et le bétail.  

De plus, la sensibilité des produits agricoles, des terres et des pratiques agricoles à ces changements est cruciale. Certaines cultures, sols et pratiques agricoles sont plus vulnérables aux nouvelles conditions climatiques, ce qui peut entraîner des rendements plus faibles ou des pertes de récoltes.  

Enfin, les capacités d'adaptation du secteur agricole, telles que l'adoption de techniques de culture résilientes au climat et le développement de systèmes d'alerte précoce, sont essentielles pour atténuer les impacts du changement climatique sur l'agriculture. Une compréhension approfondie de ces facteurs interconnectés est indispensable pour élaborer des stratégies visant à garantir la sécurité alimentaire marocaine à long terme. 

L’intérêt est porté sur la caractérisation de l’évolution des variables climatiques  afin d’évaluer l’exposition au changement climatique des différentes régions marocaines. 
## Objectifs
On œuvre à caractériser l’impact des changements climatiques sur la température, pluviométrie par région et aussi le décalage saisonnier
## Méthodologie
### Mesure de l’impact du changement climatique sur le décalage saisonnier
Elaboration d’un outil d’aide à l’interprétation des données climatiques et des différentes phases dont passe l’évolution de la température et de la précipitation. L’objectif primaire était de parvenir à définir ce qu’est une saison à l’aide de cet outil en agrégant les différentes périodes d’évolution. 

Quantifier la position temporelle des change-points usuels (où la distribution conjointe de mean_temp et precipitation change) et sa variance à l’aide des données historiques, ceci pour calculer la déviation par rapport à ces valeurs des change-points de nos observations actuelles. Interpréter empiriquement la valeur de ces change-points On utilise la fonction e.divisive() du package ecp qui fait de l’analyse non paramétrique des points de changement multiples de données multivariées. Cette approche permet de détecter des changements de distribution non seulement marginale mais aussi conjointe. 

Ici, plusieurs points de changement sont estimés en appliquant de manière itérative une procédure de localisation d'un seul point de changement. À chaque itération, l'emplacement d'un nouveau point de changement est estimé de manière à diviser un segment existant. Par conséquent, la progression de cette méthode peut être schématisée sous la forme d'un arbre binaire. Dans cet arbre, le nœud racine correspond au cas où il n'y a pas de point de changement et contient donc toute la série temporelle. Tous les autres nœuds non-racine sont soit une copie de leur parent, soit correspondent à l'un des nouveaux segments créés par l'ajout d'un point de changement à leur parent. 

La signification statistique d'un point de changement estimé est déterminée par un test de permutation, étant donné que la distribution de la statistique du test dépend des distributions des observations, qui sont généralement inconnues. Supposons qu'à la k -ème itération, l'ensemble actuel de points de changement ait segmenté la série temporelle en k segments S1, S2, . . ., Sk, et que nous ayons estimé le nombre de points de changement dans la série temporelle. Sk, et que nous avons estimé l'emplacement du prochain point de changement comme étant ˆτk, qui a une valeur de statistique de test associée de q0. 

Nous obtenons ensuite notre échantillon permuté en permutant les observations dans chacun des segments S1, . . . , Sk. Ensuite, conditionnellement aux emplacements des points de changement précédemment estimés, nous estimons l'emplacement du point de changement suivant dans notre échantillon permuté, ˆτk,r, ainsi que la valeur de la statistique de test qr qui lui est associée. Notre valeur p approximative est alors calculée comme ˆp = #{r : qr ≥ q0}/(R + 1), où R est le nombre total de permutations effectuées 
### Caractérisation des variables climatiques : température et précipitations  
#### Source de données : Crop Growth Monitoring System – Maroc 
Un système national de suivi de la campagne agricole et de prédiction agro météorologique des récoltes céréalières, appelé « CGMS-MAROC » (Crop Growth Monitoring System – Maroc), a été initié par l’Institut National de la Recherche Agronomique (INRA), dans le cadre du projet E-AGRI. Le CGMS-MAROC est piloté par l’INRA et géré en consortium formel avec la Direction de la Météorologie Nationale (DMN) et la Direction de la Stratégie et des Statistiques (DSS). Le développement de CGMS-MAROC a été possible grâce à une collaboration technologique avec des institutions de recherche internationales, à savoir : l’Institut Flamand pour la Recherche et la Technologie (VITO), le Centre de Recherche Commun de l’Union Européenne (JRC), l’Institut de Recherche de l’Université de Wageningen (Alterra) et l’Université de Milan (UNIMI). Le CGMS-MAROC est ainsi le premier système opérationnel de suivi de la campagne agricole et de prédiction agrométéorologique des récoltes céréalières au Maroc, institutionnalisé par un partenariat stratégique qui permet son développement et sa pérennisation. 
 
Le CGMS-MAROC surveille le développement des cultures, à partir des conditions météorologiques, des caractéristiques des sols et des paramètres des cultures. 
 
Le CGMS-MAROC est constitué de trois niveaux : 
 
Niveau 1 : La collecte des données météorologiques et leur interpolation sur une grille carrée de 9x9 km sur tout le territoire national ; 
 
Niveau 2 : La simulation de la croissance des cultures, par plusieurs modèles de simulations agrométéorologiques ; 
 
Niveau 3 : La prédiction des récoltes à partir d’une approche combinée, mettant à contribution des analyses statistiques paramétriques et non paramétriques des données météorologiques, des données de simulation et des données satellitaires. 
##### Format des données  
Observations journalières depuis le 01/01/1980 au 23/09/2023 des températures maximales, minimales, moyennes et une pluviométrie cumulative s'annulant chaque Septembre de chaque région
#####  Préparation des données 
-Conversion du format .xls a .csv à l’aide d’Excel 

-Traitement des données et préparation à l’analyse. Les données manquantes sont remplacées par une méthode d’imputation par la dernière observation avec un check sur leur qualité avant et après imputation à l’aide de statistiques de synthèse.  
##### Analyse et production de graphiques  
-Désagrégation de la variable pluviométrie pour dégager une pluviométrie journalière 

On opte pour une approche d’analyse qui prend en considération l’aspect saisonnier ainsi : 

Une saison débute du premier du mois et est caractérisée comme suit : Printemps: [Avril,Juin] Eté: [Juillet, Septembre] Automne: [Octobre,Décembre] Hiver: [Janvier,Mars] 
On génère depuis les températures moyennes journalières une série temporelle annuelle de températures maximales et minimales saisonnières. On utilise pour cela la méthode d’estimation de la densité par noyau pour couper les extrémités de la distribution afin de ne pas inclure les valeurs aberrantes et être le plus fidèle aux conditions réelles de stress thermique. 

Ainsi, on ne s’intéresse qu’aux valeurs qui représentent 95% des variations enregistrées. Et on élimine les queues a droite et a gauche de la distribution a l’aide de la fonction de distribution cumulative. 

De ces intervalles on peut voir comment évolue leur étendue chaque année, est ce que ca augmente ou diminue. Dans le cas ou la température minimale augmente, si l’étendue reste constante, on atteint encore plus de températures chaudes, si l’étendue diminue, peut-etre que l’on n’atteint pas des températures qui sont vraiment chaudes, il faut comparer l’évolution de l’étendue et l’évolution de la température minimale dans ce cas. Si l’étendue augmente, forcément on atteint des températures encore plus chaudes que si l’étendue était constante, et ainsi de suite. 

On génère des graphes de temperature_intervals, range_of_variation, upper_bounds et lower_bounds et précipitations. 

Temperature intervals : Intervalle de variation de températures moyennes 

Range of variation : Une mesure de l’étendue de l’intervalle de variation des températures moyennes  

Upper bounds : Températures maximales atteintes a partir des températures moyennes  

Lower bounds : Températures minimales atteintes a partir des températures moyennes  

Total_rainfall: Précipitations 

On cherche les régions ayant le moins de variabilité en termes d’intervalles de température par saison. On utilise pour cela le coefficient de variation. CV=(Ecart-type /Moyenne​)×100. 
## Résultats
### Mesure de l’impact du changement climatique sur le décalage saisonnier  
L’inter-variabilité entre les années des données climatiques est importante même si on ne se restreint qu’a l’intervalle [1985,2020] et l’on ne s’adonne pas a analyser les années 2021,2022,2023 ou l’évolution est présumée bi-saisonnière. 

Reproductibilité des résultats : J’ai entamé une série de tests pour vérifier si l’étendue temporelle des données influence la détection des différentes phases que traversent les données climatiques. On rappelle qu’a chaque itération, l'emplacement d'un nouveau point de changement est estimé de manière à diviser un segment existant. Par conséquent, la progression de cette méthode peut être schématisée sous la forme d'un arbre binaire. Il est possible si l’on diminue l’étendue temporelle, par exemple de 2 ans a 1 an que les résultats ne soient plus les mêmes. 

Fort heureusement, les résultats de détection au bout d’un an et de deux ans et plus sont les mêmes. Ceci aurait été un problème non négligeable car la complexité de notre méthode n’est pas linéaire. C’est-à-dire qu’au fur et à mesure qu’on augmente les observations, le temps de traitement n’augmente pas avec la même proportion, il explose. Dans notre cas, la complexité de calcul est O(kT^2), où k est le nombre de points de changement estimés et T le nombre d'observations. On suppose que k est constant et ne varie pas beaucoup au cours des ans. Ce qui est vérifié dans le cas de nos données. Prenons tr le temps de traitement d’un an. Le temps de traitement de [1985,2020] dans notre cas sera de 36*36*tr c-à-d 1296*tr. Ainsi, s’il nous prend 1 minute pour analyser 1 an, 36 ans nous prendra 22 heures. 

Par rapport à la fiabilité : 

En appliquant cette technique aux données de Casablanca-Anfa, on remarque que le nombre de phases dont passe l’évolution des données climatiques reste assez restreinte entre 1985 et 2020.Entre 6 et 8 environ. 2010 est une année aberrante à cause des inondations.
![Nombre de change points par année](https://imgur.com/a/p3VKig1) Source: Auteur
#### Fonctionnement outil: données
On insère les données climatiques brutes de la DMN, et le chemin du dossier ou on veut stocker les images dans la fonction automation_of_plots. 

Et voici le résultat : L’analyse à travers les années devient plus facile. 
![Tracés de edivisive à travers les ans d'une région](https://imgur.com/a/dcl619R)
Source: Auteur
Voici un aperçu de l’année 1985. Bleu=Hiver Vert= Printemps Rouge=Eté Orange=Automne (Le printemps débute du 1er avril au 30 Juin) et ainsi de suite pour les autres saisons. 
![Analyse des points de changements de l'année 1985](https://imgur.com/a/N9bGtpq)
On peut faire de même pour le changement de l’allure des précipitations. 
Ça reste un outil d’aide à l’interprétation des données climatiques et des différentes phases dont passe la température et la précipitation. 
### Caractérisation des variables climatiques : température et précipitations  
