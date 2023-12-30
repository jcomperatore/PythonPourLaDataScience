# Projet Python pour la Data Science

*Ce projet est réalisé dans le cadre du cours de Python pour la Data Science de Lino Galiana, 2023-2024* 

### Objectif et méthodologie

L'objectif de ce dépot est d'essayer de prédire l'orientation politique d'un texte. Nous voulons donc réaliser un algorithme NLP pour, apres un apprentissage sur un corpus de textes orientés, prédire l'orientation politique de l'auteur inconnu d'un texte.
Le projet est donc découpé en trois parties : 
  1) Récupération des données
  2) Premiere étude descriptive des données
  3) Modélisation


## 1) Récupération des données

### Récupération de données brutes

Les textes dont nous avions besoin devaient être clairement attribuables à une opinion politique. Pour cela, les discours des députés ou les programmes de campagnes des candidats semblaient être des candidats crédibles. Cependant, les programmes des candidats pouvaient représenter un peu maigre, et être plus compliqués à récuperer. 
D'autre part, les questions au gouvernement posées par les députés présentaient plusisuers avantages : nombreuses, variées, et simples à récupérer.

En efffet, elles sont accessibles pour un utilisateur à partir d'un outil de recherche [disponible ici](https://www2.assemblee-nationale.fr/recherche/questions).

En y regardant de plus près, on constate que toutes les questions concernant la XVIème legislature sont disponibles à des adresses du type [https://questions.assemblee-nationale.fr/q16/16-XXXXXQE.htm] où XXXX est le numéro de la question. 
