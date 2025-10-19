CONTAINER_NAME=
SERVICE_NAME= *sesuaikan di docker-compose

setup:
	@if [ -z "$(CONTAINER_NAME)" ]; then \
			echo "CONTAINER_NAME is empty."; \
			exit 1; \
		fi
	echo "Make Sure .env file exists"
	@make build
	@make up
	@make give-permission
	@make composer-install
	@make create-link

start-db:
	docker compose --project-name 'postgre_and_pgadmin' start && \
	docker compose --project-name 'mysql_and_phpmyadmin' stop


build: 
	docker compose build

up:
	docker compose up -d

stop:
	docker-compose stop

exec:
	docker exec  -it $(CONTAINER_NAME) bash

give-permission:
	docker exec $(CONTAINER_NAME) bash -c 	"chmod -R ugo+rw /var/www/html/ || chmod 777 -R /var/www/html/" && \
	docker exec $(CONTAINER_NAME) bash -c  	"chmod -R 777 storage" && \
	docker exec $(CONTAINER_NAME) bash -c  	"chmod -R 777 /var/www/html/" && \
	docker exec $(CONTAINER_NAME) bash -c  	"chown -R www-data:www-data storage"


composer-install:
	docker exec $(CONTAINER_NAME) bash -c "composer install --no-plugins --no-interaction"

create-link:
	docker exec $(CONTAINER_NAME) bash -c "php artisan storage:link"

delete:
	@make stop
	@make delete-container
	@make delete-image
	@make delete-volume

delete-container:
	docker rm -f $(CONTAINER_NAME) || true

delete-image:
	docker rmi -f $(CONTAINER_NAME)-$(SERVICE_NAME) || true

delete-volume:
	docker volume prune -f