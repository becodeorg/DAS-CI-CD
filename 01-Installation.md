# Installation de Gitlab 

**Minimum requirement :**
- 4 core CPU
- 4 G de ram

Connectez vous à la vm.

```
ssh admin@YOUR-IP -i userX.pem
```

- IP User 1  
- IP User 2
- IP User 3
- IP User 4
- IP User 5  

user : admin

**Documentation :** 
- [Installation sur debian](https://about.gitlab.com/install/#debian)
- [Next Steps](https://docs.gitlab.com/ee/install/next_steps.html)
  

## 1. Installation et configuration des dépendances

On fait un update 
 
```
sudo apt-get update -y && sudo apt-get upgrade -y
```

On installe les dépendances 
```
sudo apt-get install -y curl openssh-server ca-certificates perl postfix
```

## 2. Installation de GitLab package 
**Repository setup**

On ajoute gitlab dans la liste des paquets Debian 

```
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash
```
ou la version community

```
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
```

## 3. Configuration et installation


On lance l'installation de gitlab

```
sudo GITLAB_ROOT_PASSWORD="<strongpassword>" EXTERNAL_URL="http://gitlab.example.com" apt install gitlab-ee
```
ou la version community
```
sudo GITLAB_ROOT_PASSWORD="<strongpassword>" EXTERNAL_URL="http://gitlab.example.com" apt install gitlab-ce
```

## 4. Configuration du serveur SMTP
En fonction du serveur smtp :
- https://docs.gitlab.com/omnibus/settings/smtp.html


## 5. Installation Gitlab Runner
```bash
curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash
```

Et ensuite :  
```
sudo apt-get install gitlab-runner
```

```
sudo gitlab-runner start
```
 

Vérification du status de gitlab-runner
```
sudo gitlab-runner status
```
 
Bien mettre les droits sudo quand on register le runner.

