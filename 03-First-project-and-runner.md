# Premier projet et création du premier runner
## Le premier projet
On clique sur le bouton "New Project" pour commencer le processus de création d'un nouveau projet et 
on sélectionne le type de projet que l'on souhaite créer, qu'il s'agisse d'un projet vierge, 
d'un import depuis un autre référentiel, ou d'un modèle de projet.

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/325601b4-65e1-4639-9613-c75d029671e6)


On remplit les détails du projet tels que le nom, la description, et d'autres paramètres pertinents 
et on choisit la visibilité du projet en fonction des besoins, que ce soit "Public", "Internal", ou "Private".

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/cb08a517-9223-4d92-b26e-b9ddbac0d9be)

## Les pipelines, jobs et stages

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

En résumé, dans GitLab CI/CD, on définit des jobs pour effectuer des tâches spécifiques, 
on les regroupe en étapes logiques, et ces étapes sont ensuite regroupées dans un pipeline qui 
est déclenché automatiquement lorsqu'un commit est poussé sur la branche configurée.

![](https://docs.gitlab.com/ee/ci/jobs/img/pipeline_grouped_jobs_v14_2.png)

## Création du premier runner
Création du fichier .gitlab.yaml
```
stages:
  - build
  - test

job_build:
  stage: build
  script:
    - echo "Building the project"

job_test:
  stage: test
  script:
    - echo "Running tests"

```

Pour créer un runner, il faut aller dans l'onglet ``settings`` dans le menu à gauche et on étend la rubrique ``Runners``
![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/21668686-45ef-49e9-a74f-cb736d03cf19)

On choisit le runner pour Linux. Il faut également y indiquer un tag, mmais on verra plus tard tard comment l'utiliser.
![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/104c579e-45fe-4b70-8ee4-ae34f47feeb5)

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/beaba3cc-c4c3-4de4-a1ee-78e4705f387f)

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/b4300593-4a68-48d5-bc03-ede4f9e0d661)

Maintenant, on va pouvoir enregistrer le runner. 
![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/a4773056-007a-4e89-b677-905ba71967f3)

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/18a44719-3e1c-4027-bf43-1bcd930e89c6)

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/e96ef94a-02c9-4774-99e1-5cb789085572)

et pour vérifier que le runner a bien été créer : 

```
sudo cat /etc/gitlab-runner/config.toml
```


