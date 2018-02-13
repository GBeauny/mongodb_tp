# mongodb_tp

# Manipulation de la base

Gestion de la collection (Documents)

- Créer une base du nom : *dblp*
- Créer une collection : *publis*
- Créer le document suivant :

```json
{
  "type": "Book",
  "title": "Modern Database Systems: The Object Model, Interoperability, and Beyond.",
  "year": 1995,
  "publisher": "ACM Press and Addison-Wesley",
  "authors": ["Won Kim"],
  "source": "DBLP"
}
```

- Insérer le document dans la collection publis
- Créer et insérer deux autres publications à partir de la page de conférence suivante :
> http://www.informatik.uni-trier.de/~ley/db/journals/vldb/vldb23.html
- Consulter le contenu de la collection
- Maintenant importer les données (fichier json) qui se trouve dans le dossier `data`
- Dans la console `mongo` vérifier que les données ont bien été insérés ou bien avec un IDE (Robo 3T par exemple)

Désormais exprimez les requêtes suivantes :

- Liste de tous les livres (type “Book”) ;
- Liste des publications depuis 2011 ;
- Liste des livres depuis 2014 ;
- Liste des publications de l’auteur “Toru Ishida” ;
- Liste de tous les éditeurs (type “publisher”), distincts ;
- Liste de tous les auteurs distincts ;
- Trier les publications de “Toru Ishida” par titre de livre et par page de début ;
- Projeter le résultat sur le titre de la publication, et les pages ;
- Compter le nombre de ses publications ;
- Compter le nombre de publications depuis 2011 et par type ;
- Compter le nombre de publications par auteur et trier le résultat par ordre croissant

# Indexation

- Pour chaque requête de type `find()`, regarder le plan d’exécution généré avec `.explain()` à la fin de la requête 
- Créer un index sur l’attribut année `db.publis.createIndex( { year :1 } );` 
- Refaire les requêtes `find()` sur l’année en regardant le plan d’exécution généré

> Attention
> Il est également possible d’avoir le plan d’exécution sur les requêtes de type Map/Reduce (option $explain dans queryParam, voir plus bas).

# Pratique de Map / Reduce

Pour exprimer une requête MapReduce, il faut définir une fonction de map, une fonction de reduce, un filtre (optionnel), lancer le tout avec l’opérateur mapReduce et consulter le résultat (optionnel!). Soit :

| map | var mapFunction = function () {emit(this.year, 1);}; |
|--|--|
| reduce | var reduceFunction = function (key, values) {return Array.sum(values);}; |
|filtre|var queryParam = {query : {}, out : "result_set"}|
|requête|db.publis.mapReduce(mapFunction, reduceFunction, queryParam);|
|résultat|db.result_set.find();|

# Mappez et réducez

Pour les recherches suivantes, donnez la requête MapReduce sur la base en changeant la requête Map et/ou Reduce

- Pour chaque document de type livre, émettre le document avec pour clé “title”
- Pour chacun de ses livres, donner le nombre de ses auteurs
- Pour chaque document ayant “booktitle” (chapitre) publié par Springer, donner le nombre de ses chapitres.

> Attention
> La fonction de reduce n’est évaluée que lorsqu’il y a au moins 2 documents pour une même clé. Il est donc nécessaire d’appliquer un filtre après génération du résultat.

- Pour chaque éditeur “Springer”, donner le nombre de publication par année
- Pour chaque clé “publisher & année” (pour ceux qui ont un publisher), donner le nombre de publications

> Important
> La clé du emit() doit être un document.

- Pour l’auteur “Toru Ishida”, donner le nombre de publication par année
- Pour l’auteur “Toru Ishida”, donner le nombre moyen de pages pour ses articles (type Article)
- Pour chaque auteur, donner le titre de ses publications

> Attention
> La sortie du map et du reduce doit être un document (pas un tableau)

- Pour chaque auteur, donner le nombre de publications associé à chaque année
- Pour l’éditeur “Springer”, donner le nombre d’auteurs par année
- Compter les publications de plus de 3 auteurs
- Donner pour chaque publieur, donner le nombre moyen de pages par publication
- Pour chaque auteur, donner le minimum et le maximum des années, ainsi que le nombre de publication totale

# Mise à jours

- Modification : `db.media.update ({"Title" : "Database"}, {$set:{Genre : "Science"}});`

> Note
> Premier JSon : Mapping, Second JSon : Update ($set, $unset)

- Suppression : db.media.remove({"Title" : "Database"})

- Fonction itérative :

```javascript
db.publis.find().forEach(
        function(pub){
        pub.pp = pub.pages;
        db.publis.save(pub);
});
```

Pour les mises à jour suivantes, vérifier le contenu des données avant et après la mise à jour.

- Mettre à jour tous les livres contenant “database” en ajoutant l’attribut “Genre” : “Database”
- Supprimer le champ “number” de tous articles
- Supprimer tous les articles n’ayant aucun auteur
- Modifier toutes les publications ayant des pages pour ajouter le champ “pp” avec pour valeur le motif suivant : `pages.start--pages.end`

