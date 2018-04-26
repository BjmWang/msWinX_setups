# msWinX_setups
to setup MS Windows 10 (R)

### Install applications:
``` shell
sudo su
apt-get -y install wget tcllib golang openvpn pep8 ufw tmux zsh fish gnuplot openssl openssh-client pandoc gdb git zip gdebi auctex clamav aspell exuberant-ctags vim curl libav-tools default-jre default-jdk kismet libpam-mount sl fortune-mod meld hdf5-tools libav-tools at axel gnupg octave aria2 unzip python3-pip python3
```

### swift `CapsLock` to`Esc`

```
Windows Registry Editor Version 5.00 
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout] 
"Scancode Map"=hex:00,00,00,00,00,00,00,00,02,00,00,00,01,00,3a,00,00,00,00,00
```

- save the above content to `caps2esc.reg`
- double click `caps2esc.reg` to run it
- confirm

### vimrc
- install `Vim` to `D:\Vim` (donot install to `C:`)
- backup `D:\Vim\_vimrc`
- creat the new `D:\Vim\_vimrc`:
```
" VINE """""""""""""""""""""""""""""""""""""""""""""""""""""""""
"
" mw's Vim configuration,
"   ms win version --- no plugins
"
" Based on Amir Salihefendic's basic.vimrc
"     https://github.com/amix/vimrc
" Bram Moolenaar's mswin.vim
"     http://vim.cybermirror.org/runtime/mswin.vim
" and many other internet resources.
"
" COPYRIGHT  B.W.  2010-2018
" https://github.com/BjmWang/msWinX_setups
"
""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""

""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
" => Init
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
" necesary for lots of cool vim things
set nocompatible

" replace system's fish shell. run sh cmd with :! or :r!
set shell=/bin/zsh

" Sets how many lines of history VIM has to remember
set history=1000

" Enable filetype plugins
filetype plugin on
filetype indent on

" Set to auto read when a file is changed from the outside
set autoread

" set the leader
let mapleader = ","
let g:mapleader = ","

"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
" => Mode
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
" Enable syntax highlighting
syntax enable

"set fold
set foldmethod=indent " syntax, indent, marker, manual, expr ...
set foldlevel=10

" set line break
set linebreak
set textwidth=0
set wrapmargin=0

" Turn on the WiLd menu
set wildmenu

" command-line completion
set wildmode=longest:full,full

" to recognize a list header
set formatlistpat=^\\s*\\(\\d\\\|[-*]\\)\\+[\\]:.)}\\t\ ]\\s*
set formatoptions+=n

"show the tabes
set list
set listchars=tab:\|\ ,trail:-,extends:#,nbsp:.

"do not break words joined by the following characters
set iskeyword+=_,@

" make >> and << work better
set shiftround

" Specify the behavior when switching between buffers
set switchbuf=useopen,usetab,newtab
set stal=2

" wrap or not
set wrap
set whichwrap+=<,>,[,],h,l,b,s,~

" A buffer becomes hidden when it is abandoned
set hid

" Ignore case when searching
set ignorecase

" When searching try to be smart about cases
set smartcase

" Highlight search results
set hlsearch

" Makes search act like search in modern browsers
set incsearch

" Don't redraw while executing macros (good performance config)
set lazyredraw

" For regular expressions turn magic on
set magic

"use dialog when file was not saved
set confirm

"inline replace
set gdefault

"set auto-complete
set completeopt=longest,menu

"share clipboard
set clipboard+=unnamedplus

" Use spaces instead of tabs
set expandtab

" 1 tab == 4 spaces
set shiftwidth=4
set tabstop=4

" Show matching brackets, and how many tenths of a second to show
set showmatch
set mat=10

" set delay
set timeoutlen=1000

"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
" => Screen
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
" No annoying sound on errors
set noerrorbells
set novisualbell
set t_vb=
set tm=500

" Add a bit extra margin to the left
set foldcolumn=3

" Increase the space between lines
set linespace=3

"show the command typing
set showcmd

" Try to keep the cursor line in the vertically center (27 lines)
set scrolloff=3

"Always show current position
set ruler

"show line number
set number

" hightlight current line/col
set cursorline
set cursorcolumn

" Enable syntax highlighting
syntax enable

" Height of the command bar
set cmdheight=2

" colorscheme and background
let $VIM_TUI_ENABLE_TRUE_COLOR=1
colorscheme desert"pencil
set background=light "dark "
set t_ut=

" Set extra options when running in GUI mode
if has("gui_running")
    set guioptions-=T
    set guioptions-=e
    set t_Co=256
    set guitablabel=%M\ %t
endif

" colors
set colorcolumn=+1
hi ColorColumn NONE ctermbg=Cyan

"set font
"set guifont=Bitstream\ Vera\ Sans\ Mono\ 12
set guifont=DejaVu\ Sans\ Mono\ 14

" add more components to statusline
set statusline+=%#warningmsg#
"set statusline+=%{SyntasticStatuslineFlag()}
set statusline+=%*

" display the status line always
set laststatus=2

"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
" => Files
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
" Set dir to the current file's directory.
set autochdir

" Open dialog defaults to the current file's directory.
set browsedir=buffer

" Use Unix as the standard file type
set ffs=unix,dos,mac

" Ignore compiled files
set wildignore=*.o,*~,*.pyc
if has("win16") || has("win32")
    set wildignore+=*/.git/*,*/.hg/*,*/.svn/*,*/.DS_Store
else
    set wildignore+=.git\*,.hg\*,.svn\*
endif

" Turn backup on. Need to build these folders manually.
"set backup
"set backupdir=$HOME/.vim/backup
"set directory=$HOME/.vim/tmp

" Set utf8 as standard encoding, and en_US as the standard language
set encoding=utf8
set termencoding=utf8

"Chinese vim menus (windows)
source $VIMRUNTIME/delmenu.vim
source $VIMRUNTIME/menu.vim

"Chinese vim messages (windows)
language messages zh_CN.utf-8

" encodeing just opened file.
set fileencodings=utf8,gbk,ucs-bom,cp936,gb2312,gb18030,big5,euc-jp,euc-kr

" Return to last edit position when opening files (You want this!)
autocmd BufReadPost *
    \ exec ":call UpdateCopyright()" |
    \ if line("'\"") > 0 && line("'\"") <= line("$") |
    \ exe "normal! g`\"" |
    \ exe "normal! zz" |
    \ endif

