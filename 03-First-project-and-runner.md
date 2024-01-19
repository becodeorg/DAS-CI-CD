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

En résumé, dans GitLab CI/CD, vous définissez des jobs pour effectuer des tâches spécifiques, 
les regroupez en étapes logiques, et ces étapes sont ensuite regroupées dans un pipeline qui 
est déclenché automatiquement lorsqu'un commit est poussé sur la branche configurée.

![](https://docs.gitlab.com/ee/ci/jobs/img/pipeline_grouped_jobs_v14_2.png)
