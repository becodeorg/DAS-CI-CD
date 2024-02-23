# Les Variables

# Les Différents Types de Variables dans GitLab

##  Variables d'Environnement
Les variables d'environnement sont les plus courantes dans GitLab CI/CD. Elles servent à stocker des données qui peuvent être utilisées par les scripts des jobs. Par exemple, vous pouvez définir une variable DATABASE_URL pour stocker l'URL de votre base de données. Ces variables sont accessibles dans les scripts de pipeline en utilisant la syntaxe standard des variables d'environnement, comme $DATABASE_URL dans un script shell.

## Variables Protégées
Les variables protégées sont d'utiles pour stocker des données sensibles qui ne doivent être utilisées que dans un environnement de production ou un environnement similaire sécurisé. Par exemple, vous pouvez avoir une clé API qui ne doit être utilisée que lors du déploiement en production.

## Variables Masquées
Les variables masquées sont une fonctionnalité de sécurité qui empêche la valeur de la variable d'être affichée dans les logs de GitLab. C'est particulièrement important pour les secrets, comme les mots de passe ou les clés API. Lorsqu'une variable est masquée, sa valeur est remplacée par des astérisques dans les logs d'exécution de pipeline.

```
job_example:
  script:
    - echo $MY_MASKED_VARIABLE  # Cette variable est protégée et ne sera pas visible dans les logs
    - echo $MY_PROTECTED_VARIABLE  # Cette variable sera visible dans les logs
  tags:
    - docker
```

<br>

## Les variables predéfinies
Les variables prédéfinies dans GitLab CI/CD sont des variables automatiquement définies par le système et mises à la disposition de vos jobs lors de l'exécution d'un pipeline. 

1. Variables relatives au pipeline :
	- $CI_PIPELINE_ID: L'ID unique du pipeline.
	- $CI_PIPELINE_IID: L'ID interne du pipeline.
	- $CI_COMMIT_REF_NAME: Le nom de la branche ou de l'étiquette en cours.
	- $CI_COMMIT_REF_PROTECTED: Indique si la branche ou l'étiquette est protégée.
2. Variables relatives au commit associé :
	- $CI_COMMIT_SHA: Le SHA-1 du commit associé au pipeline.
	- $CI_COMMIT_SHORT_SHA: La version courte (7 premiers caractères) du SHA-1 du commit.
	- $CI_COMMIT_BRANCH: Le nom de la branche du commit associé.
	- $CI_COMMIT_TAG: Le nom de l'étiquette si le commit est associé à une étiquette


* liste : https://docs.gitlab.com/ee/ci/variables/predefined_variables.html

Exemple : 
* sans stage (juste des jobs)
```
start-job: 
  tags:
    - shell     
  script:
    - echo "Start..."
    - echo "$CI_JOB_ID"
end-job:
  tags:
    - shell     
  script:
    - echo "ended !!"  
```

## Les variables globales

```
variables:
  GLOBAL_VAR: "Hello"
start-job: 
  tags:
    - shell     
  script:
    - echo "Start..."
    - echo "$GLOBAL_VAR"
    - echo "ended !!"
```

## Les Variables locales (à un job)

```
variables:
  GLOBAL_VAR: "Hello"
start-job: 
  tags:
    - shell
  variables:
    LOCAL_VAR: "Hello DAS !!" 
  script:
    - echo "Start..."
    - echo "$LOCAL_VAR"
    - echo "ended !!"
```

## Les Variables local vs global

```
variables:
  VAR: "Hello"
start-job: 
  tags:
    - shell
  variables:
    VAR: "Hello DAS !!" 
  script:
    - echo "Start..."
    - echo "$VAR"
    - echo "ended !!"
```

## Les Variables GROUP 

* group > settings > CICD > Variables

