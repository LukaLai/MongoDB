Base de données de documents  
Au format Json sans structure prédéfinie  
Schema  
Document est un ensemble de donnés cle-valeur = row  
En mongo on peut stocker ilimite dans la Collection est un grp de doc = table  
Mongo est un système de bdd crossplateform  
Possibilite de tableau mais bcp d’info dupliqué  
Field = colonne  
Jointure = documents imbriqués  
Avantage : structure simple et claire en objet  
Fait pour la monter en charge  
Plus besoin d’orm , stockage sur disque 


### L'indexation simple :  

``` javascript
db.collection.createIndex(<champ_et_type>, <options>)
```
#### Exemple :
``` javascript
db.personnes.createIndex({"age":-1})
```
Pour consulter les indexes d'un collection :
```javascript
db.collection.getIndexes()
```
Pour supprimer un index :
```javascript
db.collection.dropIndex(‘age_-1 ‘ )
//Création de l'index supp avec un nom
db.collection.createIndex({age:-1},{name: “unsupernom”})
```

### Les tableaux : 
Ajouter dans le tableau :
```javascript
{$push: {<champs>: <Valeur>,...}}
```
L’opérateur $push permet d’ajouter une ou plusieurs valeurs au sein d’un tableau.  
#### Exemple: Ajout d'une passion

```javascript
db.hobbies.updateOne({"_id":1}, {$push:{"passion":"roller"}})
```
Il est possible d’ajouter plusieurs valeurs égales /il n’y a pas de verif de doublons.  
```javascript
db.hobbies.updateOne({"_id":2},{$push:{"passion":{$each:["Minecraft","Rise"]}}})
```
Remplacer $push par $addToSet pour éviter les doublons.  

## Exercices :

Créez une base de données sample nommée "sample_db" et une collection appelée "employees". Insérez les documents suivants dans la collection "employees":  
{ name: "John Doe", age: 35, job: "Manager", salary: 80000 }  
{ name: "Jane Doe", age: 32, job: "Developer", salary: 75000 }  
{ name: "Jim Smith", age: 40, job: "Manager", salary: 85000 }    

```javascript
//Création de la bdd
use sample_db

//Création de la collection
db.createCollection("employees")

//Ajout des documents dans la collection "employees"
db.employees.insert(
    { name: "John Doe", age: 35, job: "Manager", salary: 80000 },
    { name: "Jane Doe", age: 32, job: "Developer", salary: 75000 },
    { name: "Jim Smith", age: 40, job: "Manager", salary: 85000 })
```

## ***Exobook.md***  

Écrivez une requête MongoDB pour trouver tous les documents dans la collection "employees".  
### Commande :
![Resultat](../Mongo/Img/Image1.png)

Écrivez une requête pour trouver tous les documents où l'âge est supérieur à 33. 
### Commande :
![Resultat](../Mongo/Img/Image2.png)

Écrivez une requête pour trier les documents dans la collection "employees" par
salaire décroissant.

### Commande :
![Resultat](../Mongo/Img/Image3.png)

Écrivez une requête pour sélectionner uniquement le nom et le job de chaque document.

### Commande :
![Resultat](../Mongo/Img/Image4.png)

Écrivez une requête pour compter le nombre d'employés par poste.

### Commande :
![Resultat](../Mongo/Img/Image5.png)

Écrivez une requête pour mettre à jour le salaire de tous les développeurs à 80000.

### Commande :
![Resultat](../Mongo/Img/Image6.png)

## ***Exo.md***

Exercice 1

Affichez l’identifiant et le nom des salles qui sont des SMAC.

### Commande :
![Resultat](../Mongo/Img/Image7.png)

Exercice 2

Affichez le nom des salles qui possèdent une capacité d’accueil strictement supérieure à 1000 places.

### Commande :
![Resultat](../Mongo/Img/Image8.png)

Exercice 3

Affichez l’identifiant des salles pour lesquelles le champ adresse ne comporte pas de numéro.

### Commande :
![Resultat](../Mongo/Img/Image9.png)

Exercice 4

Affichez l’identifiant puis le nom des salles qui ont exactement un avis.

### Commande :
![Resultat](../Mongo/Img/Image10.png)

Exercice 5

Affichez tous les styles musicaux des salles qui programment notamment du blues.

### Commande :
![Resultat](../Mongo/Img/Image11.png)

Exercice 6

Affichez tous les styles musicaux des salles qui ont le style « blues » en première position dans leur tableau styles.

### Commande :
![Resultat](../Mongo/Img/Image12.png)

Exercice 7

Affichez la ville des salles dont le code postal commence par 84 et qui ont une capacité strictement inférieure à 500 places (pensez à utiliser une expression régulière).

### Commande :
![Resultat](../Mongo/Img/Image13.png)

Exercice 8

Affichez l’identifiant pour les salles dont l’identifiant est pair ou le champ avis est absent.

