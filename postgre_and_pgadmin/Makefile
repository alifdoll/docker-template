
setup:
	@make build
	@make up
	
build: 
	docker compose build

up:
	docker compose up -d

stop:
	docker compose stop

exec:
	docker exec  -it pgadmin sh

update:
	docker pull dpage/pgadmin4:latest
