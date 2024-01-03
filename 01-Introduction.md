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

Connectez vous à la vm.

```
ssh admin@`YOUR-IP`` -i userX.pem
```

- IP User 1  
- IP User 2
- IP User 3
- IP User 4
- IP User 5  

user : admin

- [Installation sur debian](https://about.gitlab.com/install/#debian)
- [Next Steps](https://docs.gitlab.com/ee/install/next_steps.html)
  
