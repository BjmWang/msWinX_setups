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
conda install -c conda-forge jupyterlab

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

### swift `CapsLock` to`Esc` 

```
Windows Registry Editor Version 5.00 
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout] 
"Scancode Map"=hex:00,00,00,00,00,00,00,00,02,00,00,00,01,00,3a,00,00,00,00,00
```

- save the above content to `caps2esc.reg`
- double click `caps2esc.reg` to run it
- confirm

- OR, just use `Wang` layout through [AutoHotKey](https://autohotkey.com/)

### Vimrc
- install `Vim` to `D:\Vim` (donot install to `C:`)
- backup `D:\Vim\_vimrc`
- put [plug.vim](https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim) into `D:\Vim\vim81\plugin\autoload`
- put `_vimrc` to `D:\Vim\`

---
- `neovim`: `C:/Users/xxx/AppData/Local/nvim/`
    + `init.vim`
    + `autoload\plug.vim`

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

### Have fun!
