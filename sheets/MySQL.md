# MySQL

[Documentação](https://dev.mysql.com/doc/refman/8.0/en/)

## Instalando o MySQL

1. Baixe o arquivo de instalação neste [link](https://dev.mysql.com/downloads/repo/apt/);

2. Entre como usuário root (**comando sudo -i**);

3. Navegue, via terminal, até o diretório onde foi baixado o arquivo de instalação;

4. Instale o pacote com o seguinte comando:
   apt install ./mysql-apt-config\_{versão\*que*você_baixou}.deb
   \*\*\_exemplo: apt install ./mysql-apt-config_0.8.14-1_all.deb*\*\*;

5. Selecione a opção **MySQL Preview Packages** e escolha a opção **Enable**.

6. Rode o comando **_apt update -y_**;

7. Rode o comando **_apt install mysql-server_**;

8. Durante a instalação, será pedido uma senha. Você não precisa preenchê-la aqui. Aperte enter no seu teclado para pular essa opção. (Senha padrão password);

9. Você receberá uma mensagem dizendo sobre a nova autenticação do MYSQL. Tecle tab e depois enter para ir para a próxima etapa;

10. Escolha a opção **Use strong Password Encryption**;

11. Saia do usuário root (comando **exit** no terminal), e execute o comando **sudo systemctl status mysql** (para verificar se o serviço mysql está ativo);

## Desinstalando o MySQL

1. Pare o serviço (comando **sudo systemctl stop mysql**);

2. Rode os comandos :

   **sudo apt-get remove --purge -s 'mysql'**

   **sudo rm -rf /etc/mysql /var/lib/mysql**

   **sudo apt-get autoremove**

   **sudo apt-get autoclean**;

## Acessar o MySQL do terminal

**mysql - u root -p** (acessa o MySql como usuário root e solicita a senha)

## Verificar status do serviço MySQL

**_sudo systemctl status mysql_**

## Iniciar serviço MySQL

**_systemctl start mysql_**

## Parar serviço MySQL

**_systemctl stop mysql_**

## Configurando o sistema para não iniciar o MySQL no boot

Por padrão o MySQL irá iniciar o serviço no boot da máquina, consumindo recursos mesmo quando não é necessário. Os comandos abaixo permitem alterar isto.

1. Após o boot, verifique se os serviços do MySQL estão ativos com o comando **systemctl list-unit-files '_mysql_'**;

2. Caso estejam ativos, rode o comando **sudo systemctl disable mysql**;

3. A partir de agora os serviços podem ser iniciados com os comandos
   **sudo systemctl stop mysql.service
   sudo systemctl start mysql.service**

### Usários e Privilégios

```sql
GRANT ALL PRIVILEGES ON base.* TO 'user'@'localhost' IDENTIFIED BY 'password';
GRANT SELECT, INSERT, DELETE ON base.* TO 'user'@'localhost' IDENTIFIED BY 'password';
REVOKE ALL PRIVILEGES ON base.* FROM 'user'@'host'; -- one permission only
REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'user'@'host'; -- all permissions
```

```sql
SET PASSWORD = PASSWORD('new_pass')
SET PASSWORD FOR 'user'@'host' = PASSWORD('new_pass')
SET PASSWORD = OLD_PASSWORD('new_pass')
```

```sql
DROP USER 'user'@'host'
```

Host ‘%’ indicates any host.

### Resetando a senha Root

```bash
/etc/init.d/mysql stop
```

```bash
mysqld_safe --skip-grant-tables
```

```bash
$ mysql # on another terminal
mysql> UPDATE mysql.user SET password=PASSWORD('new_pass') WHERE user='root';
```

```bash
## Switch back to the mysqld_safe terminal and kill the process using Control + \
$ /etc/init.d/mysql start
```

## Comandos básicos (dentro do prompt do MySQL)

### Create / Open / Delete Database

```sql
CREATE DATABASE dbNameYouWant
CREATE DATABASE dbNameYouWant CHARACTER SET utf8
USE dbNameYouWant
DROP DATABASE dbNameYouWant
ALTER DATABASE dbNameYouWant CHARACTER SET utf8
```

### Backup Database to SQL File

```bash
mysqldump -u Username -p dbNameYouWant > databasename_backup.sql
```

### Restore from backup SQL File

```bash
mysql - u Username -p dbNameYouWant < databasename_backup.sql
```

### Repair Tables After Unclean Shutdown

```bash
mysqlcheck --all-databases
mysqlcheck --all-databases --fast
```

### Browsing

```sql
SHOW DATABASES
SHOW TABLES
SHOW FIELDS FROM table / DESCRIBE table
SHOW CREATE TABLE table
SHOW PROCESSLIST
KILL process_number
```

### Select

```sql
SELECT * FROM table
SELECT * FROM table1, table2, ...
SELECT field1, field2, ... FROM table1, table2, ...
SELECT ... FROM ... WHERE condition
SELECT ... FROM ... WHERE condition GROUPBY field
SELECT ... FROM ... WHERE condition GROUPBY field HAVING condition2
SELECT ... FROM ... WHERE condition ORDER BY field1, field2
SELECT ... FROM ... WHERE condition ORDER BY field1, field2 DESC
SELECT ... FROM ... WHERE condition LIMIT 10
SELECT DISTINCT field1 FROM ...
SELECT DISTINCT field1, field2 FROM ...
```

### Select - Join

```sql
SELECT ... FROM t1 JOIN t2 ON t1.id1 = t2.id2 WHERE condition
SELECT ... FROM t1 LEFT JOIN t2 ON t1.id1 = t2.id2 WHERE condition
SELECT ... FROM t1 JOIN (t2 JOIN t3 ON ...) ON ...
```

### Conditions

```sql
field1 = value1
field1 <> value1
field1 LIKE 'value _ %'
field1 IS NULL
field1 IS NOT NULL
field1 IS IN (value1, value2)
field1 IS NOT IN (value1, value2)
condition1 AND condition2
condition1 OR condition2
```

### Insert

```sql
INSERT INTO table1 (field1, field2, ...) VALUES (value1, value2, ...)
```

### Delete

```sql
DELETE FROM table1 / TRUNCATE table1
DELETE FROM table1 WHERE condition
DELETE FROM table1, table2 FROM table1, table2 WHERE table1.id1 =
  table2.id2 AND condition
```

### Update

```sql
UPDATE table1 SET field1=new_value1 WHERE condition
UPDATE table1, table2 SET field1=new_value1, field2=new_value2, ... WHERE
  table1.id1 = table2.id2 AND condition
```

### Create / Delete / Modify Table

#### Create

```sql
CREATE TABLE table (field1 type1, field2 type2, ...)
CREATE TABLE table (field1 type1, field2 type2, ..., INDEX (field))
CREATE TABLE table (field1 type1, field2 type2, ..., PRIMARY KEY (field1))
CREATE TABLE table (field1 type1, field2 type2, ..., PRIMARY KEY (field1,
field2))
```

```sql
CREATE TABLE table1 (fk_field1 type1, field2 type2, ...,
  FOREIGN KEY (fk_field1) REFERENCES table2 (t2_fieldA))
    [ON UPDATE|ON DELETE] [CASCADE|SET NULL]
```

```sql
CREATE TABLE table1 (fk_field1 type1, fk_field2 type2, ...,
 FOREIGN KEY (fk_field1, fk_field2) REFERENCES table2 (t2_fieldA, t2_fieldB))
```

```sql
CREATE TABLE table IF NOT EXISTS (...)
```

```sql
CREATE TEMPORARY TABLE table (...)
```

#### Drop

```sql
DROP TABLE table
DROP TABLE IF EXISTS table
DROP TABLE table1, table2, ...
```

#### Alter

```sql
ALTER TABLE table MODIFY field1 type1
ALTER TABLE table MODIFY field1 type1 NOT NULL ...
ALTER TABLE table CHANGE old_name_field1 new_name_field1 type1
ALTER TABLE table CHANGE old_name_field1 new_name_field1 type1 NOT NULL ...
ALTER TABLE table ALTER field1 SET DEFAULT ...
ALTER TABLE table ALTER field1 DROP DEFAULT
ALTER TABLE table ADD new_name_field1 type1
ALTER TABLE table ADD new_name_field1 type1 FIRST
ALTER TABLE table ADD new_name_field1 type1 AFTER another_field
ALTER TABLE table DROP field1
ALTER TABLE table ADD INDEX (field);
```

#### Change field order

```sql
ALTER TABLE table MODIFY field1 type1 FIRST
ALTER TABLE table MODIFY field1 type1 AFTER another_field
ALTER TABLE table CHANGE old_name_field1 new_name_field1 type1 FIRST
ALTER TABLE table CHANGE old_name_field1 new_name_field1 type1 AFTER
  another_field
```

### Keys

```sql
CREATE TABLE table (..., PRIMARY KEY (field1, field2))
CREATE TABLE table (..., FOREIGN KEY (field1, field2) REFERENCES table2
(t2_field1, t2_field2))
```
