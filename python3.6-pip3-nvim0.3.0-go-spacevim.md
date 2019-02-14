# Linux Ubuntu 安装python3.6&pip3&nvim0.3.0&go&spacevim
---

1. 安装python3.6 

    - sudo apt-get install software-properties-common
    - sudo add-apt-repository ppa:jonathonf/python-3.6
    - sudo apt-get update // 检查包并安装
    - sudo apt-get install python3.6
    - python -V
    - python3 -V

2. Ubuntu下pip3的安装、升级、卸载

    - Ubuntu下pip3的安装
        sudo apt-get install python3-pip
    - Ubuntu下pip3的升级
        sudo pip3 install --upgrade pip/neovim...
    - Ubuntu下pip3的卸载
        sudo apt-get remove python3-pip
    - pip -V
    - pip3 -V
        
3. Ubuntu下安装go插件
    
    - 输入 vi 1.go， 编写golang的代码
    - 输入 :GoInstallBinaries，然后按下回车键，这时已经开始安装vim-go插件

4. Ubuntu下升级SpaceVim

    - vi .zprofile
    - 输入 :SPUpdate，然后按下回车键 （SPInstall）

5. 新建用户给予sudo权限

    - chmod u+w /etc/sudoers 开启sudoers文件的读写权限
    - test ALL=(ALL:ALL) ALL 给予sudo权限
    - chmod u-w /etc/sudoers 开启sudoers文件的读写权限
    - 或者直接sudo visudo

###### tags: `Linux`
