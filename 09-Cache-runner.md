# Cache
Le cache des runners dans GitLab CI/CD est un mécanisme qui permet de stocker 
et de réutiliser des fichiers ou des répertoires entre différentes exécutions 
de jobs sur le même runner.  

Cela permet d'améliorer les performances des pipelines en évitant la répétition 
de certaines tâches, comme la compilation de dépendances ou le téléchargement de bibliothèques (comme npm). 

```yaml
cache:
  key: my_cache_key
  paths:
    - .lib/
    - node_modules/
    - vendor/
stages:
  - stage1
  - stage2
job1:
    stage: stage1
    script: 
      - mkdir -p .lib
      - echo "Ceci est le cache partagé" > .lib/das.txt
    tags:
      - docker
job2:
    stage: stage2
    script:
        - cat .lib/das.txt
    tags:
      - docker

```
Mais si on y ajoute une règle pour que le job1 ne s'éxécute que sur la branche main, alors le job ne poourra que s'éxuter que si le fichier ``das.txt`` se trouve dans le cache. 
Si le cache n'est plus présent, le button Build>Pipelines>Clear runner caches  permet de l'éffacer, cela générera une erreur car il ne trouvera pas le fichier. 

```yaml
cache:
  key: my_cache_key
  paths:
    - .lib/
    - node_modules/
    - vendor/
stages:
  - stage1
  - stage2
job1:
    stage: stage1
    script: 
      - mkdir -p .lib
      - echo "Ceci est le cache partagé" > .lib/das.txt
    rules:
      - if: '$CI_COMMIT_BRANCH == "main"'
    tags:
      - docker
job2:
    stage: stage2
    script:
        - cat .lib/das.txt
    tags:
      - docker
```

Le cache se vide aussi lorsque la key change. SI on utrilise une variable comme key, un nouveau cache sera utiliser à chaque fois que le noom de la key change.

```yaml
cache:
  - key: $CI_COMMIT_REF_SLUG
```

Exemple 
```yaml
cache:
  - key: $CI_COMMIT_REF_SLUG
    paths:
      - .lib
stages:
  - step1
  - step2
j1:
  stage: step1
  script:
    - mkdir -p .lib 
    - echo $CI_COMMIT_REF_SLUG > .lib/$CI_COMMIT_REF_SLUG.txt
  tags:
    - docker
j2:
  stage: step2
  script: 
    - cat .lib/$CI_COMMIT_REF_SLUG.txt
    - ls .lib/
  tags:
    - docker
```

## Cache par Politique de Versions (cache:policy) :

La directive policy permet de spécifier une politique de cache, qui définit comment les caches doivent être gérés lors des différentes étapes du pipeline. Il existe trois valeurs possibles, pull, push et les deux combinés pull-push

- pull : Indique que le cache doit être téléchargé depuis un cache partagé ou distant avant l'exécution du job.
- push : Indique que le cache doit être poussé (enregistré) après l'exécution du job pour être utilisé par d'autres jobs ou pipelines.
- pull-push : fait les deux; c'est le mode par défaut


```yaml
stages:
  - step1
  - step2
j1-1:
  stage: step1
  script:
    - mkdir -p .lib 
    - echo $CI_COMMIT_REF_SLUG-$CI_JOB_STAGE > .lib/$CI_COMMIT_REF_SLUG-$CI_JOB_STAGE.txt
  cache:
    - key: $CI_JOB_STAGE-$CI_COMMIT_REF_SLUG
      paths:
        - .lib
      policy: pull
  tags:
    - docker
j1-2:
  stage: step1
  script:
    - cat .lib/$CI_COMMIT_REF_SLUG-$CI_JOB_STAGE.txt
    - ls .lib/
  cache:
    - key: $CI_JOB_STAGE-$CI_COMMIT_REF_SLUG
      paths:
        - .lib
  tags:
    - docker
```

Comme on a fait que un pull, il n'a pas mise à jour le cache et du coup il est indisponnible pour le second job.
Editons le fichier et mettons le polycy avec la valeur push 

```yaml
stages:
  - step1
  - step2
j1-1:
  stage: step1
  script:
    - mkdir -p .lib 
    - echo $CI_COMMIT_REF_SLUG-$CI_JOB_STAGE > .lib/$CI_COMMIT_REF_SLUG-$CI_JOB_STAGE.txt
  cache:
    - key: $CI_JOB_STAGE-$CI_COMMIT_REF_SLUG
      paths:
        - .lib
      policy: push
  tags:
    - docker
j1-2:
  stage: step1
  script:
    - cat .lib/$CI_COMMIT_REF_SLUG-$CI_JOB_STAGE.txt
    - ls .lib/
  cache:
    - key: $CI_JOB_STAGE-$CI_COMMIT_REF_SLUG
      paths:
        - .lib
  tags:
    - docker
```
