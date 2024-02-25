# Configuartion des users et des groupes
---
## 1. Mode admin
Tout d'abord, il faut passer en mode Admin.  Pour ce faire il faut cliquer en bas à gauche sur ``Admin Area``.

---

## 2. Création d'un utilisateur
- On créé un utilisateur en cliquant sur "New users" 
- Il faut que l'on remplisse le nom, pseudonyme et l'email. La personne pourra se connecter et changer son mot de passe à sa première connection. 
- L'option ``Projects limit`` definit le nombre de repo que pourra créer l'utilisateur.

---
Il faut également déterminer le niveau d'accès de l'utilisateur.

* **Regular :**  
Les utilisateurs réguliers ont accès à leurs propres groupes et projets dans GitLab.
Cela signifie qu'ils peuvent travailler sur les projets auxquels ils sont associés, créer de nouveaux projets dans ces groupes, et utiliser les fonctionnalités associées à leurs projets spécifiques.

* **Administrator :**  
Les administrateurs ont un accès illimité à tous les groupes, projets, utilisateurs et fonctionnalités de GitLab.
Ils ont le plus haut niveau de privilèges, ce qui leur permet de configurer et de gérer l'ensemble du système GitLab, y compris les droits d'accès des autres utilisateurs.

* **External :**
Les utilisateurs externes ne peuvent pas voir les projets internes ou privés à moins que l'accès ne leur soit explicitement accordé.
Ils ne peuvent pas créer de projets, de groupes, ni de fragments de code personnels. Cela limite leur capacité à contribuer à des projets ou à créer du contenu dans GitLab.

---

La dernière option ``Validate user account`` permet à l'utilisateur de valider les détails de leur carte de crédit.
Les utilisateurs validés ont accès à des minutes d'intégration continue gratuites sur des runners partagés.

---

## 3. Création d'un groupe
Un groupe, permet de gérer la configuration sur un ensemble d'utilisateurs. 
- Pour en créer un, il suffit de cliquer sur le ``+`` en haut à gauche.  
- On peut importer un groupe d'une autrte instance de gitlab ou en créer un.  

---

### Exercice 
- Creér un groupe par exemple ``BeCode``
- Créer un utilisateur avec les droits admins


