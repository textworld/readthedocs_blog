所有有关本地开发环境
===================================

nodejs环境安装
***********************************

ubuntu22.04
+++++++++++++++++++++++++++++++++++

.. code::

    sudo apt-get remove libnode-dev
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install nodejs-dev
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
    source ~/.bashrc
    nvm install 14.17.0  # Example version
    nvm use 14.17.0




docker
***********************************

数据库
+++++++++++++++++++++++++++++++++++

本章节主要讲述如何在

数据导出
-----------------------------------


下面给出一个在git bash中导出数据库的命令，通过在容器中通过mysqldump命令将一整个数据库导出为文件backup2.sql。
.. code::

    docker exec 144c93 sh -c 'exec mysqldump  --default-character-set=utf8mb4 -uroot -p"root" jeecg-boot' > backup2.sql

144c93表示的是容器id，数据库用户和密码均为root，jeecg-boot是本次需要导出的目标数据库名称。

.. attention::
    请在git bash下面使用。在powershell中可能会遭遇乱码问题。


代理问题
***********************************

docker
+++++++++++++++++++++++++++++++++++

wsl2中设置代理
-----------------------------------

.. code::

    export http_proxy=http://textworld:Aqc_paas@$(cat /etc/resolv.conf | grep nameserver | awk '{ print $2 }'):1080
    export https_proxy=http://textworld:Aqc_paas@$(cat /etc/resolv.conf | grep nameserver | awk '{ print $2 }'):1080

linux host主机设置代理
-----------------------------------

.. code::

    export http_proxy=http://textworld:Aqc_paas@127.0.0.1:1080
    export https_proxy=http://textworld:Aqc_paas@127.0.0.1:1080

powershell中设置代理
-----------------------------------

.. code::

    $env:HTTP_PROXY="http://textworld:Aqc_paas@127.0.0.1:1080"
    $env:HTTPS_PROXY="http://textworld:Aqc_paas@127.0.0.1:1080"


可迁移的配置
***********************************

docker
+++++++++++++++++++++++++++++++++++

docker镜像配置，文件位置 ``C:\Users\admin\.docker`` docker desktop版本4.27.2
.. code::

    {
        "builder": {
            "gc": {
            "defaultKeepStorage": "20GB",
            "enabled": true
            }
        },
        "experimental": false,
        "registry-mirrors": [
            "https://dockerproxy.com",
            "https://docker.mirrors.ustc.edu.cn",
            "https://docker.nju.edu.cn"
        ]
    }

迁移vagrant和virtualbox的数据目录
+++++++++++++++++++++++++++++++++++

Vagrant有一个存放box的目录，默认C:\Users\用户名\.vagrant.d，通过系统变量VAGRANT_HOME来指定。可以通过修改该变量自定义该目录，以达到减少C盘空间占用的目的。

1. 将原有目录中的数据拷贝到新目录。
2. 设置环境变量，设置新的目录地址。

.. code::

    setx MACHINE Brand1