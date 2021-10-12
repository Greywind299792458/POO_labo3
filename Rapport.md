# Rapport labo 3 POO - Damien Maier, Elliot Ganty

## Choix et hypothèses de travail
### Cours
Il est écrit dans le cachier des charges qu'un élève "participe à des cours (au moins un)". Plus loin il est écrit que "les élèves peuvent s'inscrire à des cours optionnels (minimum 2)".

Nous avons pris comme hypothèse que le cahier des charges sous entend qu'il existe en fait deux types de cours : les cours "normaux" (chaque élève participe à au moins un cours normal) et les cours optionnels (chaque élève est inscrit à au moins deux cours optionnels).

Il est encore écrit dans le cahier des charges "Les cours sont donnés par des professeurs. Les cours peuvent être donnés à des élèves de différentes maisons mais d'une même année. Les cours ont un nom." Nous avons pris comme hypothèse que ces règles s'appliquaient à tous les cours, c'est à dire aux cours normaux et aux cours optionnels.

### Les maisons sont des instances de Maison
Lors de l'utilisation de l'application, il y aura une instance de la classe Maison pour chacune des quatre maisons Gryffondor, Poufsouffle, Serdaigle et Serpentard. Comme notre schéma UML est un diagramme de classes, les noms Gryffondor, Poufsouffle, Serdaigle et Serpentard n'apparaissent pas dans le diagramme.

### Personnalité des élèves

Le cahier des charges demande que les élèves soient répartis dans les maisons "en fonction de leurs personnalités". Maison possède un attribut traitsDePersonnalitéAssociés de type String qui permet de représenter les traits de personnalité qui feront qu'un élève sera placé dans une maison.

### Maison ayant le plus de points

Le cahier des charges demande qu'il soit possible "d'obtenir la maison dans l'école qui a le plus de points". Pour cela nous avons prévu la méthode `maisonAyantLePlusDePoints()`, qui est une méthode statique de la classe Maison et qui renvoie une référence vers un objet de type Maison. Cette méthode devra lire le nombre de points de toutes les maisons et renvoyer une références vers la maison ayant le plus de points.

Pour accéder aux maisons, cette méthode utilisera l'attribut statique `maisons: Maison[]` de la classe Maison qui est un tableau contenant des références vers toutes les maisons. (Le constructeur d'une maison doit ajouter la maison à ce tableau et le destructeur doit supprimer la maison de ce tableau)

### Ajouter ou retirer des points d'une maison

Pour ajouter ou retirer des points à une maison, on appelle la méthode `ajouterOuRetirerPoints(in nbPoints:int): void` de cette maison avec comme argument le nombre de points à ajouter ou retirer (si l'argument est un nombre positif il faut ajouter des points, si c'est un nombre négatif il faut en retirer).

Les professeurs ont une méthode `ajouterOuRetirerPointsMaison(in nbPoints:int, in maison:Maison): void` qui prend en paramètre le nombre de points à ajouter ou retirer (selon si le nombre est positif ou négatif) et la maison concernée. Cette méthode va simplement appeler la méthode `ajouterOuRetirerPoints(in nbPoints:int): void` de la maison indiquée.


### Équipes de Quidditch
Initialement, nous avons voulu utiliser une classe ÉquipeDeQuidditch, qui aurait des associations avec les classes Maison, Élève et MatchDeQuidditch. Nous nous sommes rendus comptes que, étant donné que chaque maison possède exactement une équipe de Quidditch, l'ajout de cette classe apporte de la complexité inutile.

Les informations qui concernent les équipes de Quidditch sont donc représentées dans notre schéma directement avec la classe Maison. L'assocation "appartient à l'équipe de quidditch de" entre Élève et Maison permet de représenter les membres de l'équipe de Quidditch d'une maison. Les associations entre MatchDeQuidditch et Maison permettent de représenter le fait que l'équipe de Quidditch d'une maison a participé à ou a gagné un match de quidditch.

### Gagnant d'un match de Quidditch

Nous avons pris comme hypothèse qu'un match de quidditch peut exister avant que le gagnant de ce match ne soit connu. Par exemple, on peut imaginer qu'on aimerait pouvoir créer un match de quidditch dans l'application dès le moment où ce match est planifié.

Cela a comme conséquence que l'association "a gagné" entre Maison et MatchDeQuidditch a une cardinalité 0..1 du côté de Maison.