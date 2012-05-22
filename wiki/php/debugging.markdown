Debugging
=========

###Erro 500 Internal Server Error###

Há um erro de sintaxe no PHP, para verificar o erro se pode:

1. verificar o arquivo var/log/httpd/error\_log (se tiver ssl ativado, é ssl\_error\_log).
2. ativar o display\_errors e error\_logging.
  

    :::php
    <?php
    error_reporting(E_ALL);
    ini_set('display_errors', '1');
    ?>
