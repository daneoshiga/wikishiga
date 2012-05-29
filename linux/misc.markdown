Misc
=

###SSH sem mensagens

para evitar que, ao conectar ssh na máquina, apareçam as mensagens de ultimo
login, ou de pacotes a serem atualizados, só é necessário criar o arquivo
.hushlogin na home.

    :::bash
    touch ~/.hushlogin

mais informações: man login
