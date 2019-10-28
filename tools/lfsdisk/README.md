# lfsdisk

littlefs 打包工具使用说明（**仅支持 littlefs v2.x 版本**）

## 1. 简介

本文档介绍了 lfsdisk 工具的使用说明，其中大部分内容兼容 FAT 打包工具 fatdisk。

## 2. lfsdisk 使用说明

lfsdisk 是用于把 PC 上本地的一个目录转换成 RT-Thread 上烧写到 flash 上的映像文件工具。一般在 flash 上的映像文件是做为一个 littlefs 文件系统而存在。

命令行：

```
lfsdisk
lfsdisk –f config.xml
lfsdisk –c lfsdisk.bin
```

单独执行 lfsdisk 会按照默认配置文件 `lfsdisk.xml` 中的配置，把里面指定的目录转换成 flash 映像。而使用 `lfsdisk –f config.xml` 时，则使用指定的这个 `config.xml` 文件来做为配置文件进行转换。`lfsdisk –c lfsdisk.bin` 命令可对映像文件 `lfsdisk.bin` 校验并解析其内容。

## 3. 配置文件格式

配置文件 lfsdisk.xml 是以 xml 格式来保存，例子如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<lfsdisk>
   <disk_size>512</disk_size>
   <block_size>4096</block_size>
   <root_dir>lfsdisk</root_dir>
   <output>lfsdisk.bin</output>
   <strip>0</strip>
</lfsdisk>
```

其中 

* disk_size 指定了生成的映像文件空间大小，单位是 Kbytes。
* block_size 指定了生成映像文件的块大小，一般设置为 4096，单位是 Bytes。
* root_dir 指定 PC 上要转换目录名。
* output 指定生成的映像文件名称。
* strip 可以取 0 或 1，当是 0 时，生成的映像文件大小等于 disk_size；当是 1 时，则会根据映像文件的情况，如果后面是 `0xFF`，则把 `0xFF` 的部分不生成在内。


