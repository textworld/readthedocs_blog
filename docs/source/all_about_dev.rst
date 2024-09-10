所有有关本地开发环境
===================================

wsl2开发环境
***********************************

常用软件安装
+++++++++++++++++++++++++++++++++++

nodejs
-----------------------------------

ubuntu22.04环境下，通过nvm安装nodejs环境。

.. code::

    sudo apt-get remove libnode-dev
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get install nodejs-dev
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
    source ~/.bashrc
    nvm install 14.17.0  # Example version
    nvm use 14.17.0

python环境安装
-----------------------------------

ubuntu22.04 wsl2中安装python环境。

.. code::
    
    sudo apt install python3-pip
    pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
    pip install virtualenv

cuda
-----------------------------------

.. code::

    ===========
    = Summary =
    ===========

    Driver:   Not Selected
    Toolkit:  Installed in /usr/local/cuda-12.5/

    Please make sure that
    -   PATH includes /usr/local/cuda-12.5/bin
    -   LD_LIBRARY_PATH includes /usr/local/cuda-12.5/lib64, or, add /usr/local/cuda-12.5/lib64 to /etc/ld.so.conf and run ldconfig as root

    To uninstall the CUDA Toolkit, run cuda-uninstaller in /usr/local/cuda-12.5/bin
    ***WARNING: Incomplete installation! This installation did not install the CUDA Driver. A driver of version at least 555.00 is required for CUDA 12.5 functionality to work.
    To install the driver using this installer, run the following command, replacing <CudaInstaller> with the name of this run file:
        sudo <CudaInstaller>.run --silent --driver

    Logfile is /var/log/cuda-installer.log


使用docker进行日常开发
***********************************
本小节主要记录，在windows环境下使用docker进行日常开发。

使用docker对db容器进行数据的导入导出
+++++++++++++++++++++++++++++++++++


数据导出
-----------------------------------


下面给出一个在git bash中导出数据库的命令，通过在容器中通过mysqldump命令将一整个数据库导出为文件backup2.sql。
.. code::

    docker exec 144c93 sh -c 'exec mysqldump  --default-character-set=utf8mb4 -uroot -p"root" jeecg-boot' > backup2.sql

144c93表示的是容器id，数据库用户和密码均为root，jeecg-boot是本次需要导出的目标数据库名称。

.. attention::
    请在git bash下面使用。在powershell中可能会遭遇乱码问题。

数据导入
-----------------------------------

.. code::
    docker exec -i jeecg-boot-mysql mysql -u root -proot < a.sql



其他问题
***********************************

设置代理
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



IDEA全局搜索快捷键失效不起作用
+++++++++++++++++++++++++++++++++++

大概率是搜狗输入法占用了快捷键Ctrl+Shift+F
.. attention::
    请在git bash下面使用。在powershell中可能会遭遇乱码问题。





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