# Premier projet et création du premier runner
---
## Le premier projet

Création d'un projet
![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/325601b4-65e1-4639-9613-c75d029671e6)

---

On remplit les détails du projet tels que le nom, la description, et d'autres paramètres pertinents 
et on choisit la visibilité du projet en fonction des besoins, que ce soit "Public", "Internal", ou "Private".

![image](https://github.com/becodeorg/DAS-CI-CD/assets/26960886/cb08a517-9223-4d92-b26e-b9ddbac0d9be)
---
## Les pipelines, jobs et stages
---
### Job 
Un "job" représente une tâche individuelle à accomplir dans le cadre du processus CI/CD. 

```
say_hello:
  script:
    - echo "Hello DAS!"
```

---
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

---
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
---
![](https://docs.gitlab.com/ee/ci/jobs/img/pipeline_grouped_jobs_v14_2.png)
---

## Création du premier runner

Les runners sont des sous-processus qui vont se charger de faire les commandes (scripts) que vous avez définies dans votre gitlab-ci. Gitlab-CI est capable de fonctionner de différente manière :

- SSH
- Shell
- Parallels
- VirtualBox
- Docker
- Docker Machine (auto-scaling)
- Kubernetes
- Custom


---

## Comment choisir ?

- **Shell**  
  C'est le plus simple de tous. Vos scripts seront lancés sur la machine qui possède le Runner.
- **Parallels, VirtualBox**   
  Le Runner va créer (ou utiliser) une machine virtuelle pour exécuter les scripts. Pratique pour avoir un environnement spécifique (exemple macOS)
- **Docker**  
  Utilise Docker pour créer / exécuter vos scripts et traitement (en fonction de la configuration de votre .gitlab-ci.yml)
- **Docker Machine (auto-scaling)**  
  Identique à docker, mais dans un environnement Docker multimachine avec auto-scaling.
- **Kubernetes**  
  Lance vos builds dans un cluster Kubernetes. Très similaire à Docker-Machine
- **SSH**  
  À ne pas utiliser. Il existe, car il permet à Gitlab-CI de gérer l'ensemble des configurations possibles.

---

## Création du fichier ``.gitlab-ci.yaml``   
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

---

- Pour créer un runner, il faut aller dans l'onglet ``settings`` dans le menu à gauche et on étend la rubrique ``Runners``
- On choisit le runner pour Linux. Il faut également y indiquer un tag, mais on verra plus tard comment l'utiliser.
- Enregistrer le runner (en sudo).

````
sudo gitlab-runner register  --url http://34.243.1.181  --token glrt-xkoyTMSpyfEsk6-DPYLS
````

et pour vérifier que le runner a bien été créer : 

```
sudo cat /etc/gitlab-runner/config.toml
```
---



---

## Différence entre User-mode et system-mode
**Mode Utilisateur (User Mode) :**  
- Portée : Le runner est spécifique à l'utilisateur qui l'a enregistré. Il ne sera accessible que pour cet utilisateur.
- Permissions : Le runner aura les mêmes permissions que l'utilisateur qui l'a enregistré. Cela signifie qu'il peut accéder aux ressources et aux privilèges de cet utilisateur.

**Mode Système (System Mode) :**  
- Portée : Le runner est disponible pour tous les utilisateurs du système.
- Permissions : Le runner aura généralement besoin de permissions élevées, car il peut être utilisé par n'importe quel utilisateur du système. Cela signifie qu'il peut accéder à des ressources qui nécessitent des privilèges élevés.

---

### Avantages et inconvénients :
**Mode Utilisateur :**  
- Avantages : Isolation des ressources par utilisateur. Chaque utilisateur peut avoir son propre runner avec des configurations spécifiques.
- Inconvénients : Limité à un seul utilisateur. Si plusieurs utilisateurs ont besoin d'utiliser le runner, chaque utilisateur devra enregistrer son propre runner.

**Mode Système :**  
- Avantages : Disponible pour tous les utilisateurs, ce qui peut être pratique dans certains scénarios. Un seul runner peut être utilisé par tous les utilisateurs.
- Inconvénients : Requiert généralement des privilèges élevés, ce qui peut représenter un risque de sécurité. Toutes les configurations seront partagées entre les utilisateurs et les tâches doivent être exécutées manuellement à l'aide de ``gitlab-runner run``

---

## Les tags 

---

- Pour que le précédent runner puisse fonctionner, nous avons coché la case ``Run untagged jobs``. 
- Pour gérer efficacement les runners, il est préférable d'utiliser les tags afin de les réutiliser tant que possible. 
- Si l'on teste en décochant la case, les runners resteront avec le statut pending. 
- Si l'on modifie  le fichier ```gitlab-ci.yaml```, et que l'on rajoute un tag, on peut voir que seul le job qui a un tag sera lancé.

---

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
---

## Les runners partagés
Par défaut, les runners sont 'locked' lorsque qu'il est utilisé par un autre projet.
![](https://media.discordapp.net/attachments/727923649738178571/1199291526434529280/image.png)

Si l'on veut que le runner soit utilisé par plusieurs projet, il faut décocher la case. 

Ensuite, il faut activer le runner dans les paramètres CI//CD du dépot.
![](https://cdn.discordapp.com/attachments/727923649738178571/1199293028712591380/image.png?ex=65c203ab&is=65af8eab&hm=d60cbe135dcd2ca6069a57193246049de02313f1623ee1619e3b9e729088b8a8&)

---

## Exercice
- Créer 2 runners **partagés**. 
- L'un éxecutera du code shell et aura comme tag ``shell``
- L'autre éxécutera un container docker et aura comme tag ``docker``




