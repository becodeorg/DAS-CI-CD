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

La dernière option ``Validate user account`` permet à l'utilisateur de valider les détails de leur carte de crédit.
Les utilisateurs validés ont accès à des minutes d'intégration continue gratuites sur des runners partagés. L'intégration continue est une pratique de développement logiciel qui consiste à vérifier automatiquement le code à chaque modification, et les runners sont des environnements d'exécution pour ces vérifications.

## 3. Création d'un groupe
Un groupe, c'est l'équivalent d'une organisation sur github. Pour en créer un, il suffit de cliquer sur le ``+`` en haut à gauche.  
![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/228c432f-f8f6-4f54-999a-325abd85dd05)

On peut importer un groupe d'une autrte instance de gitlab ou en créer un.  
![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/8262852c-d0e5-4117-9c4d-7cd4566200e4)  

On y indique le nom  
![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/07825209-8097-4434-b68f-490098595c4b)  

Et on change la visibilité   
![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/dff0c739-5d14-4a8c-ac93-dfc139193ce8)  

* **Public :** Pour que les projets soient ouvertement visibles par tout le monde, par exemple pour des projets open source.

* **Internal :** Pour que les projets soient privés mais que tous les membres de l'organisation y aient accès.

* **Private :** Pour un besoin d'un haut niveau de confidentialité et seuls les membres spécifiques du repo peuvent y accéder.

