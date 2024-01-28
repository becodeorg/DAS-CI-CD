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

