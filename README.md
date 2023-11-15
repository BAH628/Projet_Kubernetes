
Auteur : Maimouna Bella BAH

LinkedIn : https://www.linkedin.com/in/maimounab

-------
# Mini-projet-Kubernetes

-----
## Sujet:
-----

### Mini-projet: Déployez Wordpress à l'aide de manifests (et non par helm )



-------
*  Déployez wordpress en suivant les étapes suivantes:
    * Créez un deployment mysql avec un seul replicat.
    * Créez un service de type clusteriP pour exposer vos pods mysql.
    * Créez un deployment wordpress avec les bonnes variables d'environnement pour se connecter à la base de données mysql.
    * Stocker les données de wordpress sur un volme mounté dans le /data de votre noeud.
    * Créer un service de type nodeport pour exposer le frontend wordpress.
    * Utiliser des manifests pour réaliser cet exercice.
-----
## Les étapes :

### Déploiement MySQL
Le déploiement MySQL est défini avec l'API `apps/v1` et le type `Deployment`. Il spécifie les caractéristiques du déploiement, telles que le nombre de réplicas, la stratégie de déploiement et les conteneurs à exécuter.
- Le déploiement "wp-mysql" a des étiquettes qui le lient à l'application WordPress.
- Comme demandé une réplique, ce qui signifie qu'un seul pod MySQL sera créé.
- Les sélecteurs `matchLabels` sont utilisés pour associer les pods du déploiement aux services correspondants.
- Le conteneur MySQL utilise l'image `mysql:5.7`.
- Les ports sont exposés pour permettre la communication avec le conteneur MySQL.
- Un volume persistant est monté pour stocker les données de la base de données.

### Secret
L'objet Secret est utilisé pour stocker les informations sensibles, telles que les mots de passe, de manière sécurisée.
- Le secret "wordpress-secret" contient les clés `mysql_password` et `mysql_random_root_password` encodées en base64.
- Ces valeurs sont utilisées par les conteneurs pour accéder aux informations sensibles.

### Namespace
Le Namespace est utilisé pour regrouper les ressources en fonction de leur application ou de leur objectif.
- Le Namespace "wordpress" est créé pour héberger les ressources liées à WordPress.

### Déploiement WordPress
Le déploiement WordPress est similaire au déploiement MySQL, mais il utilise l'image `wordpress:latest` et définit des variables d'environnement spécifiques pour se connecter à la base de données MySQL.
- Le déploiement "wordpress" et est étiqueté pour être associé à l'application WordPress.
- Il a une réplique, ce qui signifie qu'un seul pod WordPress sera créé.
- Les sélecteurs `matchLabels` sont utilisés pour associer les pods du déploiement aux services correspondants.
- La stratégie de déploiement est définie sur "Recreate".
- Le conteneur WordPress utilise l'image `wordpress:latest` et définit des variables d'environnement pour se connecter à la base de données MySQL.
- Les ports sont exposés pour permettre l'accès au site WordPress.
- Un volume persistant est monté pour stocker les fichiers du site WordPress.

### Services
Deux services sont définis pour exposer les déploiements MySQL et WordPress à l'intérieur du cluster.
- Le service "wp-mysql" expose le port 3306 du déploiement MySQL et utilise un type "ClusterIP".
- Le service "wordpress" expose le port 80 du déploiement WordPress et utilise un type "NodePort".

### Persistent Volumes et Persistent Volume Claims
Des volumes persistants sont utilisés pour stocker les données de la base de données MySQL et les fichiers du site WordPress.
- Un Persistent Volume (PV)  "mysql-pv" est créé avec une capacité de 10Gi et un chemin d'accès sur le nœud hôte.
- Un Persistent Volume Claim (PVC) "mysql-pvc" est créé pour réclamer un espace de stockage auprès du PV "mysql-pv".
- Des PV et PVC similaires sont créés pour le stockage du site WordPress.

### Ingress
L'objet Ingress est utilisé pour configurer les règles d'accès au site WordPress depuis l'extérieur du cluster.
- L'Ingress "wordpress-ingress" spécifie une règle pour l'hôte "wordpress.com" et redirige le trafic vers le service WordPress sur le port 80.

### Network Policy
Le Network Policy pour définir les règles de communication réseau entre les pods.
- La Network Policy "wordpress-network-policy" spécifie que seuls les pods avec l'étiquette "app: wp-mysql" peuvent accéder au port 3306 des pods avec l'étiquette "app: wordpress".
  
