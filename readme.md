# Objetivo: mysql + apache kafka + mongodb

- **Data source:** *MySQL Connector*
    - Enviar dados do MySQL para o Kafka.
- **Sink:** *MongoSink Connector*
    - Enviar dados do Kafka para o MongoDB.

---

## Tecnologias Necessárias

- Docker

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
