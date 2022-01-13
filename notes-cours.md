# Requete geospatial

Elles utilisent les types de données géométriques spécialisées (point, line, multiline, polygon...)
Elles expriment des relations entre les types de données géométriques, tels que distance, equals, touches, overlaps, disjoint etc…

À l'aide des requêtes géospatiales on peut exécuter les opérations comme:
Trouver la distance entre deux points.
Vérifier si une zone (polygone) en contient une autre.
Vérifier si une ligne croise ou touche une autre ligne ou un autre polygone.

GeoJSON est un format ouvert d’échange de données géospatiales utilisant la norme JSON représentant des entités géographiques simples et leurs attributs non spatiaux. https://docs.mongodb.com/manual/reference/geojson/

# Aggrégation

Les requêtes d’agrégation permettent de regrouper, manipuler ou associer des données.

documentation: https://docs.mongodb.com/manual/aggregation/

Première requette d'agréagation:
![image](https://user-images.githubusercontent.com/49844846/148966306-171e31cd-fe08-4203-a34b-a8caae367ad2.png)

# Index

Restocque une partie des données en fonction d'un champ selon un tri. Ce qui permet de scanner les collection et acceder à une donnée plus rapidement.

# Vues

Une vue est une table virtuelle qui n'existe pas réellement. Elle constitue souevnt des requettes complexes.
Elle n'ont pas d'impacte sur les données, Ce sont des collections en lecture seule.
On ne peut pas rennommer de vue, il faut la detruire. Il est possible d'utiliser des indexes dans une vue.
Toutes les données dans une vue sont publiques.

`db.createView('nomDeLaVue', 'restaurants', [{$project: {"": 0}}])`

`db.getCollectionInfos({name:"restaurants})`

Appeler une vue:
`db."nomDeLaVue.find()`
