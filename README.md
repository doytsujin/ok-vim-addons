# Run vim with addons for source code edit

## Step 1: Install Vim
First, install Vim and any dependencies:

```bash
sudo apt update
sudo apt install vim
```

## Step 2: Install vim-plug Plugin Manager
We'll use vim-plug to manage plugins.

Run the following command to install vim-plug:

```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

## Step 3: Create a .vimrc Configuration File
Now, configure Vim by creating or editing the .vimrc file:

```bash
vim ~/.vimrc
```

Add the following configuration:

```vim
" Initialize vim-plug
call plug#begin('~/.vim/plugged')

" General Plugins
Plug 'scrooloose/nerdtree'              " File explorer
Plug 'itchyny/lightline.vim'            " Lightweight statusline
Plug 'preservim/nerdcommenter'          " Easy commenting

" Syntax Highlighting and Linting
Plug 'dense-analysis/ale'               " Asynchronous linting and fixing
Plug 'sheerun/vim-polyglot'             " Language pack for multiple languages

" Kubernetes, Helm, and YAML
" Plug 'udalov/k8s-vim'                   " Kubernetes manifests
Plug 'towolf/vim-helm'                  " Helm chart support
Plug 'stephpy/vim-yaml'                 " YAML support

" Terraform
Plug 'hashivim/vim-terraform'           " Terraform syntax and formatting

" Ansible
Plug 'pearofducks/ansible-vim'          " Ansible syntax

" Python Development
Plug 'davidhalter/jedi-vim'             " Autocompletion for Python
Plug 'nvie/vim-flake8'                  " Python linting with Flake8

" JavaScript/TypeScript
Plug 'pangloss/vim-javascript'          " JavaScript syntax
Plug 'leafgarland/typescript-vim'       " TypeScript syntax

" Go Development
" Plug 'fatih/vim-go', { 'do': ':GoUpdateBinaries' } " Go development plugin

" Java
" Plug 'neoclide/coc.nvim', {'branch': 'release'}  " Language Server for Java and others

" Autoformatting
Plug 'Chiel92/vim-autoformat'           " Autoformat code

" Git Integration
Plug 'tpope/vim-fugitive'               " Git commands in Vim

" Initialize plugin system
call plug#end()

" General settings
syntax on                              " Enable syntax highlighting
set number                             " Show line numbers
set expandtab                          " Convert tabs to spaces
set shiftwidth=2                       " Indentation width
set tabstop=2                          " Number of spaces for tab
set autoindent                         " Auto-indent new lines
set clipboard=unnamedplus              " Use system clipboard

" Linting settings
let g:ale_fix_on_save = 1              " Fix errors on save
let g:ale_linters = {
\   'python': ['flake8'],
\   'javascript': ['eslint'],
\   'typescript': ['tsserver'],
\   'go': ['gopls'],
\   'terraform': ['tflint'],
\}

" Autoformatting on save
autocmd BufWritePre *.py,*.tf,*.js,*.ts,*.go Autoformat

" Map <C-n> to toggle NERDTree
nnoremap <C-n> :NERDTreeToggle<CR>
```

## Step 4: Install the Plugins
Once the .vimrc is set up, open Vim and install the plugins by running:

```vim
:PlugInstall
```

## Step 5: Configure LSP (Language Server Protocol)
For better autocompletion and language-specific tools, configure coc.nvim for multiple languages:

```bash
:CocInstall coc-pyright coc-tsserver coc-go coc-java coc-json coc-yaml
```

This will provide autocompletion, diagnostics, and navigation for Python, TypeScript, Go, Java, JSON, and YAML files.

## Step 6: Additional Tools
Make sure you have the necessary linters and tools installed for each language:

```bash
# Python (Flake8, Jedi)
pip install flake8 jedi

# JavaScript/TypeScript (ESLint)
npm install -g eslint

# Terraform (TFLint)
sudo apt install tflint

# Go
vim +GoInstallBinaries +qall
```