" Automatically update copyright notice with current year
autocmd BufWritePre *
    \ exec ":call UpdateCopyright()" |
    \ exec ":call DeleteTrailingWS()" |
    \ let &backupext = '.-' . strftime("%Y%m%d-%H%M%S")

" enable omni-completion
set omnifunc=syntaxcomplete#Complete
autocmd FileType python set omnifunc=pythoncomplete#Complete
autocmd FileType perl set omnifunc=perlcomplete#Complete
autocmd FileType javascript set omnifunc=javascriptcomplete#CompleteJS
autocmd FileType node set omnifunc=javascriptcomplete#CompleteJS
autocmd FileType html set omnifunc=htmlcomplete#CompleteTags
autocmd FileType css set omnifunc=csscomplete#CompleteCSS
autocmd FileType xml set omnifunc=xmlcomplete#CompleteTags
autocmd FileType php set omnifunc=phpcomplete#CompletePHP
autocmd FileType cpp set omnifunc=cppcomplete#Complete
autocmd FileType c set omnifunc=ccomplete#Complete
autocmd FileType d set omnifunc=ccomplete#Complete
autocmd Filetype octave set omnifunc=syntaxcomplete#Complete
autocmd FileType go set omnifunc=gocomplete#Complete

" commenting blocks of code.
autocmd FileType *                     let b:comment_leader = '// '
autocmd FileType c,d,cpp,java,scala,go let b:comment_leader = '// '
autocmd FileType sh,ruby,python,text   let b:comment_leader = '#  '
autocmd FileType conf,fstab,perl       let b:comment_leader = '#  '
autocmd FileType tex,octave            let b:comment_leader = '%  '
autocmd FileType mail                  let b:comment_leader = '>  '
autocmd FileType vim                   let b:comment_leader = '"  '
autocmd FileType lisp                  let b:comment_leader = ';; '
autocmd FileType haskell,vhdl,ada      let b:comment_leader = '-- '

"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
" => Keybindings
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
" Treat long lines as break lines (useful when moving around in them)
nnoremap j gj
nnoremap k gk
nnoremap <Down> gj
nnoremap <Up> gk
inoremap <Down> <C-o>gj
inoremap <Up> <C-o>gk

" Map \ to replace
noremap \ :1,$s/%/ic

" Disable highlight when <leader>/ is pressed.
noremap <silent> <leader>/ :noh<CR>

" Del the tailing ^M (to work with MSDOS files)
noremap <Leader>; mmHmt:%s/<C-V><cr>//ge<cr>'tzt'm

" Don't close window, when deleting a buffer
command! Bclose call <SID>BufcloseCloseIt()

" Opens a new tab with the current buffer's path
noremap <leader><CR> :tabedit <c-r>=expand("%:p:h")<CR>/

" :W sudo saves the file
command! W w !sudo tee % > /dev/null

" Switch CWD to the directory of the open buffer
map <leader>cd :cd %:p:h<cr>:pwd<cr>

