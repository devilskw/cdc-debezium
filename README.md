# CDC DEBEZIUM WITH POSTGRESQL
A simple CDC Debezium test:
	- CDC Debezium will listen to PostgreSQL database testdb and table tb_test. After CRUD, 
the CDC will take an audit data (tb_test) and send's to kafka

Obs.: Docker compose will create the containers
	- PostgreSQL Database;
	- Kafka
	- Zoopeeker
	- CD Debezium conector, configured for PostgreSQL


# Instructions by Kazuo
- docker build . -t cdc:latest
- [AT 1st TIME] docker-compose up dbcdc
- [AT 1st TIME] cat script.sql | docker exec -i postgres-cdc psql -U "postgres" -d "testdb" -W "password@123456" 
- docker-compose down
- docker-compose up
- execute postman post method to create topic
- verify kafka topics:
	- docker exec -it kafka bash
	- kafka-topics --zookeeper zookeeper:2181 --list
		-- Confira se está aparecendo o topico criado (dbserver1.public.tb_test)
- visualize the kafka with a consumer (under kafka):
	- docker exec -it kafka sh /usr/bin/kafka-console-consumer --bootstrap-server kafka:9092 --topic dbserver1.public.tb_test --from-beginning


## Este projeto foi uma experimentação particular e bem simples, para avaliar a utilização de um CDC que realiza a leitura de uma tabela de banco de dados específica e envia ao Kafka
