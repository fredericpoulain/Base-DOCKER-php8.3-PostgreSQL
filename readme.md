# Environnement PHP 8.3 / Postgresql / Mailcatcher in Docker



### Si les images ne sont pas encore créés : 
```bash
docker-compose build 
docker-compose up -d
```

#### OU
```bash
docker-compose up --build -d
```

### Si les images sont déjà créé :
#### Et qu'aucunes modifications n'ont été apportées aux fichiers de configuration
```bash
docker-compose up -d
```
## Entrer dans le container :
#### Attention ! Modifier "customNameProject" par le nom du container modifié précédemment
```bash
docker exec -ti Project_name bash
```
### Installer le projet Symfony :

`composer create-project symfony/skeleton:"7.0.*" project`   
`cd project`  
`composer require webapp`  


### À la racine de l'environnement Docker exécuter cette commande (linux)
Cela permettra d'avoir les droits sur tout le contenu du dossier "project".
```bash
sudo chown -R $USER ./
```
## Accès

L'application :
http://127.0.0.1:8000/   
pgAdmin4 : http://127.0.0.1:8080/  
MailCatcher :http://127.0.0.1:1080/ 



## Configuration du DATABASE_URL dans fichier .env.local :
#### Remplacer <...> par les bonnes valeurs
`DATABASE_URL="postgresql://postgres:<POSTGRES_PASSWORD>@<POSTGRES_SERVICE_NAME>:5432/<DB_NAME>?serverVersion=<VERSION_POSTGRES>&charset=utf8"`


## Configuration du MAILER_DSN dans fichier .env.local :
`MAILER_DSN=smtp://mailcatcher:1025`



## Commandes utiles :

### Construire et démarrer tous les services définis dans votre fichier docker-compose.yml.
###### NOTE: à utiliser si modifications des fichiers Dockerfile ou docker-compose.yml :

```bash
docker-compose up --build -d
```

### Ouvre un shell interactif à l'intérieur du conteneur Docker nommé «php» :

```bash
docker exec -ti Project_name bash
```

### Arrêter et redémarrer tous les conteneurs en cours d'exécution :
```bash
docker-compose down
```


### Démarrer des conteneurs Docker en arrière-plan :

```bash
docker-compose up -d
```


### Pour supprimer toutes les images Docker en une seule fois sans spécifier le nom ou l'ID de chaque image

```bash
docker rmi $(docker images -q) --force
```
### Arrête et supprimer non seulement les conteneurs, mais aussi les volumes
#### Permet de prendre en compte les modifications du docker-compose sur la base de donnée
#### **Attention** : L’utilisation de --volumes supprimera toutes les données stockées dans les volumes Docker du projet, ce qui est irréversible.
`docker-compose down --volumes`