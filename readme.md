objetivo

- source: mysqlconnector
    - enviar do mysql para o kafka
- mongosink connector
    - enviar do kafka para o mongo

# configurando mysql

docker exec -it fc3-kafka-connect-plugin-mysql-1 bash
mysql -uroot -p
password: root

use fullcycle;
show tables;
create table categories (id int auto_increment primary key, name varchar(255));
show tables;
desc categories;

insert into categories (name) values ('Eletronicos');

select * from categories;

acessando control-center na porta 9021
http://localhost:9021/clusters/v-Key80wQAGvUlbsDH6X8A/management/connect

control-center
acessar topico mysql-server.fullcycle.categories

insert into categories (name) values ('Cozinha');
vai aparecer uma nova message no topico

# configurando mongodb