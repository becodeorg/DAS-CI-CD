# Installation de Gitlab 

**Minimum requirement :**
- 4 core CPU
- 4 G de ram

Connectez vous à la vm.

```
ssh azureuser@YOUR-IP -i userX.pem
```

> Login gitlab: root:Test1234!

- Maxime :
    - Gitlab Instance : http://20.13.171.42
    - Runner 1 : 20.13.167.219
    - Runner 2 : 98.71.17.199
- Karim :
    - Gitlab Instance : http://20.123.64.161 
    - Runner 1 : 20.123.65.171
    - Runner 2 : 20.13.166.86
- Arthur :
    - Gitlab Instance : http://98.71.16.171
    - Runner 1 : 98.71.16.252
    - Runner 2 : 20.13.160.111
- Sébastien :
    - Gitlab Instance : http://20.13.166.211
    - Runner 1 : 20.13.168.58
    - Runner 2 : 20.13.168.66
- Benjamin :
    - Gitlab Instance : http://20.13.168.224
    - Runner 1 : 20.13.169.28
    - Runner 2 : 52.158.40.20

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

Une fois que tout cela est fini, nous devons rajouter l'ip de gitlab dans le fichier de config de gitlab-runner
```
[runners.docker]
  extra_hosts = ["gitlab.das.becode:20.13.147.210","registry.das.becode:20.13.147.210"]
```
