# ReadMe_Rails

+ [La différence entre un site statique et un site dynamique](https://github.com/BenCmjn/ReadMe_Rails#statique--dynamique)
+ [Le MVC](https://github.com/BenCmjn/ReadMe_Rails#mvc--model-view-controller)
+ [Les routes](https://github.com/BenCmjn/ReadMe_Rails#le-routeurs-et-les-routes)
+ [Les Bases de Données(BDD)](https://github.com/BenCmjn/ReadMe_Rails#les-bases-de-donn%C3%A9es-et-le-models)
+ [GET / POST](https://github.com/BenCmjn/ReadMe_Rails#get--post)
+ [Le concept de migration](https://github.com/BenCmjn/ReadMe_Rails#migration)
+ [Les bonus] VIEW  CRUD  FLOW  SAFE

## Statique ≠ Dynamique

Statique : Affichage de contenus sur une BDD (un gros dossier) en HTML CSS et c'est TOUT.
_Caisse à savons_


Dynamique : Affichage de contenus sur un BDD grace à pleins d'autres langages qui permettent d'afficher du contenu EN FONCTION des utilisateurs.
_Tesla_

## MVC : Model View Controller :steam_locomotive:

| Model	                           | View                                     | Controller                           |
| :------------------------------: |:----------------------------------------:| :-----------------------------------:|
| relié à la base de donnée (B.D.D)| c'est ce que l'utilisateur voit !        | c'est la tour de contrôle ! |
| Back-end                         | c'est Front-end                          | c'est l'articulation entre le le Model et le View |
| l'arrière boutique               | c'est le rayonnage en boutique           | c'est le transpalette qui achemine ce qui est stocké en arrière boutique pour le mettre en rayonnage pour l'utilisateur. |


** :rowboat: Tout se beau monde se retrouve dans le dossier App :rocket: **

En plus il y a (par ordre d'importance) :
- Config
- DB : la BDD
- Routes
- Asset : pour le JS, le CSS, et les IMG
- Test (pour tester si ça marche bien, t
- Bin
- Lib : les librairies externes
- Log : le journal de modifications (blog technique)
- Public :
- Helpers : on s'en sert pas souvent
- Tmp
- Rend

## Le Routeurs et les Routes :roller_coaster:

On est dans `Config/route.rb`
`rails routes` pour voir toutes les routes dans Ruby


#### Les routes c'est ce qui définit ce que l'utilisateur peut faire sur les chemins sur lesquels il se balade
Et c'est le routeur qui construit les routes, les chemins. Imagine une route qui se construit sous tes pas. Des rayonnages qui se remplissent au fur et à mesure que tu marche dans la boutique.
C'est le routeur qui appelle le controller (le transpalette) qui va appeller le modèle (le carton en BDD) pour ensuite afficher la data en view (le rayonnage).

Par exemple : L'utilisateur veut aller au rayon "Welcome" donc le routeur va dire `get 'welcome'` au controlleur pour qu'il lui renvoit l‘"index de welcome" `to: 'welcome#index'`  



## Les Bases de Données (et le Models) :factory:

#### Une BDD c'est un gros excel.
Où chaque cellule est une data. Cette data correspond forcément à une rangée et une colonne et est dans une feuille de l'excel.

#### Une BDD relationnelle c'est une sorte d‘excel en 3D.
**Imagine ça :** Une cellule ne se réfère pas qu'à une colonne et une rangée, mais peut t'envoyer vers une autre feuille de l'excel, avec une autre colonne et une autre rangée. C'est *un nœud*. 

#### Comment se retrouver dans la base de donnée ?
-> Dans le dossier db : il y a le fichier "Schema.rb"
-> Et faire un ptit `rails route` (`rails r` doit marcher je pense) pour retrouver sa route.

Modeliser une base de donnée :
…à compléter


## Migration

`rails db:migrate`

La migration ça sert à **modifier** la BDD. C'est à dire :
- Créer une table (une feuille excel)
- Modifier une table (ajout/suppr. de colonne, rangée, cellule)
- Faire du lien entre les tables.


## GET / POST

GET 

| Method        | Action                         | Code       |
| ------------: | -------------                  | -----      |
| GET           | Renvoie la data au user        |            |
| POST          | L'utilisateur crée la data     |`create`    |
| PUT           |                                |            |
| PATCH         |                                |`update` ?  |
| DELETE        |                                |`delete` ?  |


## bonus : CRUD = Create Read Update Destroy

C'est là qu'on va permettre d'**intéragir avec la BDD par l'interface**, et pas ~~en tapant une ligne de commande dans la console~~ !

## bonus : VIEW :gem:

c'est de l'html un peu spécial, dans le sens où les balise ressemblent à ça `<%= … =%>` ou ça `<% … %>` plutôt qu'à ça `< … >`
Tout ce qu'il y a dans une balise ERB : `<%= C'est du code Ruby ici =%>`
ERB = "Embedded RuBy" = Du Ruby dans de l'html.

Et en fait le ruby est **dans** l'html, genre :
`<h1> <%= @article.title =%> </h1> <p> <%= @article.text =%> </p>`

Différence entre `<%= … =%>` et `<% … %>` :

| Code      |`<%= … =%>`     | `<% … %>`      | link_to 'le texte du liens' |
| --------- | :--------:     | :-------------:| :-------------------------: |
| Action    | S'affichera    | S'affichera pas| Équivalent de `href` en html|
| Exemple   | @articles.title| .each do …     | préfix_path(prefix)


## bonus : Exemple d'un flow typique :

L'utilisateur veut aller sur l'article 1 (http://monsite.com/articles/1) :
1. L Routeur : `GET` -> `ressources :articles` (le chemin "articles/:id" va renvoyer à la méthode "show" du controller)
2. Le controller : il a une méthode "show" dans lequel il a
`@article = Article.find(params[:id])`
3. Le Modèle : va renvoyer la data en BDD
4. Le controller : va 'injecter' ça dans la view, où il y a du html et qui va afficher ça.
5. Le view a besoin de ses balises chelous pour réceptionner la data dans ses balises html, et renvoie tout l'HTML au controller
6.  Le controller donne le tout à l'utilisateur !
BOUM !

## bonus Safety First !

Faire attention quand on a des inputs, ne pas permettre à un petit malin de passer administrateur en faisant
Pour ça on fait une classe `private` dans le controller de notre input 


#### note pour plus tard (à réviser) :

- Voir les `Authenticity token` (pour la sécurité ?)
- `rails generates controller Welcome index`
- `ressources :articles`
- `Article**.find()**`

- `Unpermitted parameter: :name`

[![La vidéo youtube de Féfé](http://img.youtube.com/vi/deNytSPvAxA/0.jpg)](http://www.youtube.com/watch?v=deNytSPvAxA)

