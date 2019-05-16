# msWinX_setups
to setup MS Windows 10 (R)

## onsite
### cmder
在 `Settings->Startup->Environment` 添加
```
set LANG=zh_CN.UTF-8
set LC_ALL=zh_CN.utf8
```
以显示中文.

### Python
- install `anaconda`

- install packages
```
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
conda config --set show_channel_urls yes

#---

pip install --upgrade pip

pip install msgpack
conda install py-xgboost  # conda install -c anaconda py-xgboost
conda install lightgbm
conda install catboost
conda install tensorflow  # conda install -c conda-forge tensorflow 
pip install python-xlib   # import Xlib
pip install pyautogui
pip install jupyterthemes

jt  -t grade3 -f code
wget https://download.lfd.uci.edu/pythonlibs/h2ufg7oq/TA_Lib-0.4.17-cp36-cp36m-win_amd64.whl
pip install TA_Lib-0.4.17-cp36-cp36m-win_amd64.whl
```

- startup script
`ipython profile create` to creat `C:\Users\Me\.ipython\profile_default\ipython_config.py`,
and edit it to fit my needs.

### swift `CapsLock` to`Esc` (or just use `CODE` layout through [AutoHotKey](https://autohotkey.com/) )

```
Windows Registry Editor Version 5.00 
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout] 
"Scancode Map"=hex:00,00,00,00,00,00,00,00,02,00,00,00,01,00,3a,00,00,00,00,00
```

- save the above content to `caps2esc.reg`
- double click `caps2esc.reg` to run it
- confirm

### Vimrc
- install `Vim` to `D:\Vim` (donot install to `C:`)
- backup `D:\Vim\_vimrc`
- put [plug.vim](https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim) into `D:\Vim\vim81\plugin\`
- put `_vimrc` to `D:\Vim\`

### Emacs
Put `init.el` to ` C:\Users\mw\AppData\Roaming\.emacs.d `, and comment the WQY font for han!


## WSL
### Install `Python`:
- Download `Anaconda` from [here](https://anaconda.com/download/),  and
- install it following [this instruction](https://docs.anaconda.com/anaconda/install/) .
- Install tensorflow `pip install tensorflow`.
- Put [the init script](https://github.com/BjmWang/Ubuntu_setups/blob/master/lang/10_python3_startup.py) into `~/.ipython/profile_default/startup`, and uncomment `mpl.use('Agg')`.

### Install applications:
``` shell
sudo su
apt-get -y install wget tcllib golang openvpn pep8 ufw tmux zsh fish gnuplot openssl openssh-client pandoc gdb git zip gdebi auctex clamav aspell exuberant-ctags vim emacs curl libav-tools default-jre default-jdk kismet libpam-mount sl fortune-mod meld hdf5-tools libav-tools at axel gnupg octave aria2 unzip python3-pip python3 golang-1.8
```

### shell
#### bash
```
export http_proxy=http://10.81.6.30:8080
export https_proxy=https://10.81.6.30:8080

export PATH="/home/mw/anaconda3/bin:$PATH"
```

#### apt-proxy
`sudo vi /etc/apt/apt.conf.d/95proxies`

```
Acquire::http::proxy "http://10.81.6.30:8080";
Acquire::https::proxy "https://10.81.6.30:8080";
```

#### fish
```
# ~/.config/fish/config.fish

# Generic
set EDITOR vim

# for Go:
### please be very careful which go you are using!!!
### curl -O https://storage.googleapis.com/golang/go-.-.linux-amd64.tar.gz
### tar -xvf go-.-.linux-amd64.tar.gz ; sudo mv go /usr/local
#set -x PATH /usr/local/go/bin $PATH
set -x GOPATH $HOME/golang
set -x GOBIN $GOPATH/bin
set -x PATH /usr/lib/go-1.8/bin $PATH
set -x PATH $PATH $GOBIN
# Misc.
set -gx PATH $HOME/anaconda3/bin $PATH
#set -gx PATH $HOME/tensorflow/bin $PATH
#set -gx PATH /opt/android-studio/bin $PATH
# ---
set -x FISH_PATH $HOME/.config/fish
set -x PATH /usr/local/sbin $PATH
set -U fish_user_paths $fish_user_paths $GOBIN
# use 256 color term
if begin; status --is-interactive; end
    set -gx TERM xterm-256color
end

# Aliases
alias ,='cd ..'
alias ,,='cd ../..'
alias ,,,='cd ../../..'
alias ,,,,='cd ../../../..'
alias ,,,,,='cd ../../../../..'
alias -='cd -'
alias ed='emacs -nw'
alias ex='emacs'
alias pp='python3'
alias py='ipython3'
alias pyss='python -m SimpleHTTPServer'
alias pipu='sudo pip install --upgrade'
alias jpt='jupyter'
alias jpn='jupyter notebook'
alias jps='jupyter notebook --no-browser --port=8899' # server
alias jpc='ssh -N -f -L localhost:8888:localhost:8899 mw..@svr' # fill real info here!!!
alias jpcvt='jupyter nbconvert --to'
alias mm='tmux -2 attach'
alias sskg='ssh-keygen'
# use sskg to generate id_rsa&id_ras.pub, and copy .pub to ~/.ssh/authorized_keys on server.
alias qg='xmodmap ~/.Q-layout/Q.xmodmap'
alias qc='sudo loadkeys ~/.Q-layout/Q-iso15.kmap'
alias gb="go build -compiler gccgo -gccgoflags='-O3' "
alias mc="pandoc -f markdown+lhs slides.md -o slides.html -t dzslides -i -s -S --toc"
alias uu="sudo apt-get update -y; sudo apt-get upgrade -y; sudo apt-get autoremove --purge -y"

# Function
function kc
  echo "::kotlinc $argv.kt -include-runtime -d $argv.jar"
  kotlinc $argv.kt -include-runtime -d $argv.jar
end

function kr
  echo "::java -jar $argv[1].jar $argv[2..-1]"
  java -jar $argv[1].jar $argv[2..-1]
end

function lc
  ls -ah --color=always $argv | less -R
end

function vi
    if command --search vim >/dev/null do
        vim  $argv[1..-1]
    else
        nvim $argv[1..-1]
    end
end

function vd
    if command --search vim >/dev/null do
        vimdiff $argv[1..-1]
    else
        nvim -d $argv[1..-1]
    end
end

# Local configuration
if test -r ~/.config/fish/local.fish
  . "~/.config/fish/local.fish"
end
```

### Have fun!
