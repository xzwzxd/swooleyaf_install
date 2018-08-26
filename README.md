# 介绍
- 拉取项目需要安装git和git-lfs,有部分文件是git-lfs上传

# docker-compose安装
    cp resources/linux/docker-compose-Linux-x86_64 /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose
    docker-compose --version

# python3安装(centos7)
    wget https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tar.xz
    mkdir /usr/local/python3
    tar -Jxvf Python-3.6.4.tar.xz
    cd Python-3.6.4
    ./configure --prefix=/usr/local/python3
    make && make install
    /usr/local/python3/bin/pip3 install fabric3

# pycharm配置
    Setting->Project->Project Interpreter->Add Local
    设置Base interpreter并勾选上Inherit global site-packages

# 贝叶斯分类
    https://www.jianshu.com/p/f6a3f3200689

# 配置
## swooleyaf环境安装
    详情参见文件: initcentos7/swooleyaf/helper_swooleyaf.md

## sywaf防火墙
    详情参见文件: resources/nginx/lualib/helper_sywaf.md

# 命令
## swooleyaf环境(CentOS7)
    //使用帮助
    /usr/local/python3/bin/fab -f fabfile.py envHelp