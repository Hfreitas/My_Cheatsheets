# MySQL

Documentação: <https://dev.mysql.com/doc/refman/8.0/en/>

## Instalando o MySQL

1. Baixe o arquivo de instalação neste link: <https://dev.mysql.com/downloads/repo/apt/>;

2. Entre como usuário root (**comando sudo -i**);

3. Navegue, via terminal, até o diretório onde foi baixado o arquivo de instalação;

4. Instale o pacote com o seguinte comando:
   apt install ./mysql-apt-config\_{versão*que_você_baixou}.deb
   ***exemplo: apt install ./mysql-apt-config_0.8.14-1_all.deb***;

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

***sudo systemctl status mysql***

## Iniciar serviço MySQL

***systemctl start mysql***

## Parar serviço MySQL

***systemctl stop mysql***

## Configurando o sistema para não iniciar o MySQL no boot

Por padrão o MySQL irá iniciar o serviço no boot da máquina, consumindo recursos mesmo quando não é necessário. Os comandos abaixo permitem alterar isto.

1. Após o boot, verifique se os serviços do MySQL estão ativos com o comando **systemctl list-unit-files '_mysql_'**;

2. Caso estejam ativos, rode o comando **sudo systemctl disable mysql**;

3. A partir de agora os serviços podem ser iniciados com os comandos
   **sudo systemctl stop mysql.service
   sudo systemctl start mysql.service**

## Comandos básicos (dentro do prompt do MySQL)

- **SHOW DATABASES;**  (visualiza as databases disponíveis);

- **USE** "database_name";  (utilizar a database selecionada);

- **SHOW TABLES;**  (visualiza as tabelas da database utilizada);

- **SHOW** "table_name";  (visualiza tabela selecionada);

- **CREATE DATABASE** "database_name"**;**  (cria database com nome designado);

- **CREATE TABLE** "table_name"**;**  (cria tabela com nome designado);

### - Obtendo informação de uma tabela

**SELECT** "informacao_desejada" <br>
**FROM** "tabela_alvo" <br>
**WHERE** "condicoes_para_recuperacao";  (este parâmetro não é obrigatório)