" Move a line of text using ALT+[jk] or Comamnd+[jk] on mac
nnoremap <M-j> mz:m+<CR>`z
nnoremap <M-k> mz:m-2<CR>`z
vnoremap <M-j> :m'>+<CR>`<my`>mzgv`yo`z
vnoremap <M-k> :m'<-2<CR>`>my`<mzgv`yo`z

" Delete trailing white spaces
noremap <leader><BS> :%s/\s\+$//ge<CR>

" F1-F4 resources
noremap <F1> :Denite file_rec<CR>
noremap <F2> :Denite buffer<CR>
noremap <F3> :Denite line<CR>
noremap <F4> :Denite change<CR>

" F5: run according to filetypes
au FileType go nmap <F5> :terminal<CR><Plug>(go-run)
au FileType python let g:pymode_run_bind = "<F5>"

" F6: toggle and untoggle spell checking
noremap <F6> :setlocal spell!<CR>

" F7: build something
au FileType go nmap <F7> <Plug>(go-build)
au FileType tex nmap <F7> :!xelatex %<CR>
au FileType markdown nmap <F7> :!pandoc -f markdown+lhs % -o markdown.html -t dzslides -i -s -S --toc<CR>

" F8: open vim file explorer
noremap <F8> :NERDTreeToggle<CR>

" F9: start the debugger
noremap <F9> :VBGstartGDB

" F10: tags
noremap <F10> :TagbarToggle<CR>

" F11: be focus
noremap <F11> 2o<ESC>k:call AddPartingLine()<CR>j

" F12 attach copyright things
noremap <F12> :call AddCopyright()<CR>:call ProcessEnv()<CR>

" backspace in Visual mode deletes selection
vnoremap <BS> d
inoremap <C-BS> <C-W>
inoremap <C-Del> <C-O>dw

" Use CTRL-S for saving, also in Insert mode
noremap  <C-S> :update<CR>
vnoremap <C-S> <C-C>:update<CR>
inoremap <C-S> <C-O>:update<CR>

" CTRL-F4 is Close window
noremap  <C-F4> <C-W>c
inoremap <C-F4> <C-O><C-W>c
cnoremap <C-F4> <C-C><C-W>c
onoremap <C-F4> <C-C><C-W>c

" Smart way to move between windows (<ctrl>j etc.)
map <C-j> <C-W>j
map <C-k> <C-W>k
map <C-h> <C-W>h
map <C-l> <C-W>l

" emacsish keybindings
noremap  <C-G> <Esc>
vnoremap <C-G> <Esc>
snoremap <C-G> <Esc>
inoremap <C-G> <Esc>
cnoremap <C-G> <Esc>

" run a command
noremap  <C-Z> :
vnoremap <C-Z> :
snoremap <C-Z> :
inoremap <C-Z> <C-O>:

"Change Y to yank to end of line
map Y y$

" paste over without overwriting register
xnoremap p pgvy
xnoremap P Pgvy

" Toggle paste mode on and off
map <leader>pp :setlocal paste!<cr>

" To avoid the extra 'shift' keypress when typing the colon to go to cmdline mode
noremap ; :
noremap ;; ;

" Quickly insert parenthesis/brackets/etc.
inoremap <space>( ()<esc>i
inoremap <space>[ []<esc>i
inoremap <space>{ {}<esc>i
inoremap <space>' ''<esc>i
inoremap <space>" ""<esc>i
inoremap <space>` ``<esc>i
inoremap <space>$ $$<esc>i
inoremap <space>\| \|\|<esc>i

" Surround the visual selection in parenthesis/brackets/etc.
vnoremap <space>( <esc>`>a)<esc>`<i(<esc>
vnoremap <space>[ <esc>`>a]<esc>`<i[<esc>
vnoremap <space>{ <esc>`>a}<esc>`<i{<esc>
vnoremap <space>" <esc>`>a"<esc>`<i"<esc>
vnoremap <space>' <esc>`>a'<esc>`<i'<esc>
vnoremap <space>` <esc>`>a`<esc>`<i`<esc>
vnoremap <space>$ <esc>`>a$<esc>`<i$<esc>
vnoremap <space>\| <esc>`>a\|<esc>`<i\|<esc>

