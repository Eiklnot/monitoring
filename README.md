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

### Metricbeat

- Collecte les métriques du système et les envoie vers Elasticsearch.
- Configuré via le fichier `metricbeat/metricbeat.yml`.
- Dépend d'Elasticsearch et Kibana pour le stockage et la visualisation des données.

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


## Intégration de Loki et Promtail pour la Gestion des Logs

J'ai choisi d'intégrer **Loki** et **Promtail** dans mon système de monitoring pour une gestion efficace des logs. Voici comment j'ai procédé :

### Loki

J'utilise **Loki** pour centraliser la gestion des logs. Ce système de gestion de logs est non seulement scalable et hautement disponible, mais il est également conçu pour être coût-efficace et facile à utiliser. Grâce à son intégration directe avec Grafana, je peux visualiser les logs de manière intuitive.

- Accessible via le port `3100`.
- J'ai configuré un volume nommé `loki-data` pour stocker les données de logs, assurant ainsi leur persistance.

### Promtail

Pour acheminer les logs vers Loki, j'ai mis en place **Promtail**. En tant qu'agent, Promtail surveille les fichiers de logs et les envoie à Loki. Grâce à cela, je bénéficie d'une gestion centralisée des logs qui complète mon système de monitoring.

- Promtail est déjà configuré pour surveiller les fichiers dans `/var/log` et `/var/lib/docker/containers`. Le fichier `./promtail-config.yml`, que j'ai préparé à l'avance, spécifie les sources de logs et leur traitement.

### Mise en place dans mon système de monitoring

La configuration et le lancement de Loki et Promtail ont été réalisés via mon fichier `docker-compose.yml`. Pour Loki, j'ai spécifié l'utilisation de l'image `grafana/loki:latest` et mappé le port `3100` pour y accéder facilement. Les données de logs sont persistées grâce au volume `loki-data`.

Pour Promtail, étant donné que mon fichier `promtail-config.yml` était déjà configuré, j'ai simplement veillé à ce que Promtail soit correctement lié à Loki pour envoyer les logs collectés.

Cette intégration

## Fonctionnement de l'ELK Stack

L'ELK Stack est une suite de trois outils open-source, Elasticsearch, Logstash et Kibana, qui ensemble fournissent une solution puissante pour le traitement, le stockage et la visualisation des données en temps réel.

**Elasticsearch**
C'est un moteur de recherche et d'analyse distribué, capable de traiter de grandes quantités de données structurées et non structurées en temps réel. Il stocke les données et permet des recherches complexes à haute vitesse.

**Logstash**
C'est un pipeline de traitement de données côté serveur qui ingère des données de diverses sources, les transforme selon des filtres configurables et les expédie vers un ou plusieurs stocks de données, dont Elasticsearch. Il est très flexible et supporte de nombreux types d'entrées, de filtres et de sorties.

**Kibana**
C'est une interface utilisateur web pour visualiser les données d'Elasticsearch. Kibana permet de créer des tableaux de bord dynamiques qui permettent d'explorer et de visualiser les données en temps réel.

Le processus général commence par la collecte de données (logs, métriques, etc.) par Logstash, qui les traite et les envoie à Elasticsearch pour le stockage. Kibana est ensuite utilisé pour interroger et visualiser ces données, permettant aux utilisateurs de découvrir des insights et des tendances dans les données presque en temps réel.

## Fonctionnement de Grafana

Grafana est utilisé pour visualiser et analyser les données de monitoring en temps réel, provenant de sources telles que Prometheus, cAdvisor, Node Exporter, et Loki. Chaque outil joue un rôle spécifique dans l'écosystème de monitoring :

**Prometheus** 
collecte et stocke les métriques sous forme de séries temporelles, permettant le monitoring de la santé des services et l'utilisation des ressources.

**cAdvisor**
 fournit des métriques sur les performances et l'utilisation des ressources par les conteneurs, qui sont collectées par Prometheus.

**Node Exporter**
 expose les métriques systèmes des serveurs, telles que l'utilisation du CPU et de la mémoire, à Prometheus.

**Loki**
 gère les logs, permettant leur analyse en corrélation avec les métriques collectées par Prometheus.

En combinant ces outils, Grafana offre une plateforme unifiée pour visualiser à la fois les métriques et les logs, facilitant ainsi le diagnostic et le monitoring en profondeur des infrastructures IT et des applications.

## Bonnes Pratiques à Suivre

- **Sécurité**: Il faut changer les mots de passe par défaut et utiliser des variables d'environnement ou des fichiers secrets pour sécuriser les informations sensibles.
- **Maintenance**: Il est nécessaire de mettre régulièrement à jour les images de vos services afin de bénéficier des dernières corrections de sécurité et améliorations de fonctionnalités.
- **Surveillance des Performances**: Il est recommandé d'exploiter les outils disponibles (comme Kibana et Grafana) pour monitorer activement la santé et les performances de votre
