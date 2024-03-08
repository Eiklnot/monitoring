# Monitoring
BEN MARZOUK Mohamed


# Guide de Monitroring Docker Compose

Dans ce guide, je partage les étapes détaillées que j'ai suivies pour mettre en place mon système de monitoring utilisant Docker Compose, incluant des outils tels qu'Elasticsearch, Kibana, Logstash, Prometheus, Node Exporter, cAdvisor, Grafana, et Metricbeat.

## Installation et Configuration

### Ce dont j'ai eu besoin

- J'ai d'abord vérifié que **Docker** et **Docker Compose** étaient installés sur mon système.

### Préparation des fichiers YAML

- J'ai créé un dossier pour mon projet de monitoring et y ai placé mes fichiers `docker-compose.yml` et `prometheus.yml`.

### Configuration avec Docker Compose

- Mon fichier `docker-compose.yml` configure les services essentiels à mon système de monitoring, incluant leurs images, ports, volumes, et dépendances.

### Lancement des Services

- Dans un terminal ouvert dans le répertoire de mon projet, j'ai lancé les services avec la commande :
  ```bash
  sudo docker-compose up -d
  ```
- Cette commande a téléchargé les images nécessaires et démarré les conteneurs en arrière-plan.

### Vérification

- Pour vérifier le statut des services, j'ai utilisé la commande suivante dans mon terminal :
  ```bash
  sudo docker-compose ps
  ```