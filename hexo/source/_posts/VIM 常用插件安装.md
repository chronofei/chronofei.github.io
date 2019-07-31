---
title: 安装VIM常用插件
date: 2019-07-31 09:47:00
categories: 技术总结
tags:
 - vim
 - vim插件
---


##  安装插件管理器vundle

* 关于vundle的安装可以参考其[GitHub网址](https://github.com/VundleVim/Vundle.vim)

## 常用插件安装

* 在用户主目录的.vimrc文件中添加如下插件
  ```
  Plugin 'Valloric/YouCompleteMe'
  Plugin 'jiangmiao/auto-pairs'
  Plugin 'vim-airline/vim-airline'
  Plugin 'majutsushi/tagbar'
  Plugin 'godlygeek/tabular'
  Plugin 'scrooloose/syntastic'
  Plugin 'scrooloose/nerdtree'
  Plugin 'scrooloose/nerdcommenter'
  Plugin 'tpope/vim-surround'
  ```

* 在命令行中运行vim,　并在vim中运行PluginInstall，以完成插件的安装。

* 插件配置文件如下：
   ```
   " YouCompleteMe
   let g:ycm_server_python_interpreter='/usr/bin/python'
   let g:ycm_global_ycm_extra_conf='~/.vim/.ycm_extra_conf.py'

   " tagbar
   let g:tarbar_ctags_bin='/usr/bin/ctags'
   let g:tarbar_width=30
   let g:tarbar_left=1
   autocmd bufReadPost *.cpp,*.c,*.h,*.hpp,*.cc,*.cxx call tagbar#autoopen()
   map <F4> :TagbarToggle<CR>
   
   " syntastic
   let g:syntastic_enable_signs = 1
   let g:syntastic_error_symbol='✗'
   let g:syntastic_warning_symbol='►'
   let g:syntastic_always_populate_loc_list = 1
   let g:syntastic_auto_loc_list = 1
   let g:syntastic_loc_list_height = 5
   let g:syntastic_check_on_open = 1
   let g:syntastic_auto_jump = 1
   let g:syntastic_check_on_wq = 0
   let g:syntastic_enable_highlighting=1
   let g:syntastic_cpp_compiler = 'clang++'
   let g:syntastic_cpp_compiler_options = ' -std=c++11 -stdlib=libc++'
   let g:syntastic_python_checkers = ['pyflakes']
   function! <SID>LocationPrevious()                       
     try                                                   
       lprev                                               
     catch /^Vim\%((\a\+)\)\=:E553/                        
       llast                                               
     endtry                                                
   endfunction                                             
   function! <SID>LocationNext()                           
     try                                                   
       lnext                                               
     catch /^Vim\%((\a\+)\)\=:E553/                        
       lfirst                                              
     endtry                                                
   endfunction                                             
   nnoremap <silent> <Plug>LocationPrevious    :<C-u>exe 'call <SID>LocationPrevious()'<CR>                                        
   nnoremap <silent> <Plug>LocationNext        :<C-u>exe 'call <SID>LocationNext()'<CR>
   nmap <silent> sp    <Plug>LocationPrevious              
   nmap <silent> sn    <Plug>LocationNext
   nnoremap <silent> <Leader>ec :SyntasticToggleMode<CR>
   function! ToggleErrors()
       let old_last_winnr = winnr('$')
       lclose
       if old_last_winnr == winnr('$')
           " Nothing was closed, open syntastic error location panel
           Errors
       endif
   endfunction

   " nerdtree
   map <F3> :NERDTreeMirror<CR>
   map <F3> :NERDTreeToggle<CR>
   
   " nerdcommenter
   let g:NERDSpaceDelims=1
   let g:NERDCompactSexyComs=1
   let g:NERDDefaultAlign = 'left'
   let g:NERDAltDelims_java=1
   let g:NERDCustomDelimiters = { 'c' : { 'left': '/**', 'right': '**/' } }
   let g:NERDCommentEmptyLines = 1
   let g:NERDTrimTrailingWhitespace=1
   let mapleader='x'
   
   set hlsearch
   set backspace=2
   set autoindent
   set ruler
   set showmode
   set nu
   set bg=dark
   syntax on
   
   funct CPP()
       exec "!clear && g++ % && ./a.out"
   endfunc
   nmap <silent> <C-a> :call CPP()<CR>
   
   nmap <C-f> :wq<CR>
   ```

* 对于vim下的变成可以参考下面的[vimscript资料](http://learnvimscriptthehardway.onefloweroneworld.com/)

##  安装插件YouCompleteMe

* 在命令行中运行`vim --version`确保vim版本是7.4.143或以上，并且在vim中运行命令`: echo has('python') || has('python3')` ，若返回结果为１，则证明此版本vim支持python2/3脚本。
* 安装必要工具` sudo apt-get install git cmake build-essential python-dev python3-dev  
* 安装C家族语义补全` sudo apt-get install llvm-8 clang-8 libclang-8-dev libboost-all-dev `
   注意：一般参考网页中均安装3.9版本，但是以上依赖项均开发到8.0版本，且3.9版本在Ubuntu 18.04中无法使插件正常工作。
* 使用Git下载YCM源码
```
# 下载YCM源码(在　~/.vim/bundle　目录下)
git clong --recursive git@github.com:Valloric/YouCompleteMe.git
# 检查完整性(在　~/.vim/bundle/YouCompleteMe　目录下)
git submodule update --init --recursive
```

* 编译YCM
```
cd ~/.vim/bundle/YouCompleteMe
./install.py 或 python3 install.py --clang-completer
```
   注意：若运行`./install.py` 时，系统默认使用python2的配置环境，故在.vimrc配置文件中指定python解析器为`let g:ycm_server_python_interpreter='/usr/bin/python'`。若运行`python3 install.py --clang-completer`时，需在.vimrc配置文件中制定python解析器为`let g:ycm_server_python_interpreter='/usr/bin/python３'`。

* 复制.ycm_extra_conf.py文件，并添加vim配置
```
cp ~/.vim/bundle/YouCompleteMe/third_party/ycmd/examples/.ycm_extra_conf.py ~/.vim/
```
   并在.vimrc文件中添加如下配置：
```
let g:ycm_server_python_interpreter='/usr/bin/python'
let g:ycm_global_ycm_extra_conf='~/.vim/.ycm_extra_conf.py'
```

## 参考网址

* [GitHub中YouCompleteMe网址](https://github.com/ycm-core/YouCompleteMe#linux-64-bit)
* [一步一步带你安装史上最难安装的vim插件－－－YouCompleteMe](https://www.jianshu.com/p/d908ce81017a?nomobile=yes)
