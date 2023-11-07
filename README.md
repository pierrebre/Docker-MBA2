# Exo Docker

## Paramétrage des images et du container : 

- docker build -t prevention .
- docker compose up --build
- docker exec prevention-app php artisan migrate
- docker exec prevention-app php artisan create:all

## Ports :
- app : 8081
- db : 3306
- adminer : 8087 

### Note : 
Pour une raison que j'ignore pour l'instant, en faisant un npm run build, la compilation va marcher pour les fichiers css mais non pour les fichiers typescript. Je n'ai pas eu le temps de trouver l'origine du problème. J'ai dont dû les exclure du front pour que l'app fonctionne.