" brackets
inoremap <expr> <silent> ( MayCloseParentheses('(')
inoremap <expr> <silent> [ MayCloseParentheses('[')
inoremap <expr> <silent> { MayCloseParentheses('{')

" Insert the current date and time (useful for timestamps)
iab xdate <c-r>=strftime("%Y/%m/%d %H:%M:%S")<cr>

""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
" => Functions
"""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""""
function! HasPaste()
    if &paste
        return 'MP'
    else
        return 'NP'
    endif
endfunction

function! <SID>BufcloseCloseIt()
    let l:currentBufNum = bufnr("%")
    let l:alternateBufNum = bufnr("#")
    if buflisted(l:alternateBufNum)
      buffer #
    else
      bnext
    endif
    if bufnr("%") == l:currentBufNum
      new
    endif
    if buflisted(l:currentBufNum)
      execute("bdelete! ".l:currentBufNum)
    endif
endfunction

function! DeleteTrailingWS()
    exe "normal mz"
    %s/\s\+$//ge
    exe "normal `z"
endfunction

function! MayCloseParentheses(cmd)
    if col('.') == col('$')
        if a:cmd == '('
            return "()\<Left>"
        elseif a:cmd == '{'
            return "{}\<Left>"
        elseif a:cmd == '['
            return "[]\<Left>"
        endif
    else
        if a:cmd == '('
            return "("
        elseif a:cmd == '['
            return "["
        elseif a:cmd == '{'
            return "{"
        endif
    endif
endfunction

function! HasLinewidth()
    if &tw<1000
        return &tw
    else
        return 'K+'
    endif
endfunction

function! AddPartingLine()
    call append(line('.'), b:comment_leader . "· <=>---<=> · <=>---<=> · <=>---<=> · <=>---<=> · <=>---<=> · <=>---<=>")
endfunction

function! AddCopyright()
    call append(0, b:comment_leader . "==============================================")
    call append(1, b:comment_leader . "·")
    call append(2, b:comment_leader . "· Author: Benjamin Wang")
    call append(3, b:comment_leader . "·")
    call append(4, b:comment_leader . "· Benjamin.mj.wang@gmail.com")
    call append(5, b:comment_leader . "·")
    call append(6, b:comment_leader . "· Filename: ".expand("%:t"))
    call append(7, b:comment_leader . "·")
    call append(8, b:comment_leader . "· COPYRIGHT ".strftime("%Y"))
    call append(9, b:comment_leader . "·")
    call append(10, b:comment_leader . "· Description:")
    call append(11, b:comment_leader . "·")
    call append(12, b:comment_leader . "==============================================")
    call append(13, "")
    echohl WarningMsg | echo "copyright information added." | echohl None
endfunction

function! UpdateCopyright()
    let n=1
    while n < 20
        let line = getline(n)
        if line =~ '\s*\S*COPYRIGHT\S*.*$'
            if line !~ strftime("%Y")
                exe "g#\\cCOPYRIGHT \\(".strftime("%Y")."\\)\\@![0-9]\\{4\\}\\(-".strftime("%Y")."\\)\\@!#s#\\([0-9]\\{4\\}\\)\\(-[0-9]\\{4\\}\\)\\?#\\1-".strftime("%Y")
            endif
            echohl WarningMsg | echo "copyright information updated." | echohl None
            return
        endif
        let n = n + 1
    endwhile
    echohl WarningMsg | echo "no copyright information found." | echohl None
endfunction

function! ProcessEnv()
    let n=1
    while n < 3
        let line = getline(n)
        if line =~ '\s*\S*env\S*.*$'
            echohl WarningMsg | echo "env information exists." | echohl None
            return
        endif
        let n = n + 1
    endwhile
    if &filetype == 'tex'
        call append(0, b:comment_leader . "!/usr/bin/env pdflatex")
    elseif &filetype == 'sh'
        call append(0, b:comment_leader . "!/usr/bin/env fish")
    elseif &filetype == 'python' || &filetype == 'py'
        call append(0, b:comment_leader . "!/usr/bin/env python")
    elseif &filetype == 'octave' || &filetype == 'm'
        call append(0, "#  !/usr/bin/env octave")
    else
        call append(0, b:comment_leader . "!/usr/bin/env " . &filetype)
    endif
    call append(1, b:comment_leader . "-*- coding:utf-8 -*-")
    call append(2, "")
    echohl WarningMsg | echo "env information added(gg check it)!" | echohl None
endfunction

augroup LargeFile
        " Set options:
        "   eventignore+=FileType (no syntax highlighting etc
        "   assumes FileType always on)
        "   noswapfile (save copy of file)
        "   bufhidden=unload (save memory when other file is viewed)
        "   buftype=nowritefile (is read-only)
        "   undolevels=-1 (no undo possible)
        let g:large_file = 1048576 " 1MB

        au BufReadPre *
                \ let f=expand("<afile>") |
                \ if getfsize(f) > g:large_file |
                        \ set eventignore+=FileType |
                        \ setlocal noswapfile bufhidden=unload buftype=nowrite undolevels=-1 |
                \ else |
                        \ set eventignore-=FileType |
                \ endif
augroup END
```

### have fun!
