# Projet Python pour la Data Science

*Ce projet est réalisé dans le cadre du cours de Python pour la Data Science de Lino Galiana, 2023-2024* 

### Objectif et méthodologie

L'objectif de ce dépot est d'essayer de prédire l'orientation politique d'un texte. Nous voulons donc réaliser un algorithme NLP pour, apres un apprentissage sur un corpus de textes orientés, prédire l'orientation politique de l'auteur inconnu d'un texte.
Le projet est donc découpé en trois parties : 
  1) Récupération des données
  2) Premiere étude descriptive
  3) Modélisation


## 1) Récupération des données

### Récupération de données brutes

Les textes dont nous avions besoin devaient être clairement attribuables à une opinion politique. Pour cela, les discours des députés ou les programmes de campagnes des candidats semblaient être des candidats crédibles. Cependant, les programmes des candidats pouvaient représenter un peu maigre, et être plus compliqués à récuperer. 
D'autre part, les questions au gouvernement posées par les députés présentaient plusisuers avantages : nombreuses, variées, et simples à récupérer.

En efffet, elles sont accessibles pour un utilisateur à partir d'un outil de recherche [disponible ici](https://www2.assemblee-nationale.fr/recherche/questions).

En y regardant de plus près, on constate que toutes les questions concernant la XVIème legislature sont disponibles à des adresses du type [https://questions.assemblee-nationale.fr/q16/16-XXXXXQE.htm](https://questions.assemblee-nationale.fr/q16/16-8987QE.htm) où XXXX est le numéro de la question. 

Pour toutes les récupérer, nous avons donc mis en place un algorithme de Scraping qui boucle sur tous les numéros de pages, afin d'obtenir toutes les questions. Cet algorithme est disponible sous sa forme naïve dans le notebook [`Scraping Dataframe`](https://github.com/jcomperatore/PythonPourLaDataScience/blob/main/Datascrapping/Scraping%20Dataframe.ipynb)

 *⚠️Si ce notebook est une constituante importante de notre raisonnement, il n'est au final absolument pas nécessaire pour le bon focntionnement de notre projet. Nous le laissons ici pour présenter nos étapes de reflexion. Il est réutilisé avec quelques transformations dans le notebok [`Creation Datacleaned`](https://github.com/jcomperatore/PythonPourLaDataScience/blob/main/Datascrapping/Creation%20Datacleaned.ipynb) qui est lui essentiel.*

### Nettoyage des données

Une fois toutes ces données récupérées, il est nécessaire de les traiter pour pouvoir les exploiter par la suite. En effet, on s'aperçoit assez vite que les textes sont trop pollués. Si l'on regarde quelles sont les 30 mots ou expressions qui reviennent le plus, on obtient ce résultat : 

<div align =  "center">
<img src = 'img\Mots sans clean.png' width = 70%>
</div>

On voit bien qu'il faut enlever toutes les expressions dénuées de sens.
On va également profiter de cela pour lemmatiser toutes les expressions, afin de ne plus tenir compte des conjugaisons ou des accords lors du comptage des mots. Tout cela est réalisé dans le notebook [`Creation Datacleaned`](https://github.com/jcomperatore/PythonPourLaDataScience/blob/main/Datascrapping/Creation%20Datacleaned.ipynb)

Une fois ce nettoyage fait, on peut alors stocker toutes les données dans un fichier au format csv, [`data_cleaned`](https://github.com/jcomperatore/PythonPourLaDataScience/blob/main/Datascrapping/data_cleaned.csv).


## 2) Première étude descriptive

## 3) Modélisation 

## Conclusion

Ce projet nous a permis de découvrir et de nous familiariser avec les méthodes de NLP et leurs applications au traitement du discours politique. Les méthodes que nous avons commencé à mettre en œuvre dans ce projet sont des fondations qui pourraient être développées et améliorées et être utilisées dans le cadre de recherches en sciences politiques dans la même veine que de nombreuses recherches contemporaines en sciences politiques et en sciences sociales. 
Une première application de telles méthodes pourrait être d’obtenir, à l’aide d’analyse en composantes principales, une cartographie objective des proximités politiques (ou tout du moins du discours) entre différents partis et groupes politiques. En outre, on pourrait dévoiler les proximités entre les différents partis politiques selon la thématique abordée.
Par ailleurs, ces méthodes appliquées sur des corpus de textes politiques de différentes périodes pourraient permettre de dévoiler ou d’objectiver des évolutions du discours politique (extrême droitisation du champ politique, accroissement de la préoccupation écologique, évolution d’un discours contestataire vers un discours plus institutionnel ou inversement, etc…).

