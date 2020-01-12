# 使用simh安装unix7

## 准备工作
#### simh

SIMH is a highly portable, multi-system simulator.

SIMH implements simulators for:
* Data General Nova, Eclipse
* Digital Equipment Corporation PDP-1, PDP-4, PDP-7, PDP-8, PDP-9, PDP-10, PDP-11, PDP-15 (and UC15), VAX11/780, VAX3900
* GRI Corporation GRI-909, GRI-99
* IBM 1401, 1620, 7090/7094, System 3
* Interdata (Perkin-Elmer) 16b and 32b systems
* Hewlett-Packard 2114, 2115, 2116, 2100, 21MX, 1000, 3000
* Honeywell H316/H516
* MITS Altair 8800, 8080 only
* Royal-Mcbee LGP-30, LGP-21
* Scientific Data Systems SDS 940
* Xerox Data Systems Sigma 32b systems

unix6和unix7运行在PDP-11上，详细文档见 http://simh.trailing-edge.com/pdf/pdp11_doc.pdf 

项目代码地址：https://github.com/simh/simh


#### unix7相关资料

下载安装文件 http://simh.trailing-edge.com/kits/uv7swre.zip
打开有以下文件:
* AncientUnix.pdf
* README.txt
* unix_v7_rl.dsk


## 安装步骤

#### step1：boot

1. 创建启动文件 boot.ini
内容如下：
```
set cpu 11/45
set cpu 256k
set rl0 RL02
att rl0 unix_v7_rl.dsk
boot rl0
```

2. 执行启动命令

```
pdp11 boot.ini

@boot
New Boot, known devices are hp ht rk rl rp tm vt
:
```
3. 输入启动信息

```
: rl(0,0)rl2unix
```

#### step2：系统设置


1. 设置dev

```
# cd /dev
# make rl
# make tm
```

2. 设置tmp

```
# mkdir /tmp
```

3. 设置swap

```
# /etc/mknod swap b 8 0
# cp /rl2unix /unix
# sync
# sync
# sync
```

#### step3：正常启动

1. 执行启动命令

```
pdp11 boot.ini

@boot
New Boot, known devices are hp ht rk rl rp tm vt
:
```

2. 输入启动信息

```
: rl(0,0)unix
```

3. 正常登入

执行Ctrl-d
输入用户root，回车
```
login: root
Password:
You have mail.
# 
```

此时整个安装步骤完成。

## 资料信息

#### unix资源

* http://gunkies.org/wiki/Setting_Up_Unix_-_Seventh_Edition
* http://gunkies.org/wiki/Installing_v7_on_SIMH
* https://wiki.tuhs.org/doku.php?id=source:unix_archive
