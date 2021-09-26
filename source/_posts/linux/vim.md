title: vim
categories:
  - linux
tags:
  - vim
date: 2021-08-17 10:49:00
---
## 我的nvim配置
```sh
https://github.com/formattedd/vimrc
```

## 插件

### 代码补全插件 lsp

```sh
Plug 'prabirshrestha/vim-lsp'
Plug 'mattn/vim-lsp-settings'

Plug 'prabirshrestha/asyncomplete.vim'
Plug 'prabirshrestha/asyncomplete-lsp.vim'


function! s:on_lsp_buffer_enabled() abort
    setlocal omnifunc=lsp#complete
    setlocal signcolumn=yes
    if exists('+tagfunc') | setlocal tagfunc=lsp#tagfunc | endif
    nmap <buffer> gd <plug>(lsp-definition)
    nmap <buffer> gs <plug>(lsp-document-symbol-search)
    nmap <buffer> gS <plug>(lsp-workspace-symbol-search)
    nmap <buffer> gr <plug>(lsp-references)
    nmap <buffer> gi <plug>(lsp-implementation)
    nmap <buffer> gt <plug>(lsp-type-definition)
    nmap <buffer> <leader>rn <plug>(lsp-rename)
    nmap <buffer> [g <plug>(lsp-previous-diagnostic)
    nmap <buffer> ]g <plug>(lsp-next-diagnostic)
    nmap <buffer> K <plug>(lsp-hover)
    inoremap <buffer> <expr><c-f> lsp#scroll(+4)
    inoremap <buffer> <expr><c-d> lsp#scroll(-4)
    nmap <Space>f <plug>(lsp-document-format)

    let g:lsp_document_highlight_enabled = 1
    let g:lsp_diagnostics_enabled = 1
    let g:lsp_format_sync_timeout = 1000
    autocmd! BufWritePre *.go,*.py call execute('LspDocumentFormatSync')
    " autocmd BufWritePre <buffer> LspDocumentFormatSync

    " refer to doc to add more commands
endfunction


augroup lsp_install
    au!
    " call s:on_lsp_buffer_enabled only for languages that has the server registered.
    autocmd User lsp_buffer_enabled call s:on_lsp_buffer_enabled()
augroup END

```

### coc

```sh
Plug 'neoclide/coc.nvim', {'branch': 'release'} " Use release branch (recommend)

let g:coc_disable_startup_warning=1
let g:coc_global_extensions = [
            \ 'coc-translator',
            \ 'coc-html',
            \ 'coc-css',
            \ 'coc-cssmodules',
            \ 'coc-pairs',
            \ 'coc-git',
            \ 'coc-gitignore',
            \ 'coc-highlight',
            \ 'coc-marketplace',
            \ 'coc-explorer']

function! s:check_back_space() abort
    let col = col('.') - 1
    return !col || getline('.')[col - 1]  =~# '\s'
endfunction

nmap <Space>n :CocCommand explorer<CR>
autocmd BufEnter * if (winnr("$") == 1 && &filetype == 'coc-explorer') | q | endif

```

#### explorer 文件目录配置相对行
```sh
vi ~/.config/coc/extensions/node_modules/coc-explorer/autoload/coc_explorer/init.vim

找到relativenumber，修改0为1
```

### 注释
```sh
Plug 'preservim/nerdcommenter' " 注释

nmap <Space><Space> <plug>NERDCommenterToggle

" Add spaces after comment delimiters by default
let g:NERDSpaceDelims = 1

" Use compact syntax for prettified multi-line comments
let g:NERDCompactSexyComs = 1

" Align line-wise comment delimiters flush left instead of following code indentation
let g:NERDDefaultAlign = 'left'

" Set a language to use its alternate delimiters by default
let g:NERDAltDelims_java = 1

" Add your own custom formats or override the defaults
" let g:NERDCustomDelimiters = { 'c': { 'left': '/**','right': '*/' } }

" Allow commenting and inverting empty lines (useful when commenting a region)
let g:NERDCommentEmptyLines = 1

" Enable trimming of trailing whitespace when uncommenting
let g:NERDTrimTrailingWhitespace = 1

" Enable NERDCommenterToggle to check all selected lines is commented or not
let g:NERDToggleCheckAllLines = 1

```