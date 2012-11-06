Mysql
=====

Comandos Úteis
--------------

###Definindo o less como pager

    :::mysql
    mysql> pager less -SFXni

Ou então chamar o cliente mysql já passando o less como parâmetro

    #!/bin/bash
    mysql --pager='less -SFXni'

Para tornar essa opção padrão no console da própria máquina, adicionar no
arquivo ~/.my.cnf

    [client]
    pager = less -niSFX

###Acompanhamento processos do mysql

    #!/bin/bash
    watch -n1 "mysql -p[password] [database] -e 'show full processlist'"

###Corrigindo Replicação
    
Se houver um erro de query na replicação do mysql, é necessário parar a
replicação e fazer o servidor que teve problema ignorar a ultima query.

    :::mysql
    STOP SLAVE;SET GLOBAL SQL_SLAVE_SKIP_COUNTER = 1; START SLAVE;

Depois disso, é necessário checar se a replicação voltou a funcionar com o
comando:

    :::mysql
    show slave status\G

###Safe Updates

o modo "safe updates" do mysql ativa uma proteção contra UPDATES ou DELETES sem
um WHERE, e limita o número de resultados retornados por um select em 1000 (ou
1 milhão para queries com várias tabelas).

para ativar o "safe update" é necessário chamar o mysql passando o parametro
--safe-updates, -U, ou "--i-am-a-dummy"

    :::!/bin/bash
    mysql --safe-updates
