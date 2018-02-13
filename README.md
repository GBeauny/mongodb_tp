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

