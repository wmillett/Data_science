DC = docker compose

all: up

status:
	$(DC) ps

up:
	$(DC) up -d --build

down:
	$(DC) down

fclean:
	$(DC) down --rmi all -v --remove-orphans
	$(DC) rm -f
#Yes | $(DC) system prune -a --volumes


re: fclean all

run: all
	docker exec -it db_container bash

psql:
	$(DC) up -d --build
	docker exec -it db_container psql -U wmillett -d piscineds

import:
	@docker exec -i db_container bash -c 'cat > /docker-entrypoint-initdb.d/import.sql' < import.sql
	@docker exec db_container psql -U wmillett -d piscineds -f /docker-entrypoint-initdb.d/import.sql
	@docker exec db_container rm /docker-entrypoint-initdb.d/import.sql
	@echo "Data successfully imported to table data_2022_oct"
.PHONY: all up down fclean psql pgadmin re status import run
