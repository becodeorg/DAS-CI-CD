# Installation de Gitlab 

Connectez vous à la vm.

> Login gitlab: root:Test1234!

```
ssh azureuser@YOUR-IP -i userX.pem
```


- Maxime :
    - Gitlab Instance : http://20.13.171.42
    - Runner 1 : 20.13.167.219
    - Runner 2 : 98.71.17.199
- Karim :
    - Gitlab Instance : http://20.123.64.161 
    - Runner 1 : 20.123.65.171
    - Runner 2 : 20.13.166.86
- Arthur :
    - Gitlab Instance : http://98.71.16.171
    - Runner 1 : 98.71.16.252
    - Runner 2 : 20.13.160.111
- Sébastien :
    - Gitlab Instance : http://20.13.166.211
    - Runner 1 : 20.13.168.58
    - Runner 2 : 20.13.168.66
- Benjamin :
    - Gitlab Instance : http://20.13.168.224
    - Runner 1 : 20.13.169.28
    - Runner 2 : 52.158.40.20
- Ludo 
    - Gitlab : 20.13.147.210
    - Runner 1 : 20.123.81.139
    - Runner 2 : 20.93.21.178
    - Goat : 40.113.34.255

https://becodeorg.github.io/DAS-CI-CD/slide/

**Documentation :** 
- [Installation sur debian](https://about.gitlab.com/install/#debian)
- [Next Steps](https://docs.gitlab.com/ee/install/next_steps.html)
  


## Installation Gitlab Runner
```bash
curl -L "https://packages.gitlab.com/install/repositories/runner/gitlab-runner/script.deb.sh" | sudo bash
```

Et ensuite :  
```
sudo apt-get install gitlab-runner
```

```
sudo gitlab-runner start
```
 

Vérification du status de gitlab-runner
```
sudo gitlab-runner status
```
 
Bien mettre les droits sudo quand on register le runner.

Une fois que tout cela est fini, nous devons rajouter l'ip de gitlab dans le fichier de config de gitlab-runner
```
[runners.docker]
  extra_hosts = ["gitlab.das.becode:20.13.147.210","registry.das.becode:20.13.147.210"]
```
