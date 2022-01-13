# Création de la DB

## Invitation des autres membres de l’équipe via leur adresse email
![image](https://user-images.githubusercontent.com/49844846/148928790-9a930f34-0b69-4047-989e-1e383f81ade9.png)

## Création de la base de données
![image](https://user-images.githubusercontent.com/49844846/148929098-2e538aa6-8400-478b-82ee-67176935d1ae.png)

## Ajout d’un utilisateur
![image](https://user-images.githubusercontent.com/49844846/148929145-dd350431-d908-46cb-8f56-ec15858bb7dd.png)

```
Identifiant: root
Mot de passe: root
```

## Whiteliste des adresses IP des membres du projet
![image](https://user-images.githubusercontent.com/49844846/148929349-e709fc45-d7a8-4d0d-a89c-5a92ab8128a7.png)
![image](https://user-images.githubusercontent.com/49844846/148929366-5b9e4a6b-9091-40a4-8947-9ffcc155af06.png)

## Tentative de connexion avec MangoDB Shell
(Finalement je suis passé sur Compass)

![image](https://user-images.githubusercontent.com/49844846/148929445-1e6eead2-cba8-4200-961c-6b37bef6cb85.png)
![image](https://user-images.githubusercontent.com/49844846/148929456-24a74ab3-9618-45a8-8bad-51380051908c.png)

# Questionnaire initiation aux requettes

# Requête géospatiale

Elles utilisent les types de données géométriques spécialisées (point, line, multiline, polygon...)
Elles expriment des relations entre les types de données géométriques, tels que distance, equals, touches, overlaps, disjoint etc…

À l'aide des requêtes géospatiales on peut exécuter les opérations comme:
Trouver la distance entre deux points.
Vérifier si une zone (polygone) en contient une autre.
Vérifier si une ligne croise ou touche une autre ligne ou un autre polygone.

GeoJSON est un format ouvert d’échange de données géospatiales utilisant la norme JSON représentant des entités géographiques simples et leurs attributs non spatiaux. https://docs.mongodb.com/manual/reference/geojson/

L’onglet schema de MongoDBCompass nous permet de visualiser des des données géographiques :
![image](https://user-images.githubusercontent.com/49844846/148931334-a82589c4-42da-4757-971a-0f1830a0340e.png)

Nous aimerions utiliser des géodata pour visualiser la position géographique d’une liste d’utilisateurs sur une carte.

Nous avons importé une collection d’utilisateurs mockés, chaque objet utilisateur à une adresse contenant des coordonnés GPS (longitude et lagitude).

Compass n’arrivait pas à interpréter les données qui avait sous forme de carte :

![image](https://user-images.githubusercontent.com/49844846/148931399-2384e162-4f8e-4f56-bedf-9797b0142426.png)

J'ai donc créer mon propre graphique sur Charts :

![image](https://user-images.githubusercontent.com/49844846/148931483-affff60b-bef1-468f-8f33-a9e060a4282a.png)
![image](https://user-images.githubusercontent.com/49844846/148931503-10d688dd-f3b7-409a-888c-ef31a5568988.png)

Il est plus simple de comprendre nos données de cette facon qu'n lisant 2 gros chiffres à virgule.
Il est possible d'étudider cela pour prendre des décisions commeciales ou marketing.

Dans l'exemple de notre restaurant, visualiser la position de nos restaurants et de nos clients peut nous permettre de créer des enseignes plus proches de nos clients. Localiser précisément nos clients nous permet aussi de se faire une idée de qui est notre clientelle. (Age, classe sociale, langue parlée...)

// TODO: faire une requette Geo

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


# Base en commun:
Requettes TODO:

### Informations sur nos clients
![image](https://user-images.githubusercontent.com/49844846/149315473-b7555e69-06a8-41fc-96e0-292d6f2140df.png)
Utilisation de MongoDB sur VS Code

```
use('Restaurants');

db.clients.aggregate([
    {
        $group: {
            _id: "$gender",
            agerageAge: {$avg: "$age"}
        }
    }
])
```
Dans cette requette, je groupe les cmlients par genre, puis je fais une moyenne d'age par genre.

```
db.clients.aggregate([
    {
        $group: {
            _id: null,
            agerageAge: {$avg: "$age"}
        }
    }
])
```
Maintenant, en passant `null` à `_id` j'ai la moyenne d'age de tout mes clients

Liste de emails pour les compagnes d'emailing:
```
db.clients.find({}, { email: 1 })
```

Distance entre les clients et le resaurant
  Créer des restaurants plus proche des clients
  
### Nombre de visites par client:
```
db.clients.aggregate({
   $lookup:
    {
        from: "visits",
        localField: "id",
        foreignField: "visitor_id",
        as: "visits"
    }
})
```
Cette requette nous permet de savoir quand et quel client est venu dans notre restaurant.

Cela pourrait permettre de:
- Relancer les clients qui ne sont jamais revenus consommer chez nous.
- Demander un avis sur leur experience chez nous par email.
- Offrir des promotions à nos clients les plus fidèles.

### Influence par horaires
Cette requette nous permet de connaître 
- Augmenter le nombre d'employers aux horaires de forte influence.
- Mettre en place des tarifs differents à certains horaires (Happy Hour par exemple).
  

