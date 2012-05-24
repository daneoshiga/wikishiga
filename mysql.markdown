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
    watch -n1 "mysql -ppassw0rd mya2billing -e 'show full processlist'"