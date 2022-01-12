# Création de la DB

## Invitation des autres membres de l’équipe via leur adresse email
![image](https://user-images.githubusercontent.com/49844846/148928790-9a930f34-0b69-4047-989e-1e383f81ade9.png)

## Création de la base de données
![image](https://user-images.githubusercontent.com/49844846/148929098-2e538aa6-8400-478b-82ee-67176935d1ae.png)
![image](https://user-images.githubusercontent.com/49844846/148929117-6adaa852-4181-48b7-b57e-e6b21e230cf6.png)

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

1. Ecrivez une requête MongoDB pour afficher tous les documents dans les restaurants de la collection
`{}`

2. Ecrivez une requête MongoDB pour afficher les champs restaurant_id, name, borough et cuisine pour tous les documents de la collection restaurant.
![image](https://user-images.githubusercontent.com/49844846/148758701-9c03ca71-e2a5-4e4b-bc7f-fc66e23ffecc.png)

3. Ecrivez une requête MongoDB pour afficher les champs restaurant_id, name, borough et cuisine, mais exclure le champ _id pour tous les documents de la collection restaurant. 
![image](![image](https://user-images.githubusercontent.com/49844846/148759425-0dfae8e0-906a-467e-95f8-f2251bcc9028.png))

4. Ecrivez une requête MongoDB pour afficher les champs restaurant_id, nom, arrondissement et code postal, mais excluez le champ _id pour tous les documents de la collection restaurant.
![image](https://user-images.githubusercontent.com/49844846/148759820-124214c4-ac47-4645-a086-15606b80be0a.png)

5. Ecrivez une requête MongoDB pour afficher tous les restaurants qui sont dans l'arrondissement du Bronx. 
![image](https://user-images.githubusercontent.com/49844846/148758999-e5bfe4af-9cb4-44ea-9002-487c0cdfa25d.png)

6. Ecrivez une requête MongoDB pour afficher les 5 premiers restaurants qui se trouvent dans le quartier du Bronx. Aller à l'éditeur
![image](https://user-images.githubusercontent.com/49844846/148759942-27b19940-84ee-45fb-ad3a-fb14499c005f.png)

7. Ecrivez une requête MongoDB pour afficher les 5 restaurants suivants après avoir sauté les 5 premiers qui sont dans le quartier du Bronx.
![image](https://user-images.githubusercontent.com/49844846/148760043-934e4fbd-d096-4336-8660-a9211717ee4a.png)

8. Ecrivez une requête MongoDB pour trouver les restaurants qui ont obtenu un score supérieur à 90. 
![image](https://user-images.githubusercontent.com/49844846/148761557-726f3224-7dbf-4a7b-9c3c-32f45a52fda8.png)

9. Ecrivez une requête MongoDB pour trouver les restaurants qui ont obtenu un score supérieur à 80 mais inférieur à 100. 
![image](https://user-images.githubusercontent.com/49844846/148930822-7bc906b6-3295-4d2a-9ce6-da0ae8b41020.png)

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

# Aggrégation

Les requêtes d’agrégation permettent de regrouper, manipuler ou associer des données.

documentation: https://docs.mongodb.com/manual/aggregation/

Première requette d'agréagation:
![image](https://user-images.githubusercontent.com/49844846/148966306-171e31cd-fe08-4203-a34b-a8caae367ad2.png)

# Index
  def TODO F10
  TODO: Comment un index peut ralentir une requete ?

# Vues

Une vue est une table virtuelle qui n'existe pas réellement. Elle constitue souevnt des requettes complexes.
Elle n'ont pas d'impacte sur les données, Ce sont des collections en lecture seule.
On ne peut pas rennommer de vue, il faut la detruire. Il est possible d'utiliser des indexes dans uen vue.

`db.createView('nomDelaVue', 'source: collection ou autre vue')`


# Base en commun:
Requettes TODO:

Liste de clients
  Moyenne d'age des clients
  Liste de emails pour les compagnes d'emailing
Distance moyenne des clients à chaque resaurants
  Créer des restaurants plus proche des clients
Nombre de passage par client par restaurant
  Relancer les clients qui ne sont jamais revenus
  Demander un avis sur leur experience
  Offrir des promotions aux clients les plus fidèles
Influence par horaires
  Augmenter le nombre d'employers aux horaires de forte influence
  










