# Monitoring
BEN MARZOUK Mohamed


# Guide de surveillance Docker Compose

Dans ce guide, je partage les étapes détaillées que j'ai suivies pour mettre en place mon système de surveillance utilisant Docker Compose, incluant des outils tels qu'Elasticsearch, Kibana, Logstash, Prometheus, Node Exporter, cAdvisor, Grafana, et Metricbeat.

## Installation et Configuration

### Ce dont j'ai eu besoin

- J'ai d'abord vérifié que **Docker** et **Docker Compose** étaient installés sur mon système.

### Préparation des fichiers YAML

- J'ai créé un dossier pour mon projet de surveillance et y ai placé mes fichiers `docker-compose.yml` et `prometheus.yml`.
