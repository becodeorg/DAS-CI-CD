# Configuartion des users et des groupes

## 1. Mode admin
Tout d'abord, il faut passer en mode Admin.  Pour ce faire il faut cliquer en bas à gauche sur ``Admin Area``.

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/073cc528-93b5-4a0b-81df-c62f793a8b42)

## 2. Création d'un utilisateur
Ensuite on recherche l'option "Users" pour accéder à la gestion des utilisateurs et on clique sur "New users" 
Il faut que l'on remplisse le nom, pseudonyme et l'email. Si le serveur smtp est configuré, la personne pourra se connecter et changer son mot de passe à sa première connection. 

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/aba3845c-1c26-49da-a8fe-7f87c9d60fc7)

L'option ``Projects limit`` definit le nombre de repo que pourra créer l'utilisateur.

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/1da89841-9f3c-4c8b-9c7d-c5d6580479b7)

Il faut également déterminer le niveau d'accès de l'utilisateur.

* **Regular :**  
Les utilisateurs réguliers ont accès à leurs propres groupes et projets dans GitLab.
Cela signifie qu'ils peuvent travailler sur les projets auxquels ils sont associés, créer de nouveaux projets dans ces groupes, et utiliser les fonctionnalités associées à leurs projets spécifiques.

* **Administrator :**  
Les administrateurs ont un accès illimité à tous les groupes, projets, utilisateurs et fonctionnalités de GitLab.
Ils ont le plus haut niveau de privilèges, ce qui leur permet de configurer et de gérer l'ensemble du système GitLab, y compris les droits d'accès des autres utilisateurs.

* **External (Utilisateur externe) :**
Les utilisateurs externes ne peuvent pas voir les projets internes ou privés à moins que l'accès ne leur soit explicitement accordé.
Ils ne peuvent pas créer de projets, de groupes, ni de fragments de code personnels. Cela limite leur capacité à contribuer à des projets ou à créer du contenu dans GitLab.

La dernière option ``Validate user account`` permet de valider soi-même en saisissant les détails de leur carte de crédit.
Les utilisateurs validés ont accès à des minutes d'intégration continue gratuites sur des runners partagés. L'intégration continue est une pratique de développement logiciel qui consiste à vérifier automatiquement le code à chaque modification, et les runners sont des environnements d'exécution pour ces vérifications.

## 3. Création d'un groupe



