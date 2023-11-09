
Auteur : Maimouna Bella BAH

Contexte : DevOps Bootcamp

Centre de formation : eazytraining.fr

LinkedIn : https://www.linkedin.com/in/maimounab

-------
# Mini-projet-Kubernetes

-----
## Sujet:
-----

#### Mini-projet: Déployez Wordpress à l'aide de manifests (et non par helm )
![Texte alternatif](file:///home/bella/Documents/bootcamp/Kubernetes/images.jpeg)


-------
*  Déployez wordpress en suivant les étapes suivantes:
    * Créez un deployment mysql avec un seul replicat.
    * Créez un service de type clusteriP pour exposer vos pods mysql.
    * Créez un deployment wordpress avec les bonnes variables d'environnement pour se connecter à la base de données mysql.
    * Stocker les données de wordpress sur un volme mounté dans le /data de votre noeud.
    * Créer un service de type nodeport pour exposer le frontend wordpress.
    * Utiliser des manifests pour réaliser cet exercice.
