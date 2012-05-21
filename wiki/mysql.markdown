Mysql
=====

Comandos Úteis
--------------

###Definindo o less como pager

    :::mysql
    pager less -SFXni

Ou então chamar o cliente mysql já passando o less como parâmetro

    :::bash
    mysql --pager='less -SFXni'

Para tornar essa opção padrão no console da própria máquina, adicionar no
arquivo ~/.my.cnf

    [client]
    pager = less -niSFX
