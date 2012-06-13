Substituições
=============

Lista de substituições no vim
-----------------------------

Casos de uso de substituições no vim:

###Substituir "SP 16" por "16,SP" em todo o arquivo

    :::vim
    :%s/^\(.*\)\s\(\d\+\)/\2,\1/gi
