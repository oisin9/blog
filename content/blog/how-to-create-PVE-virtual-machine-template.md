+++
title = "How to Create PVE Virtual Machine Template"
date = "2024-05-10T15:48:46+08:00"
tags = ['PVE','HOW-TO']
+++

1. 首先下载发行版的Cloud Image镜像
2. 创建一个虚拟机

    * 不创建硬盘，SCSI控制器为VirtIO SCSI
    * 在创建好的虚拟机硬件设置中添加CloudInit设备
      
3. 将下载好的Cloud Image上传到PVE服务器，然后使用命令导入

    ```shell
    qm disk import VM_ID CLOUD_IMAGE_FILE.qcow2 STORAGE_POOL
    ```

4. 在硬件中找到未使用的磁盘，双击后，总线设置选择SCSI
5. 在选项-引导顺序中，将此磁盘设置为第一项，同时把硬件中的CDROM删除
6. 调整cloud-init中的配置
7. 扩容硬盘后即可启动VM
