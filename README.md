termux-vim-ycm
==============

Installing [YouCompleteMe](https://github.com/Valloric/YouCompleteMe) in [Termux](https://termux.com)

1. Install Prereqs
```bash
pkg update && pkg upgrade && pkg install procps proot vim-python openssh git golang python python-dev libclang cmake patch curl
```
2. restart termux
3. setup proot
```bash
cat - <<EOF >> .bashrc
if ! ps T -o command | grep "^$(type -p proot)" > /dev/null; then
    echo "starting chroot"
    exec termux-chroot
fi
EOF
```
4. restart termux
5. install vundle
```bash
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```
5. setup .vimrc w/vundle, ycm, vim-go
```bash
curl -fsSL https://raw.githubusercontent.com/theimpostor/termux-vim-ycm/master/vundle.vimrc >> ~/.vimrc
```
6. install plugins
```bash
vim +PluginInstall +qall
```
7. patch YCM source to build on android
```bash
cd ~/.vim/bundle/YouCompleteMe/third_party/ycmd && curl https://raw.githubusercontent.com/theimpostor/termux-vim-ycm/master/ycmd.patch | patch -p 1
```
8. build ycm binary
```bash
cd ~/.vim/bundle/YouCompleteMe && ./install.py --go-completer --clang-completer --system-libclang
```
9. install binaries for vim-go
```bash
vim +GoInstallBinaries
```
