CONTAINER_NAME=kkp-be

setup:
	@if [ -z "$(CONTAINER_NAME)" ]; then \
			echo "CONTAINER_NAME is empty."; \
			exit 1; \
		fi
	@make build
	@make up
	@make give-permission
	@make npm-install

start-db:
	docker compose --project-name 'mysql_and_phpmyadmin' start 


build: 
	docker compose build

up:
	docker compose up -d

stop:
	docker-compose stop

exec:
	docker exec  -it $(CONTAINER_NAME) bash

give-permission:
	docker exec $(CONTAINER_NAME) bash -c "chmod -R ugo+rw /usr/src/app/"


npm-install:
	docker exec $(CONTAINER_NAME) bash -c "npm install"

create-link:
	docker exec $(CONTAINER_NAME) bash -c "php artisan storage:link"

delete:
	@make stop
	@make delete-container
	@make delete-image

delete-container:
	docker rm $(CONTAINER_NAME)

delete-image:
	docker rmi $(CONTAINER_NAME)-laravel

stop-all:
	docker stop $$(docker ps -q)
