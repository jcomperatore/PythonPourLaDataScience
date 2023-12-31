# Etude de l'orientation politique dans les questions écrites de l'Assemblée nationale

*Ce projet est réalisé dans le cadre du cours de Python pour la Data Science donné par Lino Galiana à l'ENSAE Paris en 2023.* 

### Objectif et méthodologie

L'objectif de ce dépôt est d'essayer de prédire l'orientation politique d'un texte. Nous voulons donc réaliser un algorithme NLP pour, après un apprentissage sur un corpus de textes orientés, prédire l'orientation politique de l'auteur inconnu d'un texte.

Le projet est organisé en trois parties : 
  1) Récupération des données
  2) Première étude descriptive
  3) Modélisation


## 1) Récupération des données

### Récupération de données brutes

Les textes dont nous avions besoin devaient être clairement attribuables à une opinion politique. Pour cela, les discours des députés ou les programmes de campagnes des candidats semblaient être des candidats crédibles. Cependant, les programmes des candidats pouvaient représenter un corpus un peu maigre, et être plus compliqués à récupérer. 
D'autre part, les questions au gouvernement posées par les députés présentaient plusieurs avantages : elles sont nombreuses, variées, et simples à récupérer.

En effet, elles sont accessibles pour un utilisateur à partir d'un outil de recherche [disponible ici](https://www2.assemblee-nationale.fr/recherche/questions).

