# Prix des carburants à j-7
<img src="https://cdn.pixabay.com/photo/2013/08/23/22/07/gasoline-175122_1280.jpg">
<i>Source : <a href="https://cdn.pixabay.com/photo/2013/08/23/22/07/gasoline-175122_1280.jpg">Pixabay</a>, image libre de droits</i>
<br/>

## À propos
<p style='text-align: justify;'>En tant que détenteur du permis B ainsi que d'un véhicule à essence depuis plusieurs années, j'ai trouvé intéressant de m'orienter vers un jeu de données présentant le prix des différents types de carburants disponibles (à j-7) dans toutes les stations-services à l'échelle nationale. D'un point de vue général, ce jeu de données permet de comparer différentes stations-essences par leurs offres de carburants, et d'en déterminer les prix les plus compétitifs. J'ai trouvé ce jeu de données sur Opendatasoft, mais j'ai vu qu'il avait pour référence le site <a href="https://www.prix-carburants.gouv.fr/">https://www.prix-carburants.gouv.fr/</a>. Ce site, mis en place par le gouvernement, met donc à disposition de manière libre et gratuite toutes les données relatives au prix des carburants. Ainsi, on peut accéder aux jeux de données des années précédentes, avec une possibilité de remonter jusqu'à l'année 2007. Il est également important de noter que l'arrêté ministériel du 12 décembre 2006 rend obligatoire la déclaration des prix pratiqués pour tout gérant de point de vente de carburants ayant vendu au moins 500 mètres cube des carburants SP95, SP95-E10, gazole, E85, GPLC, SP98. Le non respect de cette obligation est passible d'une amende, le contrôle étant effectué par la DGCCRF (Direction générale de la concurrence, de la consommation et de la répression des fraudes). </p>
<br/>
Voici ci-dessous une vidéo présentant pourquoi le prix des carburants fluctue autant (de façon simple et légère) :
<iframe width="560" height="315" src="https://www.youtube.com/embed/iUNJs695pmQ" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<br/>
## Modification du jeu de données
<p style='text-align: justify;'>Le jeu de données que j’ai sélectionné comportait initialement plusieurs informations qui ne me convenaient pas. Ainsi, j'ai utilisé l'outil libre OpenRefine, qui m'a permis de nettoyer, mettre en forme et d'harmoniser mes données. </p>
<br/>Voici le jeu de données originel :
<iframe src="https://data.opendatasoft.com/explore/embed/dataset/prix_des_carburants_j_7@public/table/?sort=update&dataChart=eyJxdWVyaWVzIjpbeyJjaGFydHMiOlt7InR5cGUiOiJsaW5lIiwiZnVuYyI6IkFWRyIsInNjaWVudGlmaWNEaXNwbGF5Ijp0cnVlLCJjb2xvciI6IiNGRjUxNUEiLCJ5QXhpcyI6InByaWNlX2dhem9sZSJ9LHsiYWxpZ25Nb250aCI6dHJ1ZSwidHlwZSI6ImxpbmUiLCJmdW5jIjoiQVZHIiwieUF4aXMiOiJwcmljZV9zcDk1Iiwic2NpZW50aWZpY0Rpc3BsYXkiOnRydWUsImNvbG9yIjoiIzFCNjY5OCJ9LHsiYWxpZ25Nb250aCI6dHJ1ZSwidHlwZSI6ImxpbmUiLCJmdW5jIjoiQVZHIiwieUF4aXMiOiJwcmljZV9zcDk4Iiwic2NpZW50aWZpY0Rpc3BsYXkiOnRydWUsImNvbG9yIjoiI0ZDRDIzQiJ9XSwieEF4aXMiOiJ1cGRhdGUiLCJtYXhwb2ludHMiOjUwLCJzb3J0IjoiIiwidGltZXNjYWxlIjoibW9udGgiLCJjb25maWciOnsiZGF0YXNldCI6InByaXhfZGVzX2NhcmJ1cmFudHNfal83QHB1YmxpYyIsIm9wdGlvbnMiOnsic29ydCI6InVwZGF0ZSJ9fX1dLCJ0aW1lc2NhbGUiOiIiLCJkaXNwbGF5TGVnZW5kIjp0cnVlLCJhbGlnbk1vbnRoIjp0cnVlLCJzaW5nbGVBeGlzIjp0cnVlfQ%3D%3D&location=12,48.93626,2.19263&basemap=jawg.streets&static=false&datasetcard=false" width="600" height="450" frameborder="0"></iframe>
<p style='text-align: justify;'>Pour commencer, nous pouvons voir que le champ des noms, marques et adresses avaient des formats de notation différents. Il y avait par exemple des adresses écrites entièrement en majuscules, d’autres entièrement en minuscules, d’autres avec uniquement l’initiale en majuscule, etc. 
Pour avoir un jeu de données plus clair et pouvoir les manipuler de la façon la plus ergonomique possible, j’ai décidé de modifier ces données en utilisant un seul format de notation qui serait commun pour tous les types de champs : mettre les initiales en majuscules. Voici ci-dessous un exemple avec la modification du champ "Adresse". </p>
````json
"columnName": "Adresse",
    "expression": "value.toTitlecase()",
    "onError": "keep-original",
    "repeat": false,
    "repeatCount": 10,
    "description": "Text transform on cells in column Adresse using expression value.toTitlecase()"
