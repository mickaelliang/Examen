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
<iframe frameborder="0" width="580" height="450" src="https://data.opendatasoft.com/map/embed/carte_de_chaleur/?&static=false&scrollWheelZoom=false"></iframe>
<i>Outil utilisé : Opendatasoft</i><br/>
<p style='text-align: justify;'>Pour la première visualisation, j'ai pris en compte que le jeu de données que j'ai sélectionné possédait des coordonnées géographiques. Ainsi, j'ai décidé d'afficher le nombre de stations-essences à l'échelle nationale à l'aide d'une carte, à partir de leur géolocalisation. Avec l'affichage de type clusters, nous pouvons voir que la grande majorité des stations-essences se situent dans les plus grandes villes de France, à noter Paris, Lyon, Marseille, Bordeaux et Lille. C'est un constat plutôt logique dans le sens où ce sont les villes où il y a le plus d'habitants, et donc de véhicules, par conséquent il y a la nécessité d'avoir un plus grand nombre de stations-essences aux alentours de ces villes. Cette carte, relativement lisible et compréhensible, permet ainsi de voir les différents clusters de stations-essences en France, à partir de la taille des bulles et de leurs couleurs (plus ou moins foncées selon leur ordre de grandeur).</p>

## Column chart comparatif du prix du carburant selon les 5 plus grandes villes de France
<div class="flourish-embed flourish-chart" data-src="visualisation/5152790"><script src="https://public.flourish.studio/resources/embed.js"></script></div>
<i>Outil utilisé : Flourish</i><br/>
<p style='text-align: justify;'>Pour la seconde visualisation, j'ai décidé d'afficher le prix des différents types de carburants en fonction des 5 plus grandes villes de France. Pour ce faire, j'ai utilisé la représentation via un column chart, proposé par Flourish. Ainsi, nous pouvons voir qu'à chaque fois, le prix du carburant le plus élevé est constaté dans l'une des stations-essences de Paris. En effet, il faut évidemment prendre en compte que certaines villes peuvent avoir plusieurs stations-essences, avec des prix parfois très différents d'une station à une autre. Pour analyser le tarif des carburants dans une ville en détail, j'ai utilisé l'option "Row filter" de Flourish. Cela m'a permis d'afficher un petit menu interactif en haut à gauche de la visualisation, permettant de sélectionner une ville en particulier. De ce fait, en analysant la ville de Paris par exemple, j'ai pu constater qu'elle offrait plusieurs prix pour le carburant Gazole : 1,890€/L, 1,589€/L, 1,530€/L, etc. A l'inverse, nous pouvons voir que parmi ces 5 grandes villes, c'est Lyon qui propose globalement les prix les plus bas. En effet, toujours pour le prix du Gazole, cette ville offre un tarif maximum d'1,419€/L dans l'une de ses stations-services, et un tarif minimum de 1,289€/L. <br/></p> 

## Nuage de points comparatif du prix du SP98 selon la marque
<div class="flourish-embed flourish-scatter" data-src="visualisation/5144891"><script src="https://public.flourish.studio/resources/embed.js"></script></div>
<i>Outil utilisé : Flourish</i><br/>
<p style='text-align: justify;'>Pour la troisième visualisation, J'ai utilisé la représentation par nuage de points, proposé par Flourish. Ce nuage de points permet également d'établir un comparatif, mais cette fois-ci en fonction du prix du SP98 et de la marque. Nous pouvons voir que la grande majorité des tarifs proposés se situe entre 1,500€/L et 1,750€/L. Notons d'ailleurs que le nuage de points utilisé pour cette représentation n'est pas totalement disparse. En effet, il est intéressant de remarquer que les points formés par les différents prix formerait presque une sorte de courbe sinusoïdale. En analysant cette visualisation, nous pouvons constater que c'est la marque Système U qui propose le prix le plus cher pour le SP98 dans l'une de ses stations-essences : 4,46€/L. A l'inverse, c'est Total qui offre le prix le moins cher pour ce carburant dans l'une de ses stations-essences, prix qui est seulement de 0,60€/L. </p>
<br/>
## Requêtes SPARQL 
<p style='text-align: justify;'>Pour enrichir mon travail, j'ai décidé d'utiliser une requête SPARQL, créée avec Wikidata Query. Cette requête m'a permis d'afficher les différentes stations-services présentes aux Etats-Unis. Nous pouvons voir sur la carte que j'ai intégré ci-dessous, que les stations-essences sont globalement bien réparties dans le pays. A la différence de la France où il y a plusieurs clusters dans les grandes villes, nous pouvons voir qu'aux Etats-Unis, il ne semble y'en avoir qu'un seul, aux alentours d'Oklahoma City.</p>
````sparql
#Stations-services aux Etats-Unis
#defaultView:Map
SELECT ?stationEssence ?stationEssenceLabel ?coords WHERE {
  SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE],en,fr". }
  ?stationEssence wdt:P31 wd:Q205495.
  ?stationEssence wdt:P17 wd:Q30.
  ?stationEssence wdt:P625 ?coords.
}
````
<center><iframe frameborder="0" width="580" height="450" src="https://query.wikidata.org/embed.html#%23Stations-services%20aux%20Etats-Unis%0A%23defaultView%3AMap%0ASELECT%20%3FstationEssence%20%3FstationEssenceLabel%20%3Fcoords%20WHERE%20%7B%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%20bd%3AserviceParam%20wikibase%3Alanguage%20%22%5BAUTO_LANGUAGE%5D%2Cen%2Cfr%22.%20%7D%0A%20%20%3FstationEssence%20wdt%3AP31%20wd%3AQ205495.%0A%20%20%3FstationEssence%20wdt%3AP17%20wd%3AQ30.%0A%20%20%3FstationEssence%20wdt%3AP625%20%3Fcoords.%0A%7D" referrerpolicy="origin" sandbox="allow-scripts allow-same-origin allow-popups"></iframe></center>
<br/>
## Conclusion
<p style='text-align: justify;'>J'ai trouvé la réalisation de ce projet très enrichissante dans le sens où elle m'a permis de me confronter plus en détails à la manipulation des différents outils de dataviz. Cela dit, j'ai rencontré quelques difficultés en les utilisant. Par exemple, pour la réalisation de ma deuxième datavisualisation (le column chart comparatif du prix des carburants selon les 5 plus grandes villes de France), je voulais au départ afficher un column chart comparatif du prix des selon toutes les villes de France. Cependant, le rendu était totalement illisible de par le nombre de valeurs de mon jeu de données. Même en essayant d'autres outils (Datawrapper, Rawgraph, Palladio) ainsi que d'autres formes de visualisations, l'affichage ne me convenait pas. C'est pourquoi j'ai restreint le comparatif du prix des carburants selon les 5 plus grandes villes de France, en modifiant mon jeu de données avec OpenRefine. Enfin, je pense que le menu "Row filter" que j'ai intégré en haut à gauche permet de rendre la visibilité encore plus claire en dévoilant le prix de chacun des carburants selon une ville en particulier.
 </p>