### Commande :
![Resultat](../Mongo/Img/Image22.png)

Exercice 9

Affichez le nom des salles dont au moins un des avis comporte une note comprise entre 8 et 10 (tous deux inclus).

### Commande :
![Resultat](../Mongo/Img/Image14.png)

Exercice 10

Affichez le nom des salles dont au moins un des avis comporte une date postérieure au 15/11/2019 (pensez à utiliser le type JavaScript Date).

### Commande :
![Resultat](../Mongo/Img/Image15.png)

Exercice 11

Affichez le nom ainsi que la capacité des salles dont le produit de la valeur de l’identifiant par 100 est strictement supérieur à la capacité.
```javascript
db.salles.find({"_id":{"$gte":[{"$multiply":["$_id",100]},"$capacite"]}},{"nom":1,"capacite":1})
```
Exercice 13

Affichez les différents codes postaux présents dans les documents de la collection salles.

### Commande :
![Resultat](../Mongo/Img/Image16.png)

Exercice 14

Mettez à jour tous les documents de la collection salles en rajoutant 100 personnes à leur capacité actuelle.

### Commande :
![Resultat](../Mongo/Img/Image17.png)

Exercice 15

Ajoutez le style « jazz » à toutes les salles qui n’en programment pas.

```javascript
db.salles.updateMany({"styles":{"$nin":["jazz"]}}{"$push":{"styles":"jazz"}})
```
Exercice 16

Retirez le style «funk» à toutes les salles dont l’identifiant n’est égal ni à 2, ni à 3.

### Commande :
![Resultat](../Mongo/Img/Image18.png)

Exercice 17

Ajoutez un tableau composé des styles «techno» et « reggae » à la salle dont l’identifiant est 3.

### Commande :
![Resultat](../Mongo/Img/Image19.png)

Exercice 19

Pour les salles dont le nom commence par une voyelle (peu importe la casse, là aussi), rajoutez dans le tableau avis un document composé du champ date valant la date courante et du champ note valant 10 (double ou entier). L’expression régulière pour chercher une chaîne de caractères débutant par une voyelle suivie de n’importe quoi d’autre est [^aeiou]+$.

### Commande :
![Resultat](../Mongo/Img/Image20.png)


Exercice 20

En mode upsert, vous mettrez à jour tous les documents dont le nom commence par un z ou un Z en leur affectant comme nom « Pub Z », comme valeur du champ capacite 50 personnes (type entier et non décimal) et en positionnant le champ booléen smac à la valeur « false ».


### Commande :
![Resultat](../Mongo/Img/Image21.png)

## ***Exo Index.md***

Je propose deux index pour couvrir ces deux requêtes : sur le codePostal et sur la capacite.  
```javascript 
db.salles.createIndex({‘adresse.codePostal’:1, ‘capacite’ :1})

//Pour supprimer les index :
db.salles.getIndex()
db.salles.dropIndex(<nom index>)
```

## ***Exo Validation.md***

L'insertion ne marche pas il faut rajouter le codepostal en le mettant dans l'objet adresse.  


## ***Exo Meteo.md***

récupération d’un fichier csv pour les datas de la méteo sur Kaggle
Création de la collection avec la commande :

### Commande :
![Resultat](../Mongo/Img/Image23.png)

 

Ajout des datas dans la collection avec l’ui de compass :

### Commande :
![Resultat](../Mongo/Img/Image24.png)

Avec compass, je peux directement changer le type de valeur en Numbers et donc éviter que mes températures deviennent des string. 


Création de l’index avec la commande :

### Commande :
![Resultat](../Mongo/Img/Image25.png)
 
Liste les index avec getIndexes():

### Commande :
![Resultat](../Mongo/Img/Image26.png)
 

Récupère les stations qui ont une température de plus de 25° au cours de l’été.

### Commande :
![Resultat](../Mongo/Img/Image27.png)
(Utilisation de l’agregation)

Commande qui permet de trier les stations selon le % max d’humidité de plus grand au plus petit.
« HumidityHighPercent »

### Commande :
![Resultat](../Mongo/Img/Image28.png)
 
(Affichage du % et de l’id seulement)
La requête suivante permet d’avoir la moyenne de la température moyenne par mois. En ajoutant un sort, on pourrait avoir les mois dans l’ordre car actuellement ils sortent en fonction du premier résultat de chaque mois trouvé.

### Commande :
![Resultat](../Mongo/Img/Image29.png) 
![Resultat](../Mongo/Img/Image30.png)  
La requête suivante permet de trier comme précédemment pour chaque mois (de l’été) ($sort possible) , Avec la température maximum atteinte.

### Commande :
![Resultat](../Mongo/Img/Image31.png)
 
Pour exporter j’utilise l’ui de compass :

### Commande :
![Resultat](../Mongo/Img/Image32.png)