Debugging
=========

##Erro 500 Internal Server Error##

Há um erro de sintaxe no PHP, para verificar o erro se pode:  
Verificar o arquivo var/log/httpd/error\_log (se tiver ssl ativado, é ssl\_error\_log).


###Ativar o display\_errors e error\_logging.

    :::php
    <?php
    error_reporting(E_ALL);
    ini_set('display_errors','1');
    ?>
