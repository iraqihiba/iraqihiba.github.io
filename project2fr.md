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
