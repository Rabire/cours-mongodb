# Projet:

## Présentation de notre travail

Je suis un data analyse membre d'une équipe IT qui avons étés recrutés par une chaine de restaurant.

Sur ce projet la chaine de fastfood `Tacos Story` met à disposition des clients des bornes pour passer leurs commandes. Ces bornes demandent au client de renseigner ses informations pour finaliser la commande.

Son besoin est le suivant:
Recevoir une analyse de données afin de connaître ses forces et ses faiblesses. Notre but final de mettre à disposition des outils pour renforcer notre force commerciale.

La chaine de restaurant compte 10 restaurants franchisés dans le monde.
Sur l'année 2021, ces restaurants ont réaliser 1000 de 200 clients différents.

# Annalyse proposée par Rabire

### Annalyse géographique

L’onglet schéma de MongoDBCompass nous permet de visualiser des données géographiques :
![image](https://user-images.githubusercontent.com/49844846/148931334-a82589c4-42da-4757-971a-0f1830a0340e.png)

Nous utilisons des géodata pour visualiser la position géographique d’une liste de personnes sur une carte car nous connaissons leur position géographique (longitude et lagitude) grace à leur adresse.

Compass n’arrivait pas à interpréter les données qui avaient sous forme de carte :
![image](https://user-images.githubusercontent.com/49844846/148931399-2384e162-4f8e-4f56-bedf-9797b0142426.png)

J'ai donc créer mon propre graphique sur Charts :

![image](https://user-images.githubusercontent.com/49844846/148931483-affff60b-bef1-468f-8f33-a9e060a4282a.png)
![image](https://user-images.githubusercontent.com/49844846/148931503-10d688dd-f3b7-409a-888c-ef31a5568988.png)

Il est plus simple de comprendre nos données de cette façon qu'en lisant 2 gros chiffres à virgule.

```
db.restaurants.aggregate([
    { "$geoNear": {
        "near": {
            "type": "Point",
            "coordinates": [ -81.093699, 32.074673 ]
        },
        "maxDistance": 500 * 1609,
        "spherical": true,
        "distanceField": "distance",
        "distanceMultiplier": 0.000621371
    }}
]).pretty()
```

Requette permettant de calculer la distance depuis un point.

Dans l'exemple de nos restaurants, visualiser la position de nos restaurants et de nos clients peut nous permettre de créer des enseignes plus proches de nos clients.

Localiser précisément nos clients nous permet aussi de se faire une idée de qui est notre clientèle. (Age, classe sociale, langue parlée...) C'est justement ce que je fais dans la partie suivante.

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

Dans cette requête, je groupe les clients par genre, puis je fais une moyenne d'age par genre.

Nous avons fait cela car la chaine a prévu de mettre des jouets dans les menus enfants. Les jouets peuvent être unisexe ou different selon le sexe de l'enfant.

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

Maintenant, en passant `null` à `_id` j'ai la moyenne d'age de tous mes clients. C'est la première chaine de fastfood qui met d'accord les jeunes et les moins jeunes !

Liste des emails:

```
db.clients.find({}, { email: 1 })
```

Cette requête nous permet d'extraire une liste d'emails pour mener des compagnes d'emailing. C'est une stratégie marketing courante.

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

Cette requête nous permet de savoir quand et quel client est venu dans notre restaurant.

Cela pourrait permettre de:

- Relancer les clients qui ne sont jamais revenus consommer chez nous.
- Demander un avis sur leur experience chez nous par email.
- Offrir des promotions à nos clients les plus fidèles.

### Influence par horaires

Cette requête nous permet de connaître

- Augmenter le nombre d'employers aux horaires de forte influence.
- Mettre en place des tarifs differents à certains horaires (Happy Hour par exemple).

```
db.visits.count({visit_time: {$regex: /^20/ }})
```

```
db.visits.count({visit_time: {$regex: /^12/ }})
```

Les 2 requêtes au dessus permettent de connaitre le bombre de visites entre 20h et 21h et le nombre de visites entre 12h et 13h
