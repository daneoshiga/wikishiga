Comandos
========

Combinações de teclas executadas no modo 'Normal' do vim

###Identar todo o arquivo###

    :::vim
    gg=G

####Funcionamento:####
* __gg__    vai pro inicio do arquivo
* __=__     comando de identação
* __G__     faz o movimento até o fim do arquivo, o que identa o código

###Shell dentro do vim
É possível executar comandos do shell dentro do vim, ou abrir um teminal sem
fechar o vim

    :::vim
    !ls

    :sh

    !!ls

* usando __!__ o comando é executado no shell, e em seguida retorna pro vim  

* usando __:sh__ um shell é aberto para execução de vários comandos, ctrl-d ou
  exit fecha o shell e volta para o vim  

* usando __!!__ coloca o output de um comando shell dentro do arquivo do vim na
  posição atual do cursor  
