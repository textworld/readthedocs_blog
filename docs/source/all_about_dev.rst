所有有关本地开发环境
===================================

docker
*************

数据库
++++++++++

数据导出
----------


下面给出一个在git bash中导出数据库的命令，通过在容器中通过mysqldump命令将一整个数据库导出为文件backup2.sql。
.. code::

    docker exec 144c93 sh -c 'exec mysqldump  --default-character-set=utf8mb4 -uroot -p"root" jeecg-boot' > backup2.sql

144c93表示的是容器id，数据库用户和密码均为root，jeecg-boot是本次需要导出的目标数据库名称。
