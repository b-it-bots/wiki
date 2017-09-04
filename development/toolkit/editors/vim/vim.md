# Vim
## Introductory Material
[The vim cheatsheet and introductory tutorial](http://www.viemu.com/a_vi_vim_graphical_cheat_sheet_tutorial.html)

## Installation
First of all make sure that vim is installed
```bash
sudo apt-get install vim
```

Copy the `.vimrc` file in this directory to your home directory as `.vimrc`.
Assuming that you cloned this repository in your home folder you can do:
```
cp ~/dotfiles/vim/.vimrc ~/
```

If it doesn't exist already, create a directory "autoload" inside `.vim`:
```
mkdir -p ~/.vim/autoload
```

Go to that directory:
```
cd ~/.vim/autoload
```

Download the plugin:
```
curl https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim -o plug.vim
```

Enter vim:
```
vim
```

Install all plugins by calling PlugInstall inside vim
```
:PlugInstall!
```
Once it's done installing the plugins, in your `.vimrc` file go to line 17 and uncomment it.

<Change the following variable `TIMEOUT_SECONDS = 0.5` to `2` in the file with path `~/.vim/YouCompleteMe/python/ycm/client/completion_request.py`>

# Contributors
* Octavio Arriaga - **Original author**
* Argentina Ortega - **Formatting**

# See Also
* https://egghead.io/courses/learn-to-use-vim