````
<p style='text-align: justify;'>J’ai cependant décidé de garder les différents types de carburant en majuscule quand il en était le cas (ex : SP95, SP98) car ce sont des acronymes pour définir « Sans Plomb 95 » ainsi que « Sans Plomb 98 ». Ces acronymes ayant une signification particulière et étant inscrits dans le langage courant, je n’ai pas trouvé nécessaire de modifier le format de notation de ces champs.
Pour continuer sur le sujet des carburants, les données de leur prix étaient également très différentes. La majorité des prix des carburants avaient un format de type décimal x,xxx (trois chiffres après la virgule). Une autre partie avaient un format de type x,xx (deux chiffres après la virgule). Enfin, d’autres carburants pouvaient avoir un prix inscrit plus fantaisiste, tels que 1,45999991 pour du SP95 dans certaines stations-services.
Pour les mêmes raisons évoquées précédemment sur l’uniformisation des formats de notation, j’ai décidé de conserver pour les prix des carburants un format de type décimal avec trois chiffres après la virgule. 
Pour ce faire, j’ai donc modifié les données initiales et procédé de la façon suivante :
<br/>
Pour transformer les nombres avec uniquement deux chiffres après la virgule, j’ai appliqué la formule GREL ci-dessous:</p>
````grel
value +"000"[0,5-value.length()]
````
<p style='text-align: justify;'>Cette formule, appliquée à toutes les cellules des champs des différents types de carburant m’a permis d’obtenir des prix avec trois chiffres après la virgule. Voici ci-dessous un exemple de la modification avec le prix du Gazole. </p>
````json
 "columnName": "Prix Gazole",
    "expression": "grel:value +\"00\"[0,5-value.length()]",
    "onError": "keep-original",
    "repeat": false,
    "repeatCount": 10,
    "description": "Text transform on cells in column Prix Gazole using expression grel:value +\"00\"[0,5-value.length()]"
````
<p style='text-align: justify;'>Pour transformer les nombres avec plus de trois chiffres après la virgule, j’ai créé une facette textuelle d’un champ de type "prix carburant". Puis, j’ai édité manuellement ces données pour les limiter à trois chiffres après la virgule. Voici ci-dessous un exemple de la modification avec le prix du SP95. </p>
````json
 "columnName": "Prix SP95",
    "expression": "value",
    "edits": [
      {
        "from": [
          "1.488999999999999"
        ],
        "fromBlank": false,
        "fromError": false,
        "to": "1.489"
````
<p style='text-align: justify;'>➨ L’historique de la totalité des modifications réalisées est accessible en cliquant <a href="https://mickaelliang.github.io/ModifsDataExamen/">ici</a>.<br/>
➨ Le fichier csv de mon jeu de données comportant les nouvelles modifications est disponible en téléchargement via Wetransfer en cliquant <a href="https://wetransfer.com/downloads/cd96ca7e9756b0c702c8362a71cda05d20210131155232/b844ea88f6a3d01849c6b8a34b421f8a20210131155258/219c41">ici</a>.</p><br/>
## Carte de France des clusters
<iframe frameborder="0" width="600" height="450" src="https://data.opendatasoft.com/map/embed/carte_de_chaleur/?&static=false&scrollWheelZoom=false"></iframe>
<i>Outil utilisé : opendatasoft</i><br/>
<p style='text-align: justify;'>Pour la première visualisation, j'ai pris en compte que le jeu de données que j'ai sélectionné possédait des coordonnées géographiques. Ainsi, j'ai décidé d'afficher le nombre de stations-essences à l'échelle nationale à l'aide d'une carte, à partir de leur géolocalisation. Avec l'affichage de type clusters, nous pouvons voir que la grande majorité des stations essences se situent dans les plus grandes villes de France, à noter Paris, Lyon, Marseille, Bordeaux et Lille. C'est un constat plutôt logique dans le sens où ce sont les villes où il y a le plus d'habitants, et donc de véhicules, par conséquent il y a la nécessité d'avoir un plus grand nombre de stations-essences aux alentours de ces villes. Cette carte, relativement lisible et compréhensible, permet ainsi de voir les différents clusters de stations-essences en France, à partir de la taille des bulles et de leurs couleurs (plus ou moins foncées selon leur ordre de grandeur).</p>

## Seconde visualisation
<div class="flourish-embed flourish-chart" data-src="visualisation/5142807"><script src="https://public.flourish.studio/resources/embed.js"></script></div>
## Troisième visualisation

## Requêtes SPARQL 


