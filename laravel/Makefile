CONTAINER_NAME=sellerpro_toolbox_v2

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

docker-exec:
	docker exec $(CONTAINER_NAME) bash

give-permission:
	docker exec $(CONTAINER_NAME) bash -c "chmod -R ugo+rw /var/www/html/ || chmod 775 -R /var/www/html/"


composer-install:
	docker exec $(CONTAINER_NAME) bash -c "composer install --no-plugins --no-interaction"