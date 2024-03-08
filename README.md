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

## Commandes Utilisées

- **Elasticsearch**: Accessible via [http://localhost:9200](http://localhost:9200).
- **Kibana**: Interface disponible sur [http://localhost:5601](http://localhost:5601).
- **Logstash**: Reçoit des données sur le port `5044`.
- **Prometheus**: Grattage des métriques configuré sur le port `9090`.
- **Grafana**: Connecté à [http://localhost:3000](http://localhost:3000) pour visualiser les métriques, avec les identifiants `admin` / `password`.

## Détails sur la Configuration des Services

### Elasticsearch

- Stocke les données collectées pour une recherche et une analyse rapide.
- Accessible sur le port `9200`.

### Kibana

- Offre une interface utilisateur pour visualiser les données stockées dans Elasticsearch.
- Dépend d'Elasticsearch pour fonctionner correctement.
- Accessible sur le port `5601`.

### Logstash

- Traite et transfère les données de journalisation vers Elasticsearch.
- Reçoit des données sur le port `5044`.
- Dépend d'Elasticsearch.

### Prometheus

- Collecte et stocke les métriques sous forme de séries temporelles.
- Configuré pour gratter les métriques de différents services.
- Accessible sur le port `9090`.

### Node Exporter

- Expose les métriques du système d'un hôte pour la collecte par Prometheus.
- Exposé sur le port `9100`.

### cAdvisor

- Fournit des métriques sur l'utilisation des ressources et les performances des conteneurs.
- Exposé sur le port `8080`.

### Grafana

- Permet la visualisation des données de monitoring à partir de sources telles que Prometheus.
- Accessible sur le port `3000`.
- Les identifiants par défaut sont configurés via les variables d'environnement dans le fichier `docker-compose.yml`.