En y regardant de plus près, on constate que toutes les questions concernant la XVIème legislature sont disponibles à des adresses du type [https://questions.assemblee-nationale.fr/q16/16-XXXXXQE.htm](https://questions.assemblee-nationale.fr/q16/16-8987QE.htm) où XXXX est le numéro de la question. 

Pour toutes les récupérer, nous avons donc mis en place un algorithme de Scrapping qui boucle sur tous les numéros de pages, afin d'obtenir toutes les questions. Cet algorithme est disponible sous sa forme naïve dans le notebook [`Scraping Dataframe`](https://github.com/jcomperatore/PythonPourLaDataScience/blob/main/Datascrapping/Scraping%20Dataframe.ipynb)

 *⚠️ Si ce notebook est une constituante importante de notre raisonnement, il n'est au final absolument pas nécessaire pour le bon focntionnement de notre projet. Nous le laissons ici pour présenter nos étapes de reflexion. Il est réutilisé avec quelques transformations dans le notebook [`Creation Datacleaned`](https://github.com/jcomperatore/PythonPourLaDataScience/blob/main/Datascrapping/Creation%20Datacleaned.ipynb) qui est lui essentiel.*

### Nettoyage des données

Une fois toutes ces données récupérées, il est nécessaire de les traiter pour pouvoir les exploiter. En effet, on s'aperçoit assez vite que les textes sont trop pollués. Si l'on regarde par exemple quels sont les 30 mots ou expressions qui reviennent le plus, on obtient ce résultat : 

<div align =  "center">
<img src = 'img\Mots sans clean.png' width = 70%>
</div>

On voit bien qu'il faut enlever toutes les expressions dénuées de sens.
On va également profiter de cela pour lemmatiser toutes les expressions, afin de ne plus tenir compte des conjugaisons ou des accords lors du comptage des mots. Tout cela est réalisé dans le notebook [`Creation Datacleaned`](https://github.com/jcomperatore/PythonPourLaDataScience/blob/main/Datascrapping/Creation%20Datacleaned.ipynb)

Une fois ce nettoyage fait, on peut alors stocker toutes les données dans un fichier au format csv, [`data_cleaned`](https://github.com/jcomperatore/PythonPourLaDataScience/blob/main/Datascrapping/data_cleaned.csv). Cela évite de réitérer à chaque exécution tout le scrapping et le pré-processing, excessivement longs. 


## 2) Première étude descriptive

Une fois que ces données ont été récupérées, on peut commencer à déjà s'y intéresser au moyen de [statistiques descriptives](https://github.com/jcomperatore/PythonPourLaDataScience/blob/main/Statistiques%20descriptives/Statistiques_descriptives.ipynb). Le premier réflexe que nous avons eu est de réaliser une représentation graphique des mots obtenus : 

<div align =  "center">
<img src = 'img\representation mots.png' width = 70%>
</div>

Si le manque de 's' à `françai` peut d'abord nous choquer (probablement dû à la lemmaization), on peut ensuite remarquer que des mots thématiques se dégagent : `numérique`, `souveraineté industrielle`, `santé prévention` ou encore `transition écologique` occupent une place conséquente sur l'écran.

Le deuxième travail effectué se voulait d'afficher les groupes qui utilisent le plus régulièrement certaines expressions. Il est assez naturellement venu le besoin de les normaliser par rapport au nombre de questions posées par les groupes.

<div align =  "center">
<img src = 'img\ecologie.png' width = 49%>
<img src = 'img\question par groupe.png' width = 49%>
</div>

<div align =  "center">
<img src = 'img\ecologie normalisé.png'>
</div>

En effet, on peut voir avec cet exemple de l'écologie que c'est le RN qui pose le plus de questions qui concernent ce sujet. Cependant, par rapport au nombre de questions posées, le parti écologiste reprend logiquement sa première place, puisqu'il s'agit de son thème de prédilection. 


Enfin, on a également pu s'intéresser a des représentations géographiques de ces statistiques, qui peuvent donner des résultats assez attendus : 
<div align =  "center">
<img src = 'img\image.png'>
</div>

On observe assez logiquement que les députés issus de la diagonale du vide sont plus investis au sujet de la ruralité que les parisiens par exemple.

## 3) Modélisation

Afin de pouvoir analyser plus en avant le corpus de textes recueilli dans la première partie de ce projet, nous avons cherché à le traiter à l'aide de méthodes de NLP. L'idée à la source du travail que nous avons effectué dans cette partie est que les textes allaient, en première analyse, se regrouper plus par thématiques abordées que par groupes politiques ou orientation idéologique de leur auteur. Il nous semblait donc qu'une classification thématique des textes était un préalable indispensable à toute analyse du contenu politique. 

Nous avons donc dans cette partie défini des fonctions python permettant de vectoriser le corpus de texte, de regrouper les différents textes à l'aide d'algorithmes de clustering et d'effectuer des analyses en composantes principales afin de représenter graphiquement, sur un plan, nos corpus de textes. Afin de vectoriser les textes du corpus, nous avons utilisé une approche naïve dite "bag of words" consistant à compter l'apparition de chaque mot du vocabulaire (tous les mots apparaissant dans le corpus de textes) pour vectoriser les textes, sans prendre en compte les interactions entre différents mots.

Nous avons dans un premier temps appliqué ces fonctions à un corpus de textes très simple (six textes d'une phrase) pour les tester et illuster notre méthode. Le corpus de texte que nous avons écrit se divisait intuitivement en deux groupes de textes très similaires, et la fonction de clustering retrouvait bien ces deux groupes de textes, indiquant le bon fonctionnement de nos codes (avec l'ACP aussi, les points représentant des textes d'un même groupe se confondaient).

Ensuite, nous avons cheché à appliquer cette méthode au corpus de questions écrites au gouvernement. Cependant, il semble que la vectorisation effectuée ne permet pas de mettre en lumière les tendances politiques des questions de notre corpus ni même d'en trouver la thématique. En effet, la vectorisation avec l'approche "bag of words"que mous avons effectuée est trop naïve et l'analyse est polluée par la présence de mots qui ne n'indiquent ni une thématique particulière ni une tendance politique donnée et dont la répartition dans les textes peut être modélisée comme aléatoire. Afin de classifier les textes par thématiques et de faire une étude ultérieure sur les tendances des textes politiques, il semble nécessaire d'effectuer une vectorisation plus fine, avec des méthodes de "word embedding" par exemple.

## Conclusion

Ce projet nous a permis de découvrir et de nous familiariser avec les méthodes de NLP et leurs applications au traitement du discours politique. Les méthodes que nous avons commencé à mettre en œuvre dans ce projet sont des fondations qui pourraient être développées et améliorées et être utilisées dans le cadre de recherches en sciences politiques dans la même veine que de nombreuses recherches contemporaines en sciences politiques et en sciences sociales. 

Une première application de telles méthodes pourrait être d’obtenir, à l’aide d’analyse en composantes principales, une cartographie objective des proximités politiques (ou tout du moins du discours) entre différents partis et groupes politiques. En outre, on pourrait dévoiler les proximités entre les différents partis politiques selon la thématique abordée.

Par ailleurs, ces méthodes appliquées sur des corpus de textes politiques de différentes périodes pourraient permettre de dévoiler ou d’objectiver des évolutions du discours politique (extrême droitisation du champ politique, accroissement de la préoccupation écologique, évolution d’un discours contestataire vers un discours plus institutionnel ou inversement, etc…).

