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
