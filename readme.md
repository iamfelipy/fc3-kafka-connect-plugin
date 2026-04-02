# Testar integrações do Kafka Connect com data source, sink, converters e transformers

## Tecnologias utilizadas
- MySQL
- Apache Kafka
- Kafka Connect
- MongoDB

## Integrações configuradas

- **Data Source:** MySQL Connector (`mysql-connector`)
    - Conector: `io.debezium.connector.mysql.MySqlConnector`
    - Converter (padrão Debezium): `org.apache.kafka.connect.json.JsonConverter`
    - Transforma dados do MySQL em eventos Kafka
- **Sink:** MongoDB Sink Connector (`mongo-sink-from-mysql`)
    - Conector: `com.mongodb.kafka.connect.MongoSinkConnector`
    - Converter (padrão MongoDB Sink): `org.apache.kafka.connect.json.JsonConverter`
    - Transformer: `org.apache.kafka.connect.transforms.ExtractField$Value` (campo: `after`)
    - Consome eventos do Kafka e grava no MongoDB

- **Data source:** *MySQL Connector*
    - Enviar dados do MySQL para o Kafka.
- **Sink:** *MongoSink Connector*
    - Enviar dados do Kafka para o MongoDB.

---

## Tecnologias Necessárias

- Docker

---

## Subindo o ambiente com Docker Compose

Execute o comando abaixo na raiz do projeto para iniciar todos os serviços:

```bash
docker compose up -d
```

Aguarde alguns instantes para garantir que todos os containers estejam em execução antes de seguir para as configurações dos connectors.

---

## Importando as Configurações dos Connectors

Acesse o Control Center em:

```
http://localhost:9021/clusters/v-Key80wQAGvUlbsDH6X8A/management/connect
```

---

## Configurando o MySQL

Acesse o container do MySQL e entre no cliente MySQL:

```bash
docker exec -it fc3-kafka-connect-plugin-mysql-1 bash
mysql -uroot -p
# senha: root
```

Dentro do MySQL, execute:

```sql
USE fullcycle;
SHOW TABLES;
CREATE TABLE categories (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(255)
);
SHOW TABLES;
DESC categories;

INSERT INTO categories (name) VALUES ('Eletronicos');
SELECT * FROM categories;
```

---

## Acessando o Control Center

Abra no navegador:

```
http://localhost:9021/clusters/v-Key80wQAGvUlbsDH6X8A/management/connect
```

Verifique o tópico `"mysql-server.fullcycle.categories"` no Control Center.

---

## Configurando o MongoDB

Insira mais dados via MySQL para testar o fluxo:

```sql
INSERT INTO categories (name) VALUES ('Cozinha');
```

---

## Fluxo da Mensagem

```
client -> MySQL -> Kafka -> MongoDB
```

---

## Acessando o Mongo Express

Acesse a coleção `fullcycle` via Mongo Express:

```
http://localhost:8085/
```
