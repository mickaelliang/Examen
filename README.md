# À propos
Page en cours de travaux !

## Modification du jeu de données
<p style='text-align: justify;'>Le jeu de données que j’ai sélectionné comportait initialement plusieurs informations qui ne me convenaient pas. Ainsi, j'ai utilisé l'outil libre OpenRefine, qui m'a permis de nettoyer, mettre en forme et d'harmoniser mes données. </p>
<br/>Voici le jeu de données originel :
<iframe src="https://data.opendatasoft.com/explore/embed/dataset/prix_des_carburants_j_7@public/table/?sort=update&dataChart=eyJxdWVyaWVzIjpbeyJjaGFydHMiOlt7InR5cGUiOiJsaW5lIiwiZnVuYyI6IkFWRyIsInNjaWVudGlmaWNEaXNwbGF5Ijp0cnVlLCJjb2xvciI6IiNGRjUxNUEiLCJ5QXhpcyI6InByaWNlX2dhem9sZSJ9LHsiYWxpZ25Nb250aCI6dHJ1ZSwidHlwZSI6ImxpbmUiLCJmdW5jIjoiQVZHIiwieUF4aXMiOiJwcmljZV9zcDk1Iiwic2NpZW50aWZpY0Rpc3BsYXkiOnRydWUsImNvbG9yIjoiIzFCNjY5OCJ9LHsiYWxpZ25Nb250aCI6dHJ1ZSwidHlwZSI6ImxpbmUiLCJmdW5jIjoiQVZHIiwieUF4aXMiOiJwcmljZV9zcDk4Iiwic2NpZW50aWZpY0Rpc3BsYXkiOnRydWUsImNvbG9yIjoiI0ZDRDIzQiJ9XSwieEF4aXMiOiJ1cGRhdGUiLCJtYXhwb2ludHMiOjUwLCJzb3J0IjoiIiwidGltZXNjYWxlIjoibW9udGgiLCJjb25maWciOnsiZGF0YXNldCI6InByaXhfZGVzX2NhcmJ1cmFudHNfal83QHB1YmxpYyIsIm9wdGlvbnMiOnsic29ydCI6InVwZGF0ZSJ9fX1dLCJ0aW1lc2NhbGUiOiIiLCJkaXNwbGF5TGVnZW5kIjp0cnVlLCJhbGlnbk1vbnRoIjp0cnVlLCJzaW5nbGVBeGlzIjp0cnVlfQ%3D%3D&location=12,48.93626,2.19263&basemap=jawg.streets&static=false&datasetcard=false" width="600" height="450" frameborder="0"></iframe>
<p style='text-align: justify;'>Pour commencer, les noms, marques et adresses auxquelles appartiennent les stations-services avaient des formats de notation différentes. Il y avait par exemple des adresses écrites entièrement en majuscules, d’autres entièrement en minuscules, d’autres avec uniquement l’initiale en majuscule, etc. 
Pour avoir un jeu de données plus clair et pouvoir les manipuler de la façon la plus ergonomique possible, j’ai décidé de modifier ces données en utilisant un seul format de notation qui serait commun pour tous les types de champs : mettre les initiales en majuscules. Voici ci-dessous un exemple avec l'adresse. </p>
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
Pour transformer les nombres avec uniquement deux chiffres après la virgule, j’ai appliqué la formule GREL ci-dessous:</p>
````grel
value +"000"[0,5-value.length()]
````
<p style='text-align: justify;'>Cette formule, appliquée à toutes les cellules des champs des différents types de carburant m’a permis d’obtenir des prix avec trois chiffres après la virgule. Voici ci-dessous un exemple avec le prix du Gazole. </p>
````json
 "columnName": "Prix Gazole",
    "expression": "grel:value +\"00\"[0,5-value.length()]",
    "onError": "keep-original",
    "repeat": false,
    "repeatCount": 10,
    "description": "Text transform on cells in column Prix Gazole using expression grel:value +\"00\"[0,5-value.length()]"
````
<p style='text-align: justify;'>Pour transformer les nombres avec plus de trois chiffres après la virgule, j’ai créé une facette textuelle d’un champ de type "prix carburant". Puis, j’ai édité manuellement ces données pour les limiter à trois chiffres après la virgule. Voici ci-dessous un exemple avec le prix du SP95. </p>
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
<p style='text-align: justify;'>L’historique de la totalité des modifications réalisées est présent sur la page github suivante : </p>
## Première visualisation

## Seconde visualisation

## Troisième visualisation


