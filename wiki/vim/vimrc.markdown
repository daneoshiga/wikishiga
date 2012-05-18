.vimrc
======
Configurações úteis para se ter no arquivo /home/[usuario]/.vimrc

    :::vim
    set sm                         " ShowMatch: mostra o par do parenteses/chaves recem 
                                   " fechado
    set hid                        " HIDden: nao lembro pra que servia mas era massa
    set aw                         " AutoWrite: gravacao automatica a cada alteracao
    set ai                         " AutoIndent: identacao automatica
    set ts=4                       " TabStop: numero de caracteres de avanco do TAB
    set sw=4                       " numero de colunas para o comando > (ShiftWidth)
    set sts=4                      " SoftTabStop: must be equal to ShiftWidth so 
                                   " identation in normal mode works fine
    set et                         " ExpandTab: troca TABs por espacos
    set report=0                   " reporta acoes com linhas
    set shm=filmnrwxt              " SHortMessages: encurta as mensagem do rodape
    set ruler                      " mostra a posicao do cursor, regua
    set showcmd                    " mostra o comando sendo executado
    set wm=2                       " sets a wrap margin of 2 characters, and does 
                                   " automatic word-wrapping
    set laststatus=2               " mostra N linhas de estado (status)
    set textwidth=79               " quebra de linha
    set backspace=indent,eol,start " Allow backspacing over everything in insert mode.
    set nosmartindent              " desligando pois esta padrao no CL40
    set autoindent                 " always set autoindenting on
    set copyindent                 " copy the previous indentation on autoindenting
    set nojoinspaces               " ! coloca 2 espacos apos o . quando usando o gq
    set history=1000               " remember more commands and search history
    set undolevels=1000            " use many muchos levels of undo
    set title                      " change the terminal's title
    set noerrorbells               " don't beep
    set wildmode=longest,list:full " para completacao do TAB igual bash
    set diffopt+=iwhite            " Ignore white space in vimdiff
    set number                     " Enable line number
    set wildignore=*.swp,*.bak,*.pyc,*.class


    filetype on
    filetype plugin on
    filetype indent on



Comandos do vim
