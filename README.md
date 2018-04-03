termux-vim-ycm
==============

Installing [YouCompleteMe](https://github.com/Valloric/YouCompleteMe) and [vim-go](https://github.com/fatih/vim-go) in [Termux](https://termux.com)

1. Install prereqs
```bash
pkg update && pkg upgrade && pkg install procps proot vim-python openssh git golang python python-dev libclang cmake patch curl libcrypt-dev
```
2. Restart termux
3. Setup proot
```bash
cd ~ && curl -fsSL https://raw.githubusercontent.com/theimpostor/termux-vim-ycm/master/bashrc.patch | patch
```
4. Restart termux
5. Install vundle
```bash
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```
5. Setup .vimrc w/vundle, ycm, vim-go
```bash
curl -fsSL https://raw.githubusercontent.com/theimpostor/termux-vim-ycm/master/vundle.vimrc >> ~/.vimrc
```
6. Install plugins
```bash
vim +PluginInstall +qall
```
7. Patch YCM source to build on android
```bash
cd ~/.vim/bundle/YouCompleteMe/third_party/ycmd && curl https://raw.githubusercontent.com/theimpostor/termux-vim-ycm/master/ycmd.patch | patch -p 1
```
8. Build ycm binary
```bash
cd ~/.vim/bundle/YouCompleteMe && ./install.py --go-completer --clang-completer --system-libclang
```
9. Install binaries for vim-go
```bash
vim +GoInstallBinaries
```
