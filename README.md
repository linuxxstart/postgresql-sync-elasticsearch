# Sincronizar PostgreSQL com Elasticsearch via Debezium

### Esquema

![postgresql_sync_elastic](/imagens/postgresql_sync_elastic.png)


Estamos usando o Docker Compose para implementar os seguintes componentes:

* PostgreSQL - Pré-requisito para usar um postgres externo 
  * [pgoutput](https://debezium.io/documentation/reference/connectors/postgresql.html#postgresql-pgoutput) A partir da versão 10 do postgres o debezium consegue usar a replicação logica sem necessidade de adicionar plugins. Baste declarar no conector o nome do plugin: "plugin.name": "pgoutput"
  ![syn_09](/imagens/sync_09.png)
  * [postgresql](https://debezium.io/documentation/reference/connectors/postgresql.html#postgresql-server-configuration),[permissões de usuários](https://debezium.io/documentation/reference/connectors/postgresql.html#postgresql-permissions), [permissoões de replicação](https://debezium.io/documentation/reference/connectors/postgresql.html#postgresql-host-replication-permissions)
  * [decoderbufs](https://github.com/debezium/postgres-decoderbufs)
  * [wal2json](https://github.com/eulerto/wal2json)


* Kafka
  * ZooKeeper
  * Kafka Broker
  * Kafka Connect with [Debezium](http://debezium.io/) and [Elasticsearch](https://github.com/confluentinc/kafka-connect-elasticsearch) Connectors
* [Avro Serialization](https://debezium.io/documentation/reference/1.6/configuration/avro.html)
* Elasticsearch

Imagens docker do debezium 1.6 estavéis na criação do projeto e o uso de Dockerfile para gerar a imagen do debezium connector com o plugin do ElasticsearchSinkConnector 11.1.0.


### Subindo containers

```shell
docker-compose up --build -d

```
### Adicionando os conectores

```shell
# aguarde os serviços estarem no ar e criar primeiro o conector do postgres(source).

curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @reqs/connections/source.json
```

### Verificar se os topics foram criados no kafka

Acesse localhost:9000, devemos ter os topics criados e com as configurações da segunda imagem.

![topics_kafka_01](/imagens/topics_kafka_01.png)
![topics_kafka_02](/imagens/topics_kafka_02.png)

### Criando os conectores de sync com o elasticsearch
```shell
./start.sh
```
Caso o elasticsearch tenho usuário e senha, add os parâmetros abaixo:
```shell
"connection.username": "usuario",
"connection.password": "senha",
```

### Testando

```shell
# Verifique o conteúdo do PostgreSQL database:
docker-compose exec postgres bash -c 'psql -U $POSTGRES_USER $POSTGRES_DATABASE -c "SELECT * FROM users"'

# Verifique o conteúdo do Elasticsearch database:
curl http://localhost:9200/users/_search?pretty
```

### Criando usuário

```shell
docker-compose exec postgres bash -c 'psql -U $POSTGRES_USER $POSTGRES_DATABASE'
test_db=# INSERT INTO users (email) VALUES ('apple@gmail.com');

# Verifique o conteúdo do Elasticsearch database:
curl http://localhost:9200/users/_search?q=id:6
```

```json
{
  ...
  "hits": {
    "total": 1,
    "max_score": 1.0,
    "hits": [
      {
        "_index": "users",
        "_type": "_doc",
        "_id": "6",
        "_score": 1.0,
        "_source": {
          "id": 6,
          "email": "apple@gmail.com"
        }
      }
    ]
  }
}
```

### Atualizando usuário

```shell
test_db=# UPDATE users SET email = 'tesla@gmail.com' WHERE id = 6;

# Verifique o conteúdo do Elasticsearch database:
curl http://localhost:9200/users/_search?q=id:6
```

```json
{
  ...
  "hits": {
    "total": 1,
    "max_score": 1.0,
    "hits": [
      {
        "_index": "users",
        "_type": "_doc",
        "_id": "6",
        "_score": 1.0,
        "_source": {
          "id": 6,
          "email": "tesla@gmail.com"
        }
      }
    ]
  }
}
```

### Deletando usuário

```shell
test_db=# DELETE FROM users WHERE id = 6;

# Verifique o conteúdo do Elasticsearch database:
curl http://localhost:9200/users/_search?q=id:6
```

```json
{
  ...
  "hits": {
    "total": 1,
    "max_score": 1.0,
    "hits": []
  }
}
```

### Comando úteis 


Verificar os plugins:
```shell
curl http://localhost:8083/connector-plugins -s | jq
```
Verificar os conectores:
```shell
curl http://localhost:8083/connectors -s | jq
```
Verificar a conexão com as bases:
```shell
curl http://localhost:8083/connectors/test_db-connector/status -s | jq
```
Deletar conector kafka:
```shell
curl -X DELETE http://localhost:8083/connectors/nomedoconector
```

### Criando index pattern no Kibana

![kibana_01](/imagens/kibana_01.png)
![kibana_02](/imagens/kibana_02.png)
![kibana_03](/imagens/kibana_03.png)
![kibana_04](/imagens/kibana_04.png)
![kibana_05](/imagens/kibana_05.png)


### Edição e criação do projeto com base:

https://github.com/YegorZaremba/sync-postgresql-with-elasticsearch-example