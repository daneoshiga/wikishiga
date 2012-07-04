.vimrc
======

Configurações úteis para se ter no arquivo ~/.vimrc
-----------------------------------------------------------------

Colocando aqui todo meu vimrc, algumas das configurações são **específicas** para o
funcionamento de certos plugins, como o pathogen e php-doc, o colorscheme e a
guifont precisam ser instalados no sistema já que não são padrão de nenhuma
distribuição.

No fim do arquivo existe uma lista de plugins, a lista está formata de modo que
seja possível atualizar os plugins usando o script [vimpire](https://bitbucket.org/sirex/vimpire)


    :::vim
    set nocompatible
    set is hls ic scs magic                  " opcoes espertas de busca
    set sm                                   " ShowMatch: mostra o par do parenteses/chaves recem fechado
    set hid                                  " HIDden: nao lembro pra que servia mas era massa
    set aw                                   " AutoWrite: gravacao automatica a cada alteracao
    set ai                                   " AutoIndent: identacao automatica
    set ts=4                                 " TabStop: numero de caracteres de avanco do TAB
    set sw=4                                 " numero de colunas para o comando > (ShiftWidth)
    set sts=4                                " SoftTabStop: must be equal to ShiftWidth so identation in normal mode works fine
    set et                                   " ExpandTab: troca TABs por espacos
    retab                                    " converter os TABs ja existentes
    set report=0                             " reporta acoes com linhas
    set shm=filmnrwxt                        " SHortMessages: encurta as mensagem do rodape
    set ruler                                " mostra a posicao do cursor, regua
    set showcmd                              " mostra o comando sendo executado
    set wm=2                                 " sets a wrap margin of 2 characters, and does automatic word-wrapping
    set lbr                                  " turns linebreak on so words doesn't split on wrap
    set laststatus=2                         " mostra N linhas de estado (status)
    set textwidth=79                         " quebra de linha
    set backspace=indent,eol,start           " Allow backspacing over everything in insert mode.
    set nosmartindent                        " desligando pois esta padrao no CL40
    set autoindent                           " always set autoindenting on
    set copyindent                           " copy the previous indentation on autoindenting
    set wrap                                 " forca a quebra de linha
    set nojoinspaces                         " ! coloca 2 espacos apos o . quando usando o gq
    set history=1000                         " remember more commands and search history
    set undolevels=1000                      " use many muchos levels of undo
    set wildignore=*.swp,*.bak,*.pyc,*.class,*.jpg,*.png,*.gif
    set title                                " change the terminal's title
    set noerrorbells                         " don't beep
    set wildmenu                             " More useful command-line completion
    set wildmode=longest,list:full           " para completacao do TAB igual bash
    set backup                               " habilita backup
    set backupdir=/tmp/
    set dir=/tmp/
    set diffopt+=iwhite                      " Ignore white space in vimdiff
    set number                               " Enable line number
    set scrolloff=8                          " Start scrolling when we're 8 lines away from margins
    set sidescrolloff=15                     " Side scroll of 15 characters
    set sidescroll=1                         " Enable sidescroll
    set foldmethod=indent                    " fold based on indent
    set foldnestmax=3                        " deepest fold is 3 levels
    set nofoldenable                         " dont fold by default
    " set mouse=a
    " set spell           " Enable highlighting of misspelled terms

    " Status line improvements from Kim Schultz ("Hacking Vim")
    set statusline=%F%m%r%h%w\ [FORMAT=%{&ff}]\ [TYPE=%Y]\ [ASCII=\%03.3b]\ [HEX=\%02.2B]\ [POS=%04l,%04v]\ [%p%%]\ [LEN=%L]
    set laststatus=2

    " Source the vimrc file after saving it. This way, you don't have to reload Vim to see the changes.
    if has("autocmd")
     augroup myvimrchooks
      au!
      autocmd bufwritepost .vimrc source ~/.vimrc
     augroup END
    endif

    " tab navigation like firefox
    :nmap <C-up> :tabprevious<CR>
    :nmap <C-down> :tabnext<CR>
    :map <C-up> :tabprevious<CR>
    :map <C-down> :tabnext<CR>
    :imap <C-up> <Esc>:tabprevious<CR>i
    :imap <C-down> <Esc>:tabnext<CR>i
    :nmap <C-t> :tabnew<CR>
    :imap <C-t> <Esc>:tabnew<CR>

    " Set characters to show for trailing whitespace and
    " end-of-line. Also supports tab, but I set expandtab
    " and thus tabs are always turned into spaces.
    " set listchars=tab:>>,trail:!,eol:$

    "configs for ragtag plugin
    inoremap <M-o>  <Esc>o
    inoremap <C-j>  <Down>
    let g:ragtag_global_maps = 1

    " colorscheme torte
    set t_Co=256    "to make Mustang coloscheme work on terminal"

    colorscheme Mustang

    set guifont=Monaco

    " highlight all useless whitespaces
    highlight RedundantSpaces term=standout ctermbg=red guibg=red
    match RedundantSpaces /\s\+$\| \+\ze\t/

    " remove all useless whitespaces
    cab trim %s/\s\+$//

    " Use pathogen to easily modify the runtime path to include all
    " plugins under the ~/.vim/bundle directory
    call pathogen#runtime_append_all_bundles()
    call pathogen#helptags()

    filetype on
    filetype plugin on
    filetype indent on

    if has("autocmd")
        augroup myvimrchooks
            au!
            autocmd bufwritepost .vimrc source ~/.vimrc
        augroup END
    endif

    " syntastic
    let g:syntastic_enable_signs=0
    let g:syntastic_auto_loc_list=1
    let g:syntastic_enable_highlighting=1
    let g:syntastic_loc_list_height=3

    " php-doc
    so ~/.vim/bundle/php-doc/utility/php-doc.vim
    noremap <C-P> <ESC>:call PhpDocSingle()<CR>i
    nnoremap <C-P> :call PhpDocSingle()<CR>
    vnoremap <C-P> :call PhpDocRange()<CR>

    " jquery
    au BufRead,BufNewFile jquery.*.js set ft=javascript syntax=jquery

    " plugin: snipmate git git://github.com/msanders/snipmate.vim.git
    " plugin: vim-repeat git git://github.com/tpope/vim-repeat.git
    " plugin: ragtag git git://github.com/tpope/vim-ragtag.git
    " plugin: surround git git://github.com/tpope/vim-surround.git
    " plugin: markdown git git://github.com/tpope/vim-markdown.git
    " plugin: php-indenting-for-vim git git://github.com/2072/PHP-Indenting-for-VIm.git
    " plugin: tabular git git://github.com/godlygeek/tabular.git
    " plugin: syntastic git git://github.com/scrooloose/syntastic.git
    " plugin: IndexedSearch git git://github.com/vim-scripts/IndexedSearch.git
    " plugin: debugger git git://github.com/vim-scripts/debugger.py.git
    " plugin: php-doc git git://github.com/vim-scripts/php-doc.git
    " plugin: AutoComplPop git git://github.com/vim-scripts/AutoComplPop.git
    " plugin: jquery git git://github.com/vim-scripts/jQuery.git
    " plugin: numbers git git://github.com/myusuf3/numbers.vim.git
    " plugin: vim-l9 git git://github.com/clones/vim-l9.git
    " plugin: matchit git git://github.com/vim-scripts/matchit.zip.git
    " plugin: command-t git git://git.wincent.com/command-t.git
    " run: (cd ruby/command-t ; ruby extconf.rb && make)
