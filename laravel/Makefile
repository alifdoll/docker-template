CONTAINER_NAME=

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


build: 
	docker compose build

up:
	docker compose up -d

stop:
	docker-compose stop

exec:
	docker exec  -it$(CONTAINER_NAME) bash

give-permission:
	docker exec $(CONTAINER_NAME) bash -c "chmod -R ugo+rw /var/www/html/ || chmod 775 -R /var/www/html/"


composer-install:
	docker exec $(CONTAINER_NAME) bash -c "composer install --no-plugins --no-interaction"


delete:
	@make stop
	@make delete-container
	@make delete-image

delete-container:
	docker rm $(CONTAINER_NAME)

delete-image:
	docker rmi $(CONTAINER_NAME)-laravel