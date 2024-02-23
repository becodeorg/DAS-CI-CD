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

Bon à savoir, il n'est pas obligatoire d'avoir des stages pour déclencher des jobs.
Depuis quelques temps, gitlab permet de faire de "Stageless". 

### Pipeline
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
Création du fichier ``.gitlab-ci.yaml``   
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

On choisit le runner pour Linux. Il faut également y indiquer un tag, mais on verra plus tard comment l'utiliser.
![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/104c579e-45fe-4b70-8ee4-ae34f47feeb5)

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/beaba3cc-c4c3-4de4-a1ee-78e4705f387f)

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/b4300593-4a68-48d5-bc03-ede4f9e0d661)

Maintenant, on va pouvoir enregistrer le runner (en sudo). 
![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/a4773056-007a-4e89-b677-905ba71967f3)

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/18a44719-3e1c-4027-bf43-1bcd930e89c6)

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/e96ef94a-02c9-4774-99e1-5cb789085572)

````
sudo gitlab-runner register  --url http://34.243.1.181  --token glrt-xkoyTMSpyfEsk6-DPYLS
````

et pour vérifier que le runner a bien été créer : 

```
sudo cat /etc/gitlab-runner/config.toml
```
Différence entre User-mode et system-mode
Dans user mode, les runners que vous inscrivez ne fonctionneront que pour l'utilisateur actuel. Si vous vous connectez depuis un autre utilisateur, les exécuteurs ne seront pas disponibles pour votre pipeline et si vous essayez d'exécuter votre pipeline, cela sera  bloqué du fait qu'il n'y a aucun exécuteur disponible pour fonctionner.

Dans system mode, les coureurs que vous inscrivez seront disponibles pour courir et travailler tant que la machine est allumée, quel que soit l'utilisateur à partir duquel vous vous connectez.

## Les tags 
Pour que le précédent runner puisse fonctionner, nous avons coché la case ``Run untagged jobs``. 
Pour gérer efficacement les runners, il est préférable d'utiliser les tags afin de les réutiliser tant que possible.
Si l'on teste en décochant la case, les runners resteront avec le statut pending. 
![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/4ab591a6-da87-4dae-ad7f-eb2c00107033)

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/aca186a2-d9ff-4c6b-96be-ce98c43987df)

Si l'on modifie  le fichier ```gitlab-ci.yaml```, et que l'on rajoute un tag, on peut voir que seul le job qui a un tag sera lancé.

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/58540f96-5c4c-44e6-a2ae-d83dfd065614)

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/20a0699d-e3e1-4dcd-a8ca-10018abe4f86)

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/2728c1b7-8f80-40b3-915b-470e444bb841)

## Runner docker

> Gitlab > settings > CI/CD > Runners

Specific/Shared runners

- Doc : https://docs.gitlab.com/runner/install/index.html
- Linux : https://docs.gitlab.com/runner/install/linux-manually.html

Note : dns vers l'instance gitlab

### Image Gitlab-runner
```
mkdir -p /data/
docker run -d  \
   --name gitlab-runner \
   --restart always \
   -v /var/run/docker.sock:/var/run/docker.sock \
   -v /data/gitlab-runner:/etc/gitlab-runner \
   gitlab/gitlab-runner:latest
```

Et ensuite on lance le register 
```
docker exec -it gitlab-runner gitlab-runner register --url http://34.243.1.181  --token glrt-ys
3N4ndE_h6eN47DmurZ
```
Edition du fichier .gitlab-ci.yaml
```yaml
stages:          # List of stages for jobs, and their order of execution
  - test

hello-job:      # This job runs in the deploy stage.
  stage: test  # It only runs when *both* jobs in the test stage complete successfully.
  image: debian:latest
  tags: 
    - docker
  script:
    - echo "Start..."
    - echo "*****************************************************************"
    - echo "-----------------------------------------------------------------"
    - sleep 30
    - echo "Application successfully deployed."

```

## Les runners partagés
Par défaut, les runners sont 'locked' lorsque qu'il est utilisé par un autre projet.
![](https://media.discordapp.net/attachments/727923649738178571/1199291526434529280/image.png)

Si l'on veut que le runner soit utilisé par plusieurs projet, il faut décocher la case. 

Ensuite, il faut activer le runner dans les paramètres CI//CD du dépot.
![](https://cdn.discordapp.com/attachments/727923649738178571/1199293028712591380/image.png?ex=65c203ab&is=65af8eab&hm=d60cbe135dcd2ca6069a57193246049de02313f1623ee1619e3b9e729088b8a8&)



