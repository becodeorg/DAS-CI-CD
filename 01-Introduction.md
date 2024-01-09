# Le CI/CD avec Gitlab 

## Les pipelines, jobs et stages (5 minutes)

### Job 
Un "job" représente une tâche individuelle à accomplir dans le cadre du processus CI/CD. 

```
say_hello:
  script:
    - echo "Hello DAS!"
```

### Stage 
Les "stages" permettent d'organiser le pipeline et d'exécuter 
des jobs de manière séquentielle ou parallèle, en fonction des besoins du projet.

```
stages:
  - build
  - test
  - deploy
```

### Pipelines
Chaque fois qu'un commit est effectué sur une branche surveillée (par exemple, la branche principale), 
GitLab déclenche automatiquement la création d'un nouveau pipeline. Ce pipeline est un ensemble de "jobs" organisés en "Stages" (étapes).  

```
stages:
  - build
  - test
  - deploy

job_build:
  stage: build
  script:
    - echo "Building the application..."

job_test:
  stage: test
  script:
    - echo "Running tests..."

job_deploy:
  stage: deploy
  script:
    - echo "Deploying the application..."
```
### Conclusion 
En résumé, dans GitLab CI/CD, vous définissez des jobs pour effectuer des tâches spécifiques, 
les regroupez en étapes logiques, et ces étapes sont ensuite regroupées dans un pipeline qui 
est déclenché automatiquement lorsqu'un commit est poussé sur la branche configurée.

![](https://docs.gitlab.com/ee/ci/jobs/img/pipeline_grouped_jobs_v14_2.png)

## Installation (2 Heures) 
**Minimum requirement :**
- 4 core
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
  

### 1. Installation et configuration des dépendances

On fait un update 
 
```
sudo apt-get update -y && sudo apt-get upgrade -y
```

On installe les dépendances 
```
sudo apt-get install -y curl openssh-server ca-certificates perl
```

On install postfix pour l'envoie d'email  

```
sudo apt-get install -y postfix
```

### 2. Installation de GitLab package 
**Repository setup**

On ajoute gitlab dans la liste des paquets Debian 

```
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash
```
ou la version community

```
curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
```

### 3. Configuration et installation


On lance l'installation de gitlab

```
sudo GITLAB_ROOT_PASSWORD="<strongpassword>" EXTERNAL_URL="http://gitlab.example.com" apt install gitlab-ee
```
ou la version community
```
sudo GITLAB_ROOT_PASSWORD="<strongpassword>" EXTERNAL_URL="http://gitlab.example.com" apt install gitlab-ce
```

### 4. Gitlab start

Si l'url doit être modifié, il faut relancer la configuration.

```
sudo gitlab-ctl reconfigure
```




