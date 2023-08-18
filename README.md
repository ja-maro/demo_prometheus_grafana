# demo_prometheus_grafana
A simple docker compose with prometheus (monitoring itself) and grafana for data display

# to start
`docker compose up -d`

then access Prometheus at :
http://localhost:9090

Grafana at (login is admin/password) :
http://localhost:3000

# to remove
`docker compose down -v`

# French

## Prometheus
Prometheus est un outil de monitoring open-source comprenant une Time-series database, c’est-à-dire une base de données spécialisée dans le stockage de valeurs numériques représentant l’évolution d’une quantité spécifique au cours du temps (des valeurs horodatées). Il permet aussi un affichage basique sous forme de graphiques.
Prometheus est pull-based : il va récupérer les informations mises à disposition par micrometer (ou d’autres outils de monitoring) en les scrapant à intervalles réguliers.

### Accéder au serveur Prometheus
http://localhost:9090
Pour afficher les applications scrapées par Prometheus (définies dans le prometheus.yaml), on se connecte à l’endpoint /targets ( http://localhost:9090/targets ).
On peut définir des alertes sur Prometheus, ainsi qu’effectuer des requêtes en PromQL pour afficher les métriques scrapées de façon basique.

Prometheus est configuré via le fichier `/prometheus/prometheus.yaml`
La configuration actuelle lui fait surveiller Grafana et lui-même. On peut rajouter des jobs pour surveiller d'autres applications.

## Grafana
Grafana est un outil open-source d’affichage et d’analyse qui permet d’exploiter les métriques stockées dans Prometheus. On peut créer différents dashboards, qui regroupent plusieurs affichages, que l’on peut rassembler ou individualiser selon les besoins. Un outil de playlist offre la possibilité de cycler automatiquement entre plusieurs dashboards.
Grafana peut envoyer des alertes lorsque certaines conditions sont remplies.

### Accéder au serveur Grafana
On peut accéder aux dashboards Gafana via http://localhost:3000 (par défaut, login admin/password).  
Il existe de nombreux dashboards pré-configurés à importer directement : https://grafana.com/grafana/dashboards/  
On peut ensuite les modifier, ou créer son propre dashboard, et le remplir de panels nourris par des requêtes PromQL

Grafana se configure via l'interface web. L'application est pré-configurée pour utiliser Prometheus comme source de données, et contient 3 dashboards (2 pour Prometheus, 1 pour Grafana).

Il est possible de configurer à l'aide de fichiers et répertoire suivants ( dans `./grafana/`) :

`grafana.ini` pour la configuration générale
`provisioning/datasources/datasource.yml` pour la datasource prometheus
`provisioning/dashboards/dashboard.yml` & `provisioning/dashboards/` pour les différents dashboards

NB: on peut trouver de nombreux dashboards par ici : https://grafana.com/grafana/dashboards/  
(si vous les intégrez via le docker compose et non l'interface web, il faut modifier la variable de datasource sous la forme `${DS_xxxx}`)