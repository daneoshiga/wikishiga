Linux
=====

Comandos Úteis
--------------

###Descobrir Charset do arquivo###
    
    #!/bin/bash
    file -i [nome-arquivo]

###Atualizar pacote###

    #!/bin/bash
    yum update [nome-pacote]

###Descobrir pid do processo###

    #!/bin/bash
    ps aux | grep [nome-processo]

### Reiniciar o apache###

    #!/bin/bash
    service httpd restart
