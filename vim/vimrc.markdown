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
    set textwidth=99                         " quebra de linha
    set backspace=indent,eol,start           " Allow backspacing over everything in insert mode.
    set nosmartindent                        " desligando pois esta padrao no CL40
    set autoindent                           " always set autoindenting on
    set copyindent                           " copy the previous indentation on autoindenting
    set wrap                                 " forca a quebra de linha
    set nojoinspaces                         " ! coloca 2 espacos apos o . quando usando o gq
    set history=1000                         " remember more commands and search history
    set undolevels=1000                      " use many muchos levels of undo
    set undodir=/tmp//
    set undofile
    set wildignore=*.swp,*.bak,*.pyc,*.class,*.jpg,*.png,*.gif
    set title                                " change the terminal's title
    set noerrorbells                         " don't beep
    set wildmenu                             " More useful command-line completion
    set wildmode=longest,list:full           " para completacao do TAB igual bash
    set backup                               " habilita backup
    set backupdir=/tmp//
    set noswapfile
    set diffopt+=iwhite                      " Ignore white space in vimdiff
    set number                               " Enable line number
    set scrolloff=8                          " Start scrolling when we're 8 lines away from margins
    set sidescrolloff=15                     " Side scroll of 15 characters
    set sidescroll=1                         " Enable sidescroll
    set foldmethod=indent                    " fold based on indent
    set foldnestmax=3                        " deepest fold is 3 levels
    set nofoldenable                         " dont fold by default
    set wildignorecase                       " case-insensitive filename completion
    set updatetime=4000                      " fixing updatetime for better easytags usage
    set t_ut=                                " disable Background Color Erase, to make colorschemes work right inside tmux
    "set tags=$VIRTUAL_ENV/tags,~/tags;/
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

    " open definition on new tab
    map <C-\> :tab split<CR>:exec("tag ".expand("<cword>"))<CR>

    " Set characters to show for trailing whitespace and
    " end-of-line. Also supports tab, but I set expandtab
    " and thus tabs are always turned into spaces.
    " set listchars=tab:>>,trail:!,eol:$

    if has("gui_running")
        set guifont=Monaco\ for\ Powerline
    endif

    " highlight all useless whitespaces
    highlight RedundantSpaces term=standout ctermbg=red guibg=red
    match RedundantSpaces /\s\+$\| \+\ze\t/

    " remove all useless whitespaces
    cab trim %s/\s\+$//
    cab vimpressmd 7,$!Markdown.pl

    " Use pathogen to easily modify the runtime path to include all
    " plugins under the ~/.vim/bundle directory
    call pathogen#infect()

    filetype on
    filetype plugin on
    filetype indent on

    " javascript
    autocmd FileType javascript,css setlocal ts=2 sts=2 sw=2 expandtab
    autocmd FileType php set omnifunc=phpcomplete#CompletePHP
    autocmd FileType yaml setlocal ts=2 sts=2 sw=2 expandtab
    " Treat .rss files as XML
    autocmd BufNewFile,BufRead *.rss setfiletype xml

    let php_sql_query=1
    let php_htmlInStrings=1

    set t_Co=256    "to make Mustang coloscheme work on terminal"
    let g:solarized_termcolors=256
    let g:solarized_termtrans=1
    let g:solarized_contrast='high'
    set background=dark
    colorscheme solarized

    if has("autocmd")
        augroup myvimrchooks
            au!
            autocmd bufwritepost .vimrc source ~/.vimrc
        augroup END
    endif

    " lets save the file even if forgot to use sudo
    cmap w!! w !sudo tee % >/dev/null

    " jquery
    au BufRead,BufNewFile jquery.*.js set ft=javascript syntax=jquery

    function! OpenPhpFunction (keyword)
      let proc_keyword = substitute(a:keyword , '_', '-', 'g')
      exe '5 split'
      exe 'enew'
      exe 'set buftype=nofile'
      exe 'silent r!links -dump http://www.php.net/manual/en/print/function.'.proc_keyword.'.php'
      exe 'norm gg'
      exe 'call search ("Description")'
      exe 'norm jdgg'
      exe 'call search("User Contributed Notes")'
      exe 'norm dGgg'
      exe 'norm V'
    endfunction
    au FileType php noremap K :call OpenPhpFunction(expand('<cword>'))<CR>

    " Enable omni completion.
    autocmd FileType css setlocal omnifunc=csscomplete#CompleteCSS
    autocmd FileType html,markdown setlocal omnifunc=htmlcomplete#CompleteTags
    autocmd FileType javascript setlocal omnifunc=javascriptcomplete#CompleteJS
    "autocmd FileType python setlocal omnifunc=pythoncomplete#Complete
    autocmd  FileType python let b:did_ftplugin = 1

    autocmd FileType xml setlocal omnifunc=xmlcomplete#CompleteTags

    autocmd Filetype gitcommit setlocal spell textwidth=72

    autocmd BufNewFile *.py 0put= '# -*- coding: utf-8 -*-'|$

    " plugin: snipmate git git://github.com/msanders/snipmate.vim.git
    " plugin: vim-repeat git git://github.com/tpope/vim-repeat.git
    " plugin: ragtag git git://github.com/tpope/vim-ragtag.git
    inoremap <M-o>  <Esc>o
    inoremap <C-j>  <Down>
    let g:ragtag_global_maps = 1

    " plugin: surround git git://github.com/tpope/vim-surround.git
    " plugin: markdown git git://github.com/tpope/vim-markdown.git
    "" plugin: php-indenting-for-vim git git://github.com/2072/PHP-Indenting-for-VIm.git
    "" plugin: php.vim-html-enhanced git git://github.com/vim-scripts/php.vim-html-enhanced.git
    " plugin: tabular git git://github.com/godlygeek/tabular.git
    " plugin: syntastic git git://github.com/scrooloose/syntastic.git
    let g:syntastic_enable_signs=0
    let g:syntastic_auto_loc_list=1
    let g:syntastic_enable_highlighting=1
    let g:syntastic_loc_list_height=3
    let g:syntastic_python_checkers=['flake8']
    let g:syntastic_python_flake8_args='--ignore=E501,E128,F403'

    " plugin: IndexedSearch git git://github.com/vim-scripts/IndexedSearch.git
    """ plugin: debugger git git://github.com/vim-scripts/debugger.py.git
    "" plugin: php-doc git git://github.com/vim-scripts/php-doc.git
    "" plugin: AutoComplPop git git@github.com:othree/vim-autocomplpop.git
    "let g:acp_completeoptPreview = 1
    "let g:acp_behaviorKeywordLength = 0
    "let g:acp_behaviorPythonOmniLength = 0
    "let g:acp_behaviorHtmlOmniLength = 0
    "let g:acp_behaviorCssOmniPropertyLength = 0

    " plugin: jquery git git://github.com/vim-scripts/jQuery.git
    " plugin: numbers git git://github.com/myusuf3/numbers.vim.git
    " plugin: vim-l9 git git://github.com/clones/vim-l9.git
    " plugin: matchit git git://github.com/vim-scripts/matchit.zip.git
    "" plugin: powerline git git://github.com/Lokaltog/vim-powerline.git
    "let g:Powerline_symbols = 'fancy'

    " plugin: speeddatin git git://github.com/tpope/vim-speeddating.git
    " plugin: autotags git git@github.com:craigemery/vim-autotag.git
    "" plugin: piv git git://github.com/vim-scripts/PIV.git
    "" plugin: vdebug git git://github.com/vim-scripts/Vdebug.git
    " plugin: hybrid git git://github.com/vim-scripts/hybrid.vim.git
    " plugin: jinja--yang git git://github.com/vim-scripts/jinja--Yang.git
    "" plugin: vimpress git git://github.com/PotHix/Vimpress.git
    " plugin: ctrlp git git://github.com/kien/ctrlp.vim.git
    "
    " CtrlP extension for fuzzy-search in tag matches (tjump/tselect replacement)
    " plugin: ctrlp-tjump git git@github.com:vim-scripts/ctrlp-tjump.git

    " Make gvim-only colorschemes work transparently in terminal vim
    " plugin: csapprox git git://github.com/godlygeek/csapprox.git

    " Solarized colorscheme
    " plugin: solarized git git@github.com:altercation/vim-colors-solarized.git

    " Make CSS more readable
    " plugin: bettercss git git://github.com/vim-scripts/Better-CSS-Syntax-for-Vim.git

    " PHP Collection contains: compiler, ftplugin, script for K key, dicts
    "" plugin: phpcollection git git://github.com/vim-scripts/PHPcollection.git

    " Insert or delete brackets, parens, quotes in pair.
    " plugin: autopairs git git://github.com/vim-scripts/Auto-Pairs.git

    "" live reload
    "" plugin: livereload git https://github.com/flomotlik/vim-livereload.git
    "" run: (rake)

    " Vim runtime files for Haml, Sass, and SCSS
    " plugin: sass git https://github.com/tpope/vim-haml.git
    "
    " New maintained version of vim-javascript
    " plugin: vim-javascript git git://github.com/vim-scripts/vim-javascript.git
    "
    " Show local changes based on git
    " plugin: vim-signify git git@github.com:mhinz/vim-signify.git
    "
    " Like powerline, but smaller/faster
    " plugin: vim-airline git https://github.com/bling/vim-airline.git
    let g:airline_powerline_fonts = 1
    let g:airline_left_sep = '⮀'
    let g:airline_left_alt_sep = '⮁'
    let g:airline_right_sep = '⮂'
    let g:airline_right_alt_sep = '⮃'
    let g:airline_branch_prefix = '⭠'
    let g:airline_readonly_symbol = '⭤'
    let g:airline_linecolumn_prefix = '⭡'
    let g:airline_theme='badwolf'
    let g:airline#extensions#syntastic#enabled = 1
    let g:airline#extensions#tagbar#enabled = 1

    "
    " Lightweight, customizable and functional Vim plugin for JSHint integration.
    " plugin: jshint2 git git@github.com:vim-scripts/jshint2.vim.git
    "
    " Using the jedi autocompletion library for VIM.
    " plugin: jedi-vim git https://github.com/davidhalter/jedi-vim.git
    " run: (git submodule update --init)
    let g:jedi#auto_initialization = 1
    let g:jedi#popup_select_first = 0
    let g:jedi#show_call_signatures = 0

    " Add the virtualenv's site-packages to vim path
    if has('python')
    py << EOF
    import os.path
    import sys
    import vim
    if 'VIRTUAL_ENV' in os.environ:
        project_base_dir = os.environ['VIRTUAL_ENV']
        sys.path.insert(0, project_base_dir)
        activate_this = os.path.join(project_base_dir, 'bin/activate_this.py')
        execfile(activate_this, dict(__file__=activate_this))
    EOF
    endif

    " Puppet language syntax highlighting for Vim
    " plugin: puppet-syntax-vim git git@github.com:puppetlabs/puppet-syntax-vim.git
    "
    " Perform all your vim insert mode completions with Tab
    " plugin: supertab git git@github.com:ervandew/supertab.git
    "
    " Tagbar
    " plugin: tagbar git git://github.com/majutsushi/tagbar
    nmap <F8> :TagbarToggle<CR>
    let g:tagbar_autoclose = 1
    let g:tagbar_show_visibility = 0
    let g:tagbar_show_linenumbers = -1

    " Fugitive Git wrapper
    " plugin: fugitive git git://github.com/tpope/vim-fugitive.git
    " run: (vim -u NONE -c "helptags vim-fugitive/doc" -c q)
    " autocmd BufReadPost fugitive://* set bufhidden=delete

    " unimpaired
    " plugin: unimpaired git git@github.com:tpope/vim-unimpaired.git